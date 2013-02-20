---
layout: post
title: Sequelize, the JavaScript ORM, in practice
published: true
tags:
- NodeJS
excerpt: "Node.js is well-know for its good connectivity with NoSQL databases. A less know fact is that it's also very efficient with relational databases. Among the dozens ORMs out there in JavaScript, one stands out for relational databases: Sequelize. It's quite easy to learn but there are not many pointers about how to organize model code with this module. Here are a few tips we learned by using Sequelize in a medium size project."
image: /images/nodejs-mysql.png
---
Node.js is well-know for its good connectivity with NoSQL databases. A less know fact is that it's also very efficient with relational databases. Among the dozens ORMs out there in JavaScript, one stands out for relational databases: [Sequelize](http://www.sequelizejs.com/). It's quite easy to learn but there are not many pointers about how to organize model code with this module. Here are a few tips we learned by using Sequelize in a medium size project.

<img src="/images/nodejs-mysql.png" />

## Sequelize 101

Sequelize claims to supports MySQL, PostgreSQL and SQLite. The [Sequelize docs](http://www.sequelizejs.com/#models) explain the first steps with the JavaScript ORM. First, initialize a database connection, then a few models, without worrying about primary or foreign keys:

```javascript
var sequelize = new Sequelize('database', 'username'[, 'password'])
var Project = sequelize.define('Project', {
  title:       Sequelize.STRING,
  description: Sequelize.TEXT
});
var Task = sequelize.define('Task', {
  title:       Sequelize.STRING,
  description: Sequelize.TEXT,
  deadline:    Sequelize.DATE
});
Project.hasMany(Task);
```

Next, create new instances and persist them, query the database, etc.

```javascript
// create an instance
var task = Task.build({title: 'very important task'})
task.title // ==> 'very important task'
// persist an instance
task.save()
  .error(function(err) {
    // error callback
  })
  .success(function() {
    // success callback
  });

// query persistence for instances
var tasks = Task.all({ where: ['dealdine < ?', new Date()] })
  .error(function(err) {
    // error callback
  })
  .success(function() {
    // success callback
  });
```

Sequelize uses promises so you can chain error and success callbacks, and it all plays well with unit tests.

All that is pretty well documented, but the Sequelize documentation only covers the basic usage. Once you start using Sequelize in real world projects, finding the right way to implement a feature gets trickier.

## Model File Structure

All the examples in the Sequelize documentation show all model declarations grouped in a single file. Once a project reaches production size, this is not a viable approach. The alternative is to *import* models from a module using `sequelize.import()`.

The problem is that relationships rely on several models. When you declare a relationship, models from both sides of the relationship must already be imported. You should not import model files from other model files because of Node.js module caching policy (more on that later on); instead, you can define relationships in a standalone file.

Here is the file structure we've been working with:

    models/
      index.js      # import all models and creates relationships
      PhoneNumber.js
      Task.js
      User.js
      ...

And here is how the main `models/index.js` initializes the entire model:

```javascript
var Sequelize = require('sequelize');
var config    = require('config').database;  // we use node-config to handle environments

// initialize database connection
var sequelize = new Sequelize(
  config.name,
  config.username,
  config.password,
  config.options
);

// load models
var models = [
  'PhoneNumber',
  'Task',
  'User'
];
models.forEach(function(model) {
  module.exports[model] = sequelize.import(__dirname + '/' + model);
});

// describe relationships
(function(m) {
  m.PhoneNumber.belongsTo(m.User);
  m.Task.belongsTo(m.User);
  m.User.hasMany(m.Task);
  m.User.hasMany(m.PhoneNumber);
})(module.exports);

// export connection
module.exports.sequelize = sequelize;
```

## Using Models In Code

From other parts of the application, if you need a model class, require the `models/index.js` instead of the standalone model file. That way, you don't have to repeat the Sequelize initialization.

```javascript
var models = require('./models');
var User = models.User;

var user = User.build({ first_name: "John", last_name: "Doe "});
```

The problem is, when you require the `models/index.js` file, Node may use a cached version of the module... or not:

From [nodejs.org](http://nodejs.org/docs/latest/api/modules.html#caching):

>Multiple calls to require('foo') may not cause the module code to be executed multiple times.
>(...)
>Modules are cached based on their resolved filename. Since modules may resolve to a different filename based on the location of the calling module (loading from node_modules folders), it is not a guarantee that require('foo') will always return the exact same object, if it would resolve to different files.

That means that using `require('./models')` to get the models may create more than one connection to the database. To avoid that, the `models` variable must be somehow singleton-esque. This can be easily achieved, if you're using a framework like [expressjs](http://expressjs.com/), by attaching the `models` module to the application:

```javascript
app.set('models', require('./models'));
```

And when you need to require a class of the model in a controller, use this application setting rather than a direct import:

```javascript
var User = app.get('models').User;
```

## Accessing Other Models

Sequelize models can be extended with class and instance methods. You can add abilities to model classes, much like in a true ActiveRecord implementation. But a problem arises when adding a method that depends on another model: how can a model access another one?

```javascript
// in models/User.js
module.exports = function(sequelize, DataTypes) {
  return sequelize.define('User', {
    first_name: DataTypes.STRING,
    last_name: DataTypes.STRING,
  }, {
    instanceMethods: {
      countTasks: function() {
        // how to implement this method ?
      }
    }
  });
};
```

If the two models share a relationship, there is a way. Here, one `User` has many `Tasks`, that makes the `Task` model accessible through `User.associations['Tasks'].target`. And here is yet another problem: since Sequelize doesn't use prototype-based inheritance, how can a `User` instance gain access to the `User` class? Digging into the Sequelize source brings the protected `__factory` to the light. With all this undocumented knowledge, it is now possible to write the `countTasks()` instance method:

```javascript
countTasks: function() {
  return this.__factory.associations['Tasks'].target.count({ where: { user_id: this.id } });
}
```

Note that `Task.count()` returns a promise, so `countTasks()` also returns a promise:

```javascript
user.countTasks().success(function(nbTasks) {
  // do somethig with the user task count
});
```

## Extending models (a.k.a Behaviors)

What if you need to reuse several methods across several models? Sequelize doesn't have a [behavior system](http://propelorm.org/documentation/07-behaviors.html) per se (or "concerns" in the Ruby on Rails terminology), although it's [quite easy to implement](https://github.com/sdepold/sequelize/pull/429). For now, you're condemned to import common methods before the call to `sequelize.define()` and use `Sequelize.Utils._.extend()` to add it to the `instanceMethods` or `classMethods` object:

```javascript
// in models/FriendlyUrl.js
module.exports = function(keys) {
  return {
    getUrl: function() {
      var ret = '';
      keys.forEach(function(key) {
        ret += this[key];
      })
      return ret
        .toLowerCase()
        .replace(/^\s+|\s+$/g, "")    // trim whitespace
        .replace(/[_|\s]+/g, "-")
        .replace(/[^a-z0-9-]+/g, "")
        .replace(/[-]+/g, "-")
        .replace(/^-+|-+$/g, "");
    }
  };
}

// in models/User.js
var friendlyUrlMethods = require('./FriendlyUrl')(['first_name', 'last_name']);
module.exports = function(sequelize, DataTypes) {
  return sequelize.define('User', {
    first_name: DataTypes.STRING,
    last_name: DataTypes.STRING,
  }, {
    instanceMethods: Sequelize.Utils._.extend({}, friendlyUrlMethods, {
      countTasks: function() {
        return this.__factory.associations['Tasks'].target.count({ where: { user_id: this.id } });
      }
    });
  })
};
```

Now the `User` model instances gain access to a `getUrl()` method:

```javascript
var user = User.build({ first_name: 'John', last_name: 'Doe' });
user.getUrl(); // 'john_doe'
```

A limitation of this trick is that you must define behaviors *before* the actual model. This forbids behaviors accessing other models.

## Query Series

Sequelize provides a tool called the `QueryChainer` to ease the resynchronization of queries.

```javascript
new Sequelize.Utils.QueryChainer()
  .add(User, 'find', [id])
  .add(Task, 'findAll')
  .error(function(err) { /* hmm not good :> */ })
  .success(function(results) {
    var user = results[0];
    var tasks = results[1];
    // do things with the results
  });
```

After using it a little, this utility turns out to be very limited. Most notably, `QueryChainer` executes all queries in parallel by default. And you only get access to the results of the queries in the final callback - no way to pass values from one query to the other.

We've found it much more convenient to use a generic resynchronizing module like [`async`](https://github.com/caolan/async), which provides the wonderful [`async.auto()`](https://github.com/caolan/async#auto) utility. This method lets you list tasks together with dependencies, and determines which task can be run in parallel, and which must be run in series.

```javascript
async.auto([
  user: function(next) {
    User.find(id).complete(next);
  },
  tasks: ['user', function(next) {
    Tasks.findAll({ where: { user_id: user.id } }}).complete(next);
  }]
], function(err, results) {
    var user = results.user;
    var tasks = results.tasks;
    // do things with the results
});
```

Notice the `complete()` method, which is an alternative to the two `success()` and `error()` callbacks. `complete()` accepts a callback with the signature `(err, res)`, which is more natural in the Node.js world, and compatible with `async`.

## Prefetching

One thing ORMs are usually good at is minimizing queries. Sequelize offers a prefetching feature, allowing to group two queries in a single one using a JOIN. For instance, if you want to retrieve a Task together with the related User, write the query as follows:

```javascript
Task.find({ where: { id: id } }, include: ['User'])
  .error(function(err) {
    // error callback
  })
  .success(function(task) {
    task.getUser(); // does not trigger a new query
  });
```

This is another undocumented feature, although the documentation [should be updated soon](https://github.com/sdepold/sequelize-doc/pull/20/files).

## Migrations

Sequelize provides a migration command line utility. But because it only allows modifying the model using Sequelize commands (and [not calling any asynchronous method of your own](https://github.com/sdepold/sequelize/pull/433)), this migration command falls short.

As of now, we've been handling migrations manually using numbered SQL files and a custom utility to run them in order.

## Custom SQL queries

Sequelize is built over database adapters, and as such provides a way to execute arbitrary SQL queries against the database. Here is an example:

```javascript
var util = require('util');
var query = 'SELECT * FROM `Task` ' +
            'LEFT JOIN `User` ON `Task`.`userid` = `User`.`id` ' +
            'WHERE `User`.`last_name` = %s';
var escapedName = sequelize.constructor.Utils.escape(last_name);
queryWithParams = util.format(query, escapedName);
sequelize.query(queryWithParams, Task)
  .error(function(err) {
    // error callback
  })
  .success(function(tasks) {
    task.getUser(); // does not trigger a new query
  });
```

`sequelize.query()` returns a promise just like other query functions. If you provide the model to use for hydration (`Task` in this case), the `query()` method returns model instances rather than a simple JSON.

Note that you must escape values by hand before concatenating them into the SQL query. For strings, `sequelize.constructor.Utils.escape()` is your friend. For integers, `util.format('%d')` should do the trick.

## Conclusion

Is Sequelize ready for prime time ? Almost. The learning curve is made longer by an incomplete documentation, but most of the features required by a production-level ORM are there. However, I wouldn't recommend it for production just yet if you're not ready to run on your own fork, since the rate at which PRs are merged in the [Sequelize GitHub repository](https://github.com/sdepold/sequelize) is low.