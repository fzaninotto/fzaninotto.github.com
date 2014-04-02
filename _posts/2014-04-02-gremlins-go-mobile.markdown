---
layout: post
title: "Gremlins.js Go Mobile"
published: true
excerpt: "Our monkey testing library for webapps can now simulate touch interactions. Are you ready to stress test your HTML5 mobile app?"
image: /images/mobile_gremlins.jpg
tags:
- JavaScript
- test
---
<img src="/images/mobile_gremlins.jpg" class="postImage"/></a>

The success of the [gremlins.js](http://redotheweb.com/2014/01/07/completing-the-js-test-stack-introducing-greminsjs.html), a monkey testing library for webapps, took me by surprise. In the course of two weeks, the library was featured on [DailyJs](http://dailyjs.com/2014/03/11/gremlins-customsync/), [webappers](http://www.webappers.com/2014/03/12/gremlins-js-simulates-random-user-actions/), [Hacker News](https://news.ycombinator.com/item?id=7426026), [Reddit](http://www.reddit.com/r/javascript/comments/20qj1j/gremlinjs_throw_a_thousand_monkeys_to_your_page/), [korben.info](http://korben.info/faites-tester-votre-code-par-des-millions-de-petits-singes.html) (a huge French tech news site), and [habrahabr.ru](http://habrahabr.ru/post/216805/) (a huge Russian tech news site). It's been on the [top 5 trending repositories on GitHub](https://github.com/trending?since=monthly) for days, and more than 4,000 GitHub users have already starred the repository. 

I'm delighted that this piece of work, crafted by several marmelab developers, got such attention. It's very encouraging, and it confirms us that the current trends in web development (where logic moves to the browser) requires new tools.

The greatest result of this high attention is that new contributors start suggesting and implementing new features. The first significant contribution has just been merged, and is now available for all. It's called the [toucher Gremlin](https://github.com/marmelab/gremlins.js/blob/master/src/species/toucher.js).

Gremlins simulate all kinds of interactions on a webapp, but most of our testing was restricted to desktop browsers so far. By simulating touch events (tap, double-tap, drag, pinch), the new toucher gremlin opens the door to mobile web applications. Look at how gremlins play with the Google Maps mobile web application:

<img src="/images/gremlins_touch.gif" />

Mobile browsers are the first concerned by memory leaks and bad event subscription, so monkey testing is especially useful on such platforms. Thanks to [the contribution of Jorik Tangelder](https://github.com/marmelab/gremlins.js/pull/56), gremlins will now be able to swarm everywhere a touch screen is available. 

Happy mobile gremlins testing!
