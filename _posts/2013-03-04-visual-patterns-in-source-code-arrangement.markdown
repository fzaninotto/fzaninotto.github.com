---
layout: post
title: Visual Patterns in Source Code Arrangement
published: true
excerpt: If you take a bird's-eye view on a code repository using data visualization techniques, some visual patterns emerge that can help refactoring, team collaboration, and maintenability. This post illustrates a few patterns found using CodeFlower, an open-source code visualization tool I recently released.
image: /images/codeflower/codeflower.png
popular: true
---
Source code arrangement is a matter of debate. What would you consider a good practice for the number of lines of code per file, the number of files per directory, the total number of files in a project? To help answer these questions, one must see the big picture: how does a project code look from a bird's eye view? [CodeFlowers](http://redotheweb.com/CodeFlower) are a way to look at code layouts in a graphical way. Using it on various projects, you quickly see some visual patterns emerge.

## The Mistletoe

One very large file (greater than 500 lines of code) among a tree structure of normal size files. This file looks out of place, I call it the **mistletoe**. Whether it's a CSS or a list of utility methods, dealing with large files is often a developer's nightmare. It's a good start for a refactoring session: split the mistletoe into several files, it will disappear.

![The Mistletoe](/images/codeflower/mistletoe.png)

## The Dandelion

A directory with a lot (more than 30) very small files. It's so familiar that you want to blow on it to scatter the seeds: I call it the **dandelion**. You often find dandelions in internationalized projects, where translation files are numerous and lie in the same directory. They may not be problematic, until the number of files becomes really too big, and developers find it hard to find the one they're looking for.

![The Dandelion](/images/codeflower/dandelion.png)

## Twigs

Several thin branches, not many leafs: meet the **twigs**. This is a deep directory structure that requires a lot of clicks to browse, where the number of files per directory (one or two) is suboptimal. I see this pattern a lot in [PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md) projects, because the class naming rule imposes a deep directory structure. Try to regroup leafs on a single branch to make your fellow developers happier.

![Twigs](/images/codeflower/twigs.png)

## Twin Branches

Two branches that look the same: this is often caused by a test class layout following the library layout - and it's a good practice. Don't panic if you see **twin branches**, they make the tester's life easier.

![Twin Branches](/images/codeflower/twin_branches.png)

## Grapes

Many very large files attached to the same branch: that's the **grapes**. The files are so big and so numerous that the leafs overlap on the visualization. It makes it difficult to tell one file from the other. It's equally difficult for developers to work with such code layouts. This is often representative of aging libraries, where not enough time was spent on refactoring. But if you see only grapes in a CodeFlower, it may also be because you're looking at a program which uses a very verbose language.

![Grapes](/images/codeflower/grapes.png)

## The Sunflower

A very large flower with regular petals, and several directory levels, is a pattern I call the **sunflower**. You may find it in projects where a library is declined several times, or where several sets of data using the same layout are required. It's not a problem as long as the directories composing it are properly named.

![Sunflower](/images/codeflower/sunflower.png)

## Did You See Other Patterns?

If you spot other patterns, feel free to share them here. Code layout is a matter of taste of course, but there are common practices that are interesting to discuss.
