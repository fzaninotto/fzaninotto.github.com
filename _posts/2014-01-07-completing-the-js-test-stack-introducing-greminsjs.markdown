---
layout: post
title: "Completing the JavaScript Test Stack: Introducing Gremlins.js, a Monkey Test Library For Web Apps"
published: true
excerpt: "Persistent JavaScript applications require more attention on memory management, applicative robustness, and edge cases. How do you test that? Stress testing HTML5 and Node.js applications is made easy with this new Monkey Testing library from marmelab."
image: /images/gremlins.png
tags:
- JavaScript
- test
---

<img src="/images/gremlins.png" class="postImage"/>

Persistent JavaScript applications require more attention on memory management, applicative robustness, and edge cases. How do you test that? Stress testing HTML5 and Node.js applications is made easy with this new Monkey Testing library called [gremlins.js](https://github.com/marmelab/gremlins.js) we've just released.

## The JavaScript Testing Stack

JavaScript, on the frontend and the backend, is a pretty mature environment. Most testing tasks are covered by established and stable libraries, among which:

* Unit testing with [Mocha](http://visionmedia.github.io/mocha/)
* Behavior-Drvien development with [Jasmine](http://pivotal.github.io/jasmine/)
* Regression testing and browser automation with [Selenium](http://docs.seleniumhq.org/)
* Performance testing with [WebPageTest](http://www.webpagetest.org/) and the [Chrome Developer Tools](https://developers.google.com/chrome-developer-tools/)

But one testing task still misses a proper tool in the JavaScript world: *stress testing*.

## What Is Stress Testing?

Stress testing means testing an application under a high load of intense interactions. The goal is simple: determine the breaking point, and ensure that the application will remain stable when used in a normal environment.

After all, you can't release an application in the wild without knowing how many concurrent users it can safely support, right? And you can't know for sure that it supports a given capacity until you have tested a *way higher* level.

One way to achieve stress testing is to repeat a given usage scenario a lot of times, very quickly. The problem is that this may prove that an application is robust enough to support a high number of concurrent users doing the same thing, but it will not prove that the application is robust *per se*.

You see, users tend to behave all in a different way. They won't ever follow the scenarios you imagined. Users are uncontrollable. Users sometimes even behave like monkeys, typing everywhere on the screen to see if there is something behind that link.

## Monkey Testing

Enter *Monkey Test*, a particular type of stress test. Imagine a horde of monkeys deliberately typing random keys, clicking on random parts of the screen, or lying on the wifi access point to slow it down. Simulating this type of random input with a very high frequence is a very good way to test the robustness of a GUI, and of an entire application.

Monkey test is pretty common in mobile applications development. The Android SDK comes with an [Application Exerciser Monkey](http://developer.android.com/tools/help/monkey.html). If an Android application can resist 10,000 random simulated user events without crashing or freezing, then you can be pretty sure it won't break with the first user.

The term *monkey* comes from the [Infinite Monkey Theorem](http://en.wikipedia.org/wiki/Infinite_monkey_theorem), which states that 'a thousand monkeys hitting keys at random on a typewriter keyboard for an infinite amount of time will almost surely type out the entire works of Shakespeare'. But in Monkey Testing, the purpose of the monkey actions is not to create a work of art. It's to break an application. In my opinion, this type of animal looks more like gremlins.

## Gremlins.js

There was no monkey testing library in JavaScript. We've built one: it's called [Gremlins.js](https://github.com/marmelab/gremlins.js), and it's ready to break your applications apart. Usage is super simple:

```html
<script src="path/to/gremlins.min.js"></script>
<script>
gremlins.createHorde().unleash();
</script>
```

You will see gremlins actions on screen, and the errors they trigger on the console: 

![Gremlins in action](https://github-camo.global.ssl.fastly.net/5895c92cb175ca71bf580802e1af3a15a7046b69/687474703a2f2f6d61726d656c61622e636f6d2f6772656d6c696e732e6a732f696d672f746f646f2e676966)

You can customize everything. How many gremlins are unleashed, what type of actions they do, the attack strategy they use, everything. Gremlins, in this library, are just plain JavaScript functions. So it's very easy to create new gremlins, specially trained to break your own application:

```js
gremlins.createHorde()
  .allGremlins()
  .gremlin(function jQueryKiller() {
    // whack!
    window.$ = function() {};
  })
  .unleash();
 ```

Gremlins.js is open-source, released under the MIT Licence, [fully documented](https://github.com/marmelab/gremlins.js/blob/master/README.md), and waiting for your feedback.

## Why JavaScripts Needs This

MV* applications (Angular.js, Backbone.js, d3.js, etc) are persistent applications. The DOM redraws, the garbage collections, the memory leaks, all these new problems appear because we don't throw away web pages after a single use anymore. JavaScript Frontend developers are currently meeting the same problems that compiled application developers on environments with limited capabilities (read: mobile developers) met years before.

They need the same tools. We need to stress test our web applications, to detect leaks and cracks before our users. Gremlins.js is a step in that direction. Make good use of it!
