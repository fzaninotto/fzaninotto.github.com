---
layout: post
title: Should You Commit Your Dependencies?
published: true
excerpt: Due to modular design, package managers are now a crucial element in the web development workflow. But they are slow. Composer, bundler, bower, npm and the likes cost hours of lost development time every week. Committing dependencies to the SCM seems a good idea to speed things up. But is it really that fast, and what are the drawbacks?
image: /images/gavage.jpg
tags:
- development
- NodeJS
- php
popular: true
---

<a href="/images/gavage.jpg"><img src="/images/gavage.jpg" class="postImage"/></a>

Due to modular design, package managers are now a crucial element in the web development workflow. But they are slow. Committing dependencies to the SCM seems a good idea to speed things up. But is it really that fast, and what are the drawbacks?

Package Managers Are Slow
-------------------------

Our applications rely on more and more third-party components. One consequence is that when you checkout your application code, you're far from done. You need to run `bundle install`, or `bower install`, or `composer install`, or `npm install` to grab all dependencies and let the application run. 

The problem? Package managers sometimes can't multiplex HTTP requests. Dependencies themselves have dependencies, so package managers may only multiplex a subset of packages. Just pinging a package manager to look for updates takes time when you have dozens of dependencies. Dependency resolution is not immediate. Package managers sometimes download the whole code history of each dependency to ease future updates.

I'm aware that you can bypass dependency resolution by committing a `.lock` file. Each dependency manager has its own optimizations - see for instance [some speedup tips for `composer`](http://moquet.net/blog/5-features-about-composer-php/). Caching makes updates faster. All these techniques may cut the dependency install time by half. But half of ten minutes is five minute, and that's still too slow for each checkout.

Package Managers Must Run Very Often
------------------------------------

Each code checkout must trigger a dependency installation. The Continuous Integration server needs to checkout a pull request to validate it? `bundle install`. You want to run `git bisect` to find a bad commit? `bower install` several times. It's time for a deployment to production? `composer install`. You want to return to the master branch after working on a feature branch? `npm install`.

Developers checkout all the time. Behind each checkout, there is a hidden trap: a dependency update. Did you ever wonder why your application stopped working after a `pull`, and after five minutes realize that another developer had changed the dependency requirements? So now you must a add post-checkout hook to your SCM clients, to verify if the dependency list has changed.

Optimize Dependency Management For Checkout
-------------------------------------------

Git and other modern SCMs have a very optimized workflow for checking out. You just pull the differences. Package managers are not optimized as much. Each dependency needs at least one HTTP request, and that's for modules without dependencies themselves. So if Git is very fast at checking out and package managers are not, why don't developers commit their dependencies?

Think of database denormalization. That's when you update a `nb_comments` counter in the `post` table when adding a new `comment` records. It's a little slower for write queries, but much faster for read queries. We need the same optimization for dependencies. Do the heavyweight dependency job when adding or modifying a dependency (in a write context), not when checking out code (in a read context). Just like database denormalization, it's a step aside the First Normal Form, but it's a necessary optimization.

There are [other reasons to commit your dependenciess](http://addyosmani.com/blog/checking-in-front-end-dependencies/), but speed alone is good enough to motivate the switch.

I hear a few screams in the audience. "Bad practice", "you should only commit your own code", "that's not what SCMs are made for", etc. All valid criticisms. But it's not as if the "pure" solution had only advantages.

How Much Faster Is It?
----------------------

How much faster can dependency management become when committing dependencies? Let's put the idea to the test.

I cloned three web applications repositories from GitHub. In Node.js, I chose my own [Uptime](https://github.com/fzaninotto/uptime). In PHP, it's the [Sonata Sandbox](https://github.com/sonata-project/sandbox). For Ruby, here comes [Diaspora](https://github.com/diaspora/diaspora).

To install a full-featured application using a package manager, it takes two commands: `git clone` and `[packageManager] install`. Using committed dependencies, it's just `git clone`. You can find the full test setup in [this gist](https://gist.github.com/fzaninotto/6534625). 

Here is the average difference across 5 tests for each application, on a relatively fast network:

<table width="100%"><thead>
<tr>
<th>Language</th>
<th>Package Manager</th>
<th>Project name</th>
<th>clone+install</th>
<th>clone with deps</th>
</tr>
</thead><tbody>
<tr>
<td>Node.js</td>
<td>npm</td>
<td>Uptime</td>
<td>81.2s</td>
<td>15.5s</td>
</tr>
<tr>
<td>PHP</td>
<td>composer</td>
<td>Sonata Sandbox</td>
<td>238s</td>
<td>21.2s</td>
</tr>
<tr>
<td>Ruby</td>
<td>bundler</td>
<td>Diaspora</td>
<td>585s</td>
<td>98.0s</td>
</tr>
</tbody></table>
All tests were done with an empty package manager cache, to better reflect an install scenario. That's the worst case. 

For an update, the dependency managers will usually require much less time. But it's not instantaneous. Running `composer.phar install` on the Sonata Sandbox with all dependencies already up to date takes 6 seconds. In comparison, `git pull` takes less than a second in that case.

All in all, committing dependencies is **between 5 and 12 times faster** than using a dependency manager.

Drawbacks
---------

There are a few cases where you should never commit dependencies. When your code is a third-party component, when this code is registered as a dependency in other applications, then committing dependencies clearly doesn't work. Some dependencies require compilation, they are not portable. In this case, you can't commit them. Some dependencies, once installed, have very large elements. GitHub triggers a warning for files larger than 50MB. If you depend on a large `.jar` for instance, you're out of luck.

You can easily commit your dependencies if the package manager downloads tarballs. But package managers sometimes use SCM commands to download dependencies. The result is that the `vendor` directory may contain several `.git` or similar directories. Before committing dependencies, these directories must be cleaned up. That means every time you add or update a dependency. But it's just the matter of running a simple command: `find vendor -name '.git' -type d | xargs rm -Rf`.

Package managers can ignore *development* dependencies in a *production* environment. If you commit your dependencies, you lose this ability and all dependencies are always downloaded. However, you can remove development dependencies in production using a custom command in your deployment workflow.

Committing your dependencies may considerably increase the project repository size. With so many files, your SCM, IDE or search tools may become slower. See for instance [how facebook code makes git slow](http://comments.gmane.org/gmane.comp.version-control.git/189776).

Some development tools may even stop working. `git grep` for instance is a `grep` on steroids which ignores uncommitted files. It's very convenient to search only in the code you develop, and ignore dependencies. But it's useless if you commit dependencies.

Conclusion
----------

Should you commit your dependencies? If you're a purist, or if you're working on a module and not a project, you can't benefit from the boost. If you want a simple development workflow, you should stick with the package manager. 

But if you're upset because of the time you spend everyday waiting for your package manager, if you believe `composer install` is the new ["compiling"](http://xkcd.com/303/), then committing dependencies seems like a good way to increase your development speed.

What's your call? Would you make the switch for the sake of speed, or would you stick with long pauses every day while your package manager checks for new stuff?

I have one little concern: if a significant share of the projects hosted on GitHub commit their dependencies after reading this post, then GitHub may go down. So if you're convinced, please wait for a few days to make the move.
