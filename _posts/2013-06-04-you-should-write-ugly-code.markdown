---
layout: post
title: You Should Write Ugly Code
published: true
excerpt: Some developers know how to tell beautiful code from ugly code. They will criticize you for writing ugly code. I personally think that developers shouldn't care about code beauty, because that's not their job. Instead, they should focus on creating great products, which is infinitely more satisfying.
image: /images/ugly_code.jpg
popular: true
---

<a href="/images/ugly_code.jpg"><img src="/images/ugly_code.jpg" title="Code Extract From https://github.com/WordPress/WordPress/blob/4b13a1ffa473dc7547c33953700e054e47fc4b6c/wp-admin/includes/nav-menu.php" class="postImage"/></a>

Some developers know how to tell beautiful code from ugly code. They will criticize you for writing ugly code. I personally think that developers shouldn't care about code beauty, because that's not their job. Instead, they should focus on creating great products, which is infinitely more satisfying.

Code Fashion
------------

What defines beauty in code? Just like for clothes, opinions on the subject may vary. Each year, we find new trend-setters, like [Jeff Atwood](http://www.codinghorror.com/), [Martin Fowler](http://martinfowler.com/), or [Eric Evans](http://amzn.com/0321125215). They offer convincing arguments to explain why pattern A is better than pattern B. Until someone else publishes a book, explaining that pattern C is much, much better. And that will continue forever, or until there is no developer left on the planet.

Meanwhile, developers try to follow the definition of "beautiful", without necessarily putting it into perspective. Some devs apply coding principles blindly, because they read it in a book. They believe that there is only one way of doing things properly. Like zealots, they explain to their fellow devs that they should change the way they code in order to follow the Principles of Beautiful Code. 

I see lot of such developers in the PHP community these days. Despite having created software that [runs on more than 80% of all the websites whose server-side programming language we know](http://w3techs.com/technologies/details/pl-php/all/all), these developers realized that they totally missed the point by writing procedural code. So they go all-in with sophisticated OOP principles: interface-based programming, [dependency injection](http://fabien.potencier.org/article/11/what-is-dependency-injection), [object calisthenics](http://williamdurand.fr/2013/06/03/object-calisthenics/) form the holy grail of PHP programming these days.

I suspect that in a few years, PHP developers will change their mind and realize that the code they wrote for the sake of beauty is crap. They will probably find a new set of design patterns, or a new programming language, and ask for a Big Rewrite. Just as I think that closely following fashion in clothes is the best way to spend too much money, following coding trends for the sake of code beauty is the best way to spend too much value.

Business Value
--------------

What do developers do? They write programs, but that's really a means to reach a greater goal: creating products. And a product fulfills a service for a user. It may be a product to be used internally by the accountancy team. It might be a commercial SaaS product, to make a living by selling software. But there is always a product on top of a program, because there are users. And why do users use a particular product? Because it brings them a particular value, a value that they are even willing to pay for. That's the business value.

Doing agile product management, and interacting with a product owner during prioritization, is an excellent way to understand the concept of business value. This is especially visible when dealing with refactoring tasks. Let me take an example. 

After three sprints of iterative development on a data visualization webapp, the dev team gathers for the planning poker of the 4th sprint. The lead developer asks for some time to rework the persistence layer. During the early stages, the development team used plain old SQL queries to quickly deliver features. But now that the complexity of the application increases, maintaining custom connection and query classes becomes problematic. Switching to an ORM-based persistence would solve the problem. 

Then the product owner asks: "What will this refactoring task bring to the product?" The lead dev answers that implementing new features on top of the current persistence layer will become more and more expensive. On the contrary, switching to an ORM would reduce the maintenance costs and increase the development speed in the future, even if it brings nothing new to the customer now. In other terms, that's an investment for the future of the webapp. 

There are two possible endings to this story. The product owner may believe that the product has a future, that the balance between new features and cost reduction allows for a pause in new features. That would lead her to prioritize the refactoring on top of the product backlog. Alternatively, she may consider that the product may not be mature enough, that its future is still too uncertain to invest in consolidating tasks, or that the customers would complain about another urgent bug not being fixed soon enough. Both decisions are valid, because that's the product owners choice, based on business value.

Beautiful Is Pointless
----------------------

Let's consider code beauty again, from the angle of business value. When facing an implementation choice, should a developer opt for solution A, which uses ugly code, or for solution B, which is beautiful? That's not the right question: from the end user's perspective, the alternative doesn't make any sense. The user won't look at the code, especially if the product is not good enough to be even tried. So the developer should choose the solution that brings the most value to the product.

The risk is that the product becomes more expensive without any real added value. Would you be willing to buy a piece of furniture twice the normal price because the craftsman uses the most expensive tools available? And what would you think of a poor craftsman who, using poor equipment, manages to create great furniture? Who's the best craftsman of the two?

If a product is good, it will run for a long time. The developers will have the opportunity to improve the inner workings. Take Drupal for instance. On the inside, it show numerous code smells that may repel many developers. Yet it's used by millions of websites. And because of that success, the Drupal core team needs to make Drupal more robust. At the time of writing, Drupal is being migrated to Symfony2 components, which are considered the bleeding edge of code quality for now.

In my opinion, regardless of the design patterns or programming languages you use, if you can make a useful product, you're a talented programmer. If you can make a useful product AND find customers willing to spend more to get beautiful code inside, you're both talented and very lucky. But that probably won't last long, because soon enough one competitor will provide the same service but cheaper, and you will lose your customers.

The only people who can make a living by creating beautiful things that none use are artists. Developers are not artists. They make a living by creating things that people do use.

Should Developers Worry About Code?
-----------------------------------

The title of this post is intentionally provocative. Developers should not be looking forward to writing ugly code. That would mean doing a bad job, and nobody wants to suck at their job. Developers should have pleasure working, and that means writing at least good enough code. 

And once a codebase reaches minimum quality level so that developers are happy working with it, the code quality level should be a feature, in the hands of the product owner.

Fortunately, apart from applying the lessons of the OO paradigm theoricists literally, developers have several other ways to be happy with their job. I find huge satisfaction in building products that are profitable, or that improves people's lives. I love when someone digs in a script I've written, and understands it immediately. I am proud when people build other products on top of products I've developed.

If you're a developer, you have a huge creative capacity in your hand, but you're not an artist. Try to have fun developing *products* more than *programs*.
