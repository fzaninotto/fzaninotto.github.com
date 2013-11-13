---
layout: post
title: "From Objects To Functions: Service Closures"
published: true
excerpt: "Many backend programmers coming to JavaScript try to reproduce the same object-oriented patterns they've been using for long. Although JavaScript does allow object-oriented programming, it's usually not the most idiomatic way to implement a given feature, and its missing one of the greatest aspects of JavaScript: functional programming. See how to switch from OO to functional style with this example on service classes."
image: /images/pacman-closure.jpg
tags:
- development
- JavaScript
---

<a href="/images/pacman-closure.jpg"><img src="/images/pacman-closure.jpg" class="postImage"/></a>

Many backend programmers coming to JavaScript try to reproduce the same object-oriented patterns they've been using for long. Although JavaScript does allow object-oriented programming, it's usually not the most idiomatic way to implement a given feature, and its missing one of the greatest aspects of JavaScript: functional programming. See how to switch from OO to functional style with this example on service classes.

## Service classes

Here is a common use case: a logging service. A PHP or Java developer coming to JavaScript would probably expect the following programming API:

```js
// initialization 
var formatter = new DateFormatter();
var writer = new FileWriter('../logs/dev.log');
var logger = new Logger(formatter, writer); // inject dependencies
// usage
logger.log('hello, horld!');
// writes "13/11/2013 14:53:34 hello, world!\n" to '../logs/dev.log';
```

Using separate formatter and writer classes allows the logger service to be reused for logging into a database, a syslog server, or a distant service. Such an object-oriented API is possible in JavaScript of course, using prototypes to simulate classes:

```js
// formatter service class
var DateFormatter = function() {}; // empty constructor
DateFormatter.prototype.format = function(message) {
    return new Date().toLocaleString() + ' ' + message + "\n";
};

// filewriter service class
var fs = require('fs'); // Node Filesystem utility
var FileWriter = function(path) {
    this.setPath(path);
};
FileWriter.prototype.setPath = function(path) {
    this.path = path;
};
FileWriter.prototype.write = function(message) {
    fs.appendFileSync(this.path, message);
};

// logger service class
var Logger = function(formatter, writer) {
    this.setFormatter(formatter);
    this.setWriter(writer);
};
Logger.prototype.setFormatter = function(formatter) {
    this.formatter = formatter;
};
Logger.prototype.setWriter = function(writer) {
    this.writer = writer;
};
Logger.prototype.log = function(message) {
    message = this.formatter.format(message);
    this.writer.write(message);
};
```

Developers used to object-oriented programming usually feel uncomfortable when dealing with such code, because JavaScript doesn't have interfaces. That means the `Logger` constructor can't ensure that the `formatter` and `writer` services provide a `format()` and a `write()` method.

## From classes to functions

The three service classes defined here may have several methods, they really expose one main method each (`format`, `write`, and `log`). This is true of most service classes: one main method executes the service, the other methods are used to configure the service.

A more idiomatic way to implement services in JavaScript would be to use simple functions, as follows:

```js
// formatter service constructor
var DateFormatter = function() {
    var format = function(message) {
        return new Date().toLocaleString() + ' ' + message + "\n";
    };
    return format;  
};

// filewriter service constructor
var FileWriter = function(path) {
    var fs = require('fs');
    var write = function(message) {
        fs.appendFileSync(path, message);
    };
    return write;    
};

// logger service constructor
var Logger = function(format, write) {
    var log = function(message) {
        write(format(message));
    };
    return log;
};
```

These are functions returning functions. The returned function is a closure: it contains the local variables present during its definition. This is quite common in JavaScript. The usage of the three services is slightly different:

```js
// initialization 
var format = DateFormatter(); // format(message) is a function
var write = FileWriter('../logs/dev.log'); // write(message) is a function
var log = Logger(format, write); // log(message) is a function
// usage
log('hello, horld!');
```

No more `new`, no more `this`, no more method call. It's not object-oriented programming anymore, yet it still follows the good practices of modern programming: separation of concerns, principle of least responsibility, and dependency injection. Incidentally, interfaces are not necessary anymore in this code, since the only thing expected by the `log()` function are functions. *Any* function:

```js
// initialization
var format = function(message) {
    return 'Log: ' + message; 
};
var write = function(message) {
    console.log(msg);
};
var log = Logger(format, write);
// usage
log('hello, horld!');

```

That explains why many JavaScript developers don't feel the need for interfaces and rely on [duck typing](http://en.wikipedia.org/wiki/Duck_typing) without any afterthought.

## Bringing Back Configurability

One thing was lost in the object oriented to functional conversion: the ability to modify a service after creation. The OO implementation exposed methods like `FileWriter.setPath()` and `Logger.setFormatter()`. With the functional version above, it's not possible to modify service settings once the function service has been called. 

But it's very easy to implement it back. In JavaScript, functions are objects, so you can add methods to them:

```js
// filewriter service constructor
var FileWriter = function(path) {
    var fs = require('fs');
    var write = function(message) {
        fs.appendFileSync(path, message);
    };
    write.setPath = function(newPath) {
        path = newPath;
        return write;
    };
    return write;    
};

// logger service constructor
var Logger = function(format, write) {
    var log = function(message) {
        write(format(message));
    };
    log.setFormatter = function(newformat) {
        format = newformat;
        return log;
    };
    log.setWriter = function(newWrite) {
        write = newWrite;
        return log;
    };
    return log;
};
```

The added methods modify the constructor function closure and return the service function again. In addition, they are chainable. Modifying a service after initialization is therefore straightforward:

```js
// initialization
var log = Logger(format, write);
// service modification
log.setFormatter(anotherFormatFunction).setWriter(anotherWriteFunction);
```

This technique may seem weird at first, but it's an elegant and idiomatic way to implement single-function services in functional languages. 

## Even more Idiomatic

Functional services are used extensively in many modern JavaScript libraries, like [d3.js](http://bost.ocks.org/mike/chart/) for instance. Usually, such services use two additional good practices of JavaScript programming:

- dependencies have sensible defaults
- setter functions are also getter functions if no argument is passed.

And since the service constructors are not classes anymore, the naming conventions can drop the leading capital letter.

So the final code for the logger service example, in idiomatic JavaScript, would look like the following:

```js
// formatter service constructor
var dateFormatter = function() {
    var format = function(message) {
        return new Date().toLocaleString() + ' ' + message + "\n";
    };
    return format;  
};

// filewriter service constructor
var fileWriter = function(path) {
    path = path || '/var/log/dev.log'; // default value
    var fs = require('fs');
    var write = function(message) {
        fs.appendFileSync(path, message);
    };
    write.path = function(newPath) {
        // getter if no argument
        if (!arguments.length) return path;
        path = newPath;
        return write;
    };
    return write;    
};

// logger service constructor
var logger = function(format, write) {
    format = format || dateFormatter(); // default value
    write  = write  || fileWriter();    // default value
    var log = function(message) {
        write(format(message));
    };
    log.format = function(newFormat) {
        // getter if no argument
        if (!arguments.length) return format;
        format = newFormat;
        return log;
    };
    log.write = function(newWrite) {
        // getter if no argument
        if (!arguments.length) return write;
        write = newWrite;
        return log;
    };
    return log;
};
```

That way, calling a service constructor without argument makes it use the defaults:

```js
// initialization with defaults
var log = logger();

// custom initialization
var format = dateFormatter();
var write = fileWriter().path('../logs/dev.log');
var log = logger().format(format).write(write);

// read service configuration and dependencies
console.log(write.path()); // '../logs/dev.log'
console.log(log.format()); // [Function]

// usage
log('hello, horld!');
```

## Conclusion

Functions are first class citizens in JavaScript. Classes are not. Most services can be implemented in an elegant way using functions rather than pseudo-classes, so don't hesitate to embrace functional programming, whether you write client-side or server-side code.
