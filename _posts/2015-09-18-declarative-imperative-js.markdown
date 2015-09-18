---
layout: post
title: "Imperative and (Functional) Declarative JS In Practice"
published: true
excerpt: "JavaScript allows for various programming styles. Most programmers use imperative style, but the language also allows declarative style. What's the difference? Let's see that through an example."
image: /images/buildings.jpg
tags:
- JavaScript
---

JavaScript allows for various programming styles. Most programmers use imperative style, but the language also allows declarative style. What's the difference? Let's see that through an example.

## Objective

In this tutorial, I'll show two implementations of a very simple function: `getNestedValue()`, which can help you retrieve a value in a deeply nested object.

```js
/**
 * Get a nested object property by name
 *
 * Supports direct and nested property names (separated by dots)
 *
 *     getNestedValue({ foo: 1 }, 'foo') // 1
 *     getNestedValue({ foo: { bar: 2 } }, 'foo.bar') // 2
 *     getNestedValue({ hello: 'world' }, 'foo.bar') // undefined
 *
 * @param {Object} object
 * @param {String} propertyName
 *
 * @return {Object|String|Number}
 */
export function getNestedValue(object, propertyName) {
    // ...
}
```

The `export` statement is ES6, but it's not important; that's just the way to expose this function to the outside world. It could be `module.exports` in node, or `window.getNestedValue` in the browser. Don't pay too much attention to that.

## Unit tests

Before implementing the function, in good Test-Driven Development style, let's write the unit tests. They will use `mocha` and `chai` for the assertions, but even if you don't know these tools, they're pretty self-explanatory.

```js
const assert = require('chai').assert;

import {getNestedValue} from '../lib/objectProperties';

describe('getNestedValue()', () => {
    it('should return undefined for undefined objects', () =>
        assert.isUndefined(getNestedValue(undefined, 'foo'))
    );
    it('should return undefined for undefined properties', () =>
        assert.isUndefined(getNestedValue({}, 'foo'))
    );
    it('should return the named property if defined', () =>
        assert.equal(getNestedValue({bar: 'baz'}, 'bar'), 'baz')
    );
    it('should return the deeply nested named property if defined', () =>
        assert.equal(getNestedValue({bar: { baz: 1 }}, 'bar.baz'), 1)
    );
    it('should return undefined for a deeply nested named property if undefined', () =>
        assert.isUndefined(getNestedValue({}, 'bar.baz'))
    );
    it('should not accept to get empty property names', () =>
        assert.throws(() => getNestedValue({}, ''))
    )
});
```

There's a little more ES6 here, but don't let that bog your mind:

```js
import {getNestedValue} from '../lib/objectProperties';
// same as
var objectProperties = require('../lib/objectProperties')
var getNestedValue = objectProperties.getNestedValue;

() => {
    // do things
}
// same as
function() {
    // do things
}
```

With the empty function body defined in the first section, it's enough to run the tests. Of course, they won't pass until they are actually implemented.

## Imperative Implementation

The classic approach for most programmers would probably be the following:

```js
export function getNestedValue(object, propertyName) {
    if (!propertyName) throw new Error('Impossible to set null property');
    var subObject = object,
        parts = propertyName.split('.'),
        len = parts.length,
        i;

    for (i = 0; i < len; i++) {
        if (!subObject || typeof subObject === 'undefined') return undefined;
        subObject = subObject[parts[i]];
    }

    return subObject;
}
```

It's perfectly fine, and passes all tests:

```
$ ./node_modules/.bin/mocha --compilers js:babel/register
  getNestedValue()
    ✓ should return undefined for undefined objects
    ✓ should return undefined for undefined properties
    ✓ should return the named property if defined
    ✓ should return the deeply nested named property if defined
    ✓ should return undefined for a deeply nested named property if undefined
    ✓ should not accept to get empty property names

  6 passing (1s)
```

What's "imperative" in this script? The script is basically telling the computer **how** to do something, and as a result what you want to happen will happen. After all, that's what most programmers are taught to do, right? Right, you're usually doing imperative programming without knowing it. Most programmers are the [Monsieur Jourdain](https://en.wikipedia.org/wiki/Le_Bourgeois_gentilhomme) of imperative programming.

## Declarative Implementation

It turns out there is another way: the "declarative" way. In declarative programming, the program tells the computer **what** you would like to happen, and lets the computer figure out how to do it. How does that apply to `getNestedValue()`? See below.

```js
function getValue(object, propertyName) {
    if (!propertyName) throw new Error('Impossible to set null property');
    return typeof object === 'undefined' ? undefined : object[propertyName]
}

export function getNestedValue(object, propertyName) {
    return propertyName.split('.').reduce(getValue, object);
}
```

Sure enough, this completely different implementation passes all tests. It's shorter, less error-prone, and, once you're used to it, more readable. Isn't it?

## Reduce

First thing to notice is the use of `reduce()`. That's a neat JavaScript function that is usually underestimated. According to [the MDN `Array.prototype.reduce()` page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce):

> The `reduce()` method applies a function against an accumulator and each value of the array (from left-to-right) to reduce it to a single value.

`reduce()` takes a function as parameter (it's enough to qualify `reduce()` for the title of ["higher-order function"](https://en.wikipedia.org/wiki/Higher-order_function)). This function argument is executed once for each element in the array (kind of like `forEach()`). But the result of this function execution is passed to the function itself the next time it runs.

```js
function sumArray(values) {
    return values.reduce(
        (previousValue, currentValue) => previousValue + currentValue,
        0
    );
}

sumArray([2, 5, 8]); // 15
```

In this example, you can visualize the three executions of the "accumulator" function:

1. previousValue = 0, currentValue = 2 => return 2 + 0 = 2
2. previousValue = 2, currentValue = 5 => return 2 + 5 = 7
3. previousValue = 7, currentValue = 8 => return 7 + 8 = 15

The most important thing to understand here is that `reduce()` doesn't expose how it iterates over the array. No temporary index, no `for` loop. You don't know **how** it works, but you know **what** it does. It's a perfect declarative statement.

## Composition

The `getValue` function is actually used as a parameter in `getNestedValue` without actually being executed. 

```js
export function getNestedValue(object, propertyName) {
    return propertyName.split('.').reduce(getValue, object);
}
```

Replacing `getValue` by its value, the declarative code could be written as follows:

```js
export function getNestedValue(object, propertyName) {
    return propertyName.split('.').reduce((object, propertyName) => {
        if (!propertyName) throw new Error('Impossible to set null property');
        return typeof object === 'undefined' ? undefined : object[propertyName]
    }, object);
}
```

But it's much less readable than the first snippet, right? By exporting the inner code into the simple `getValue` function, and **composing** it into the second, the code is made much more readable.

One great thing about `reduce()` is that it allows to transform a function designed for scalars to a function working on arrays:

```js
function sum(a, b) {
    return a + b;
}
[2, 5, 8].reduce(sum, 0); // 15
function multiply (a, b) {
    return a * b;
}
[2, 5, 8].reduce(multiply, 1); // 80
```

## No More Temporary Variables

Did you notice? The imperative style requires the definition of four local variables (`subObject`, `parts`, `len`, and `i`), while the declarative style only uses function parameters.

```js
// imperative
export function getNestedValue(object, propertyName) {
    if (!propertyName) throw new Error('Impossible to set null property');
    var subObject = object,
        parts = propertyName.split('.'),
        len = parts.length,
        i;

    for (i = 0; i < len; i++) {
        if (!subObject || typeof subObject === 'undefined') return undefined;
        subObject = subObject[parts[i]];
    }

    return subObject;
}

// declarative
export function getNestedValue(object, propertyName) {
    return propertyName.split('.').reduce(getValue, object);
}
```

Less variable declarations, less questions about variable naming, less questions about variable scope... That's a huge benefit I think. In fact, one thing declarative programming gets out of the way is to manage **state**, and that's a huge relief.

## Conclusion

Which way is the best way? None. It's a matter of coding style, of preference. Some languages (like SQL, regular expressions) force you to use the declarative style. Most languages force you the other way. JavaScript gives you the choice.

The declarative way usually hides the implementation details and lets you focus on the business logic, reducing the amount of code. I tend to love it a bit more every day. I can only advise you to give it a try!

Further pointers:

* [Imperative vs Declarative](http://latentflip.com/imperative-vs-declarative/)
* [Declarative vs. Imperative Programming for the Web](http://www.codenugget.co/2015/03/05/declarative-vs-imperative-programming-web.html)
* [Imperative vs. Declarative Programming - Pros and Cons](https://netguru.co/blog/imperative-vs-declarative)
