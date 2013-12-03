---
layout: post
title: "DotJs 2013: What You Missed, What I Missed"
published: true
excerpt: "The second issue of the DotJs Conference just took place in Paris. The lineup of speakers was really impressive at first sight. Do famous JavaScript software contributors make awesome speakers? Read on for my notes of the talks and a general overview of the conference."
image: /images/dotjseu.jpg
tags:
- conference
- JavaScript
---

<a href="/images/dotjseu.jpg"><img src="/images/dotjseu.jpg" class="postImage"/></a>

The second issue of [DotJs](http://www.dotjs.eu/), the largest European JavaScript conference, took place in Paris, in [an incredible venue](http://www.dotjs.eu/venue) - even better than last year. The [lineup of speakers](http://www.dotjs.eu/) was really impressive at first sight. Names you've heard a lot before if you happen to be doing JavaScript. However, it turns out that famous software contributors are not necessarily awesome speakers. Lastly, the organizers made the choice to book about half of the conference time for networking, which is a bit too much if you can't stay until 9pm.

## Organization

Since last year, the DotConferences team has progressed a lot. The Théâtre de Paris has more comfortable seats than the smaller Théâtre des Variétés, the networking space was large enough to contain the 500+ attendees in good conditions between talks, and the food/beverages were great. All that with a tight budget (registration was below 80€, which is a bargain), which allowed some companies (like [marmelab](http://marmelab.com)) to bring all their developers along.

Great lights and sound (except for the second talk), no downtime between talks in a given session, no time spent waiting for questions from the audience (Sylvain asked all the questions, and the speakers were accessible after their talk in the lobby): all that was great. I can't talk about the Wi-Fi, because I didn't use it - the conference tries to be wireless-less, and I love this idea of spending time actually listening to speakers rather than doing code reviews on Pull Requests between slides.

## Schedule

To my mind, the big downside of the organization was the timing. The schedule has never been made public, so there was no way to guess which speaker would talk, at what time, or about which subject. It's a great way to be surprised, but it's also a great way to be disappointed. The big disappointment for me was that the most interesting speakers went on stage after 6pm. That was very unfortunate: my train was booked for 7pm, and I had no way to know in advance that I would miss what I really wanted to see (Brendan Eich, creator of JavaScript). 

The organizers designed the schedule so as to keep large empty intervals for networking. When I say large, I mean VERY large. The first conference started at 10:45am, followed by a two hours break at lunch, then another 80 minutes break at 4pm. I love to meet new people and share opinions, but this was too much. Especially since I don't live in Paris and had to take a train (but I think it was worse for non-French attendees). Please, next time, start much earlier (9:30am is probably late enough), stop earlier, too (6pm), and leave plenty of networking time *after* the conference for those with more time.

## Talks

The talks were more technical than last year, which is a good thing. I was among the first to mention my disappointment after watching 'Ted'-like talks done by non-'Ted'-like speakers last year. This year, many slides contained heavy duty JavaScript tips and hacks. But again this year, I'm a bit disappointed. I leave the conference without the urge to test a new piece of technology, without the inspiration to start doing things in a new way, without the impression to have been changed by what I saw. And this is what I really expected.

Here is an extract from my notes for the speeches.

### Addy Osmani - JavaScript tooling, web Components, and Polymer

No need to introduce Addy, famous Googler and JavaScript developer (Yeoman, TodoMVC, Aura). Addy took a few minutes to remind us of his talk from last year (about Yeoman), and introduced [Polymer](http://www.polymer-project.org/), a framework to encapsulate domain logic into new HTML markup, translating either to Web Components or to JavaScript Polyfills. "Markup can be meaningful again". Polymer looks very promising (not only to resuscitate the `<blink>` tag). Addy made a demo of a video player using AngularJS and new polymer elements. He also bootstrapped a Polymer application with Yeoman.

I'd like to try out Polymer in the future, but I wonder why two different teams at Google work on similar subjects with different libraries (since Angular has a similar approach with Directives). Anyway, great talk.

### John K Paul, Type Dependence ([slides](http://johnkpaul.github.io/presentations/dotjs/2013/js-tools/))

John's talk was targeted at Java developers who miss the features of a strongly typed language in JavaScript. The assumption that this represented a large share of the audience, was, to me, audacious at best. 

John listed tools allowing to check and enforce conventions in JavaScript, from syntax checkers and linters to deeper static analysis tools like [plato](http://jsoverson.github.io/plato/examples/jquery/). This might seem new to JavaScript developers coming from the frontend side, but I think that backend developers have been using such tools in other languages for years, including pre-commit hooks to enforce the rules. Lastly, John introduced TypeScript as THE solution for enforcing types in JavaScript. I personally think that if Java developers don't want to do duck typing, they might as well stay with Java. For me, strong types and strict coding standards only make sense on very large projects, and the JavaScript ecosystem is not completely ready for such projects anyway. 

### Remy Sharp, on IFrames ([slides](https://speakerdeck.com/rem/iframe-a-less-than-useful-look-at-the-abuse-the-iframe-takes))

A funny and informative talks about all the hacks you can (still) do with iFrames, from achieving cross-domain communication to preventing clickjacking. I can't list all the small hacks he listed, but I'm sure Remy has accumulated a huge experience with iframes while iterating on the [jsbin.com](jsbin.com) service. These hacks would be very useful in 2006, they look less appealing today, even if they still solve actual problems. I think this list of tips would have made a great blog post, easier to bookmark than a conference. But anyway, Remy's talk was entertaining. It's just not the image I want to keep about JavaScript...

### Lightning talks

5 lightning talks (4 minutes each) followed, dealing with hybrid mobile apps, integration testing, memory leak investigation in the browser, HTML5 audio synchronization, and NodeJs deployment. I like the lightning talk format: speakers have to be very well prepared, they have to pack only the most valuable information, and make the audience laugh to convince. Many good ideas to investigate, including using Passenger for Node.js deployment, exploring the heap using d3.js, or bundling behavior tests with web components. 

### Nicolas Belmonte, on Operator overloading in JS

Although famous for his data visualizations, Nicolas chose to focus on a very prospective subject, the ability to overload operators (like `+` and `*`) in JavaScript. This is motivated by the need to manipulate vector objects in WebGL visualizations - although GLSL, the C-like DSL for programming WebGL, already does that. A half of the talk was a reminder about the history of failed attempts to bring operator overloading to JavaScript, and the conclusion was that it's still nowhere to be seen. 

I have learned a few things about the WebGL stack, but I'd have preferred a more inspiring talk than an exploration of a tiny technical niche without any implementation in sight. 

### Dave Methvin, "JS Performance on the browser's world"

After a quick introduction about client-side performance, Dave, who is now the jQuery Lead Developer, focused on solving the problem of forced layouts. "Premature optimization is the root of all evil", as we all know, and we already have the tools to detect and fix frontend performance bottlenecks (in Google Chrome and IE11).

Dave was a good speaker, used plenty of examples to illustrate his concerns, and overall did a good job at raising the audience's awareness of web performance topics. I had already watched [a talk on the same subject from the Velocity Conference](http://www.youtube.com/watch?v=UrKA5j-yx8Y), so I didn't learn anything new, but I guess it was an interesting subjects when you're new to WebPerf.

### Guillermo Rauch, The need for speed ([slides](https://cloudup.com/iuO7joTPdLr))

Another talk about frontend optimization of one-page webapps, illustrated by real-world examples taken from the [cloudup](http://cloudup.com) service, where Guillermo works. Guillermo is famous for his work on socket.io, Mongoose, and [mydb](https://github.com/cloudup/mydb). He's also a good teacher. He showed a few tricks to give the impression of speed, get rid of spinners, and improve reactivity of data synchronization. I missed some kind of perspective from his talk - a compilation of tricks doesn't make a doctrine.

### James Burke, "Module Frontiers" ([slides](http://jrburke.com/talks/dotjs2013/))

The involuted talk of the day. If you're not developing a RequireJS/AMD clone, you probably didn't miss anything from James' exploration of the future module standards of EcmaScript 6 (not yet finished, not yet implemented, imperfect, and abstract). I must admit I didn't follow half of the talk - too arcane for me.

### Nicolas Geoffray on Dart.js

The performance of Nicolas was to improvise a 25 minutes talk in a single week-end, despite having to watch his kids and being a substitute for the creator of the V8 engine, Lars Bak. I know that I need an approximately one hour of preparation for one minute of talk when I'm on stage, so kudos to Nicolas for that.

After a funny preamble, Nicolas introduced Dart, yet another language by Google, which compiles to JavaScript, and focused on performance. Dart is not a superset of JavaScript (that would be TypeScript), it is not a subset either (that would be asm.js). It's just the language that Google would like us to use instead of JavaScript for the web. They have developed a runtime which executes Dart about twice as fast as the equivalent JavaScript, only in Chrome. Frankly, considering the size of the JavaScript ecosystem, I don't see us switch to Dart. Especially when a simple "Hello, World" in Dart compiles to 2,500 bytes of JavaScript. 

### Alex Sexton, "Practicing Safe Script"

An informative and entertaining talk about web security, how important and how hard it is. Some of the great quotes I heard from this talk: to reach a good security level, "all you have to do is never make a single mistake", which is impossible since security specialists "discount the probability of perfection".

Alex illustrated a few of the common security pitfalls in (frontend) web development, including Content Injection (via XSS), and CSS hacks. Content injection is impossible to detect using regexps (don't even try), and CSS hacks are impossible to mitigate because of timing attacks. 

Too bad I couldn't see the conclusion of this talk because of the late hour, it was one of the best talks of the conference. 

I couldn't see the talks of Pamela Fox, from the Khan Academy, or of Brendan Eich, creator of JavaScript. I'm really disappointed about that, the schedules were really inadequate for me.

## Conclusion

The conference was a great step forward when compared to last year. Even if I missed inspiring talks, I had the opportunity to meets great people, to talk with lots of JS devs, and to witness the strength of the JavaScript European community. It was also a good pretext to gather all marmelab developers in Paris! Thanks to the organizers and sponsors for making this possible. The next issue will be, I'm sure, even better!

Did you enjoy the conference as much as I did? Feel free to comment below to share your view about the talks and organization.
