---
layout: post
published: true
title: "\"I Hate JavaScript\""
excerpt: "Oh really, you hate JavaScript? Or maybe you hate PHP? Or a specific framework for a specific language. Let me challenge that hate. Or better, let me talk about love instead."
image: images/love_hate.jpg
tags:
- Node.js
- JavaScript
- PHP
- Symfony
---

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/procsilas/131462019" title="you choose"><img src="https://farm1.staticflickr.com/48/131462019_36bb4ce0c0_b.jpg" class="medium" alt="you choose"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

I've heard that sentence a lot during [the latest PHP conference I attended](http://pariscon2015.symfony.com). I also heard "I hate PHP" many times during [JavaScript conferences](http://www.dotjs.io). And don't get me started on Python developers, who seem to despise anything that doesn't have ["The Zen"](https://www.python.org/dev/peps/pep-0020/).

It makes me sad.

## You Don't Know What You Hate

"_I hate JavaScript: it's spaghetti code all over, with all these callbacks and events and whatnot_". Well, you don't hate JavaScript, you hate poor jQuery code. Take a look at how people write modern JavaScript ([React](https://facebook.github.io/react/)/[Redux](http://redux.js.org/) is a great example).

"_I hate Node.js: it's based on a language that was written in 10 days by a guy called Brendan_". Wake up dude, JavaScript has evolved a lot since then. Take a look at [ES2015](https://babeljs.io/docs/learn-es2015/), it's a joy to read and write.

"_I hate PHP, it has curly braces_". It also has some of the most active open-cource communities, [awesome frameworks](http://symfony.com) and libraries, maintained for real by passionate and skilled developers.

"_I hate PHP, it's so slow_". Unless you learn to profile your code correctly, and detect the bottlenecks you added by mistake, or switch to a faster implementation (PHP7, HHVM). Did you know that [PHP powers Facebook](https://www.facebook.com/notes/facebook-engineering/speeding-up-php-based-development-with-hiphop-vm/10151170460698920)?

"_I hate PHP, it doesn't handle asynchronicity/channels/functional programming_". What if the programs written in PHP don't actually need to deal with that?

My point is: ALL the people I hear saying that they hate a language hate it for the wrong reasons. By expressing their hate, they mostly show their incompetence.

## Haters Gonna Hate

Haters don't need another language to hate. Alternative frameworks are perfect targets, too. "Laravel is crap, it's so much worse than Symfony". And even if your neighbor uses the same framework as you do, you'll probably look disgusted when you see that they chose the "FooBar" authentication plugin for that framework.

Did you notice? The first thing many developers do when they open a source file that they didn't write themselves is to say: "Ew, this is crap" - even if it's using their preferred technology stack. It sometimes happen when they open a script they wrote themselves a couple years ago, too.

That's just snobbery. Maybe those developer don't just hate PHP. Maybe they hate programming. Maybe they just hate.

It reminds me of these countryside villagers who hate the people from the closest village just because they live a few kilometers away from each other. In a hyperconnected world, this sounds stupid, don't you think? Well, that Laravel developer is your neighbor. Maybe he didn't choose where he was born, but he grew up to learn and love the place. I don't see anything bad about that.

## There Is No Silver Bullet

Why are there so many programming languages? Because we need them.

Some languages are easy to learn, some have built-in concurrency support, some are completely object-oriented, some are compiled, some are statically typed, etc. Just like there is an infinity of project types, and an infinity of programmer types, we need diversity in programming languages.

Oh, and if there was one language so much better than all the others, don't you think that the entire world would already be using only this language? Right, [that didn't happen](https://en.wikipedia.org/wiki/Comparison_of_programming_languages).

## We Can't Stick To A Single Programming Language For Our Entire Life

So you're convinced that Ruby on Rails is the single and only tool that you'll ever use, because it does everything, and it does everything right.

Fast-forward 20 years from now. The only projects you're working on are legacy programs that nobody wants to maintain anymore. Modern languages offer higher abstraction levels, and every normal programmer now considers Ruby on Rails the same way you used to consider Assembly. You now picture yourself as a [Cobol developer](https://www.google.com/search?q=cobol+developer&tbm=isch). You're still far from being retired, but you're already a _has been_.

Let's go back to today. The MVC architecture, once a (rediscovered) breakthrough for web applications, makes little sense when all you need is a storage layer exposed over HTTP. Full-stack frameworks were a great fit for monolith applications. But for API-centric architectures, maybe we need to find other tools. Good practices evolve, languages evolve, customers ask for new things (real time communication, rich UX, AI, mobile apps, you name it), so programmers must evolve, too.

## Learn To Love the (Tech) Differences

We can learn something new from every language. [Scala](http://www.scala-lang.org/) makes functional programming obvious. [Flux](https://facebook.github.io/flux/) simplifies the update workflow of user interfaces like never before. [WinDev](http://www.pcsoft.fr/windev/) uses French to name functions, which is great for programmers who never learned English (and love naked women). When I meet someone doing something else than what I do, I try to detect the good ideas, the good practices that I could reuse. I love to learn from other people's experiences.

I dream about a tech conference that would not be centered around a particular technology. A tech conference mixing several developer cultures, without any preconception, but a single purpose: open our minds.

Stop hating. Start learning. Also, please, next time we meet, tell me what you love.

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/75626794@N02/22613180594/in/pool-forumphp2015/" title="IMG_4369"><img src="https://farm1.staticflickr.com/567/22613180594_ee70f89b7c_b.jpg" class="medium" alt="IMG_4369"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
