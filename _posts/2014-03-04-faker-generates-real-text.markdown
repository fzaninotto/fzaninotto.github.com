---
layout: post
title: 'Faker Now Generates Real Text'
published: true
excerpt: Faker can now generate random text in English, French and German. Read on to see how the Makov Chains generator algorithm can help you get good-looking fake text for your locale.
image: /images/book_page.jpg
tags:
- faker
- php
---

<a title="A page from 'The Captain's Daughter' by  Alexander Pushkin. Public domain image from http://www.publicdomainpictures.net/view-image.php?image=10787&picture=page" href="http://www.publicdomainpictures.net/view-image.php?image=10787&picture=page"><img src="/images/book_page.jpg" class="postImage"/></a>

Faker has always been able to generate random text, based on a "lorem ipsum" corpus. But Faker generated test is gibberish in all countries, and misses the particular language structures of certain languages. Today, Faker introduces a new real text generator, which produces "almost understandable", although completely random, portions of text.

## Usage

In addition to the old `text()` formatter, Faker now exposes a new `realText()` formatter:

```php
<?php
$faker = Faker\Factory::create('en_US');
echo $faker->realText(); // generates a random string of 200 characters at most
```

> Alice, as the jury had a little door about fifteen inches high: she tried the effect of lying down with wonder at the stick, and held out its arms folded, frowning like a telescope. And so it was.

You may recognize a taste of Lewis Carroll in this text, and you would be right. Here is another random string of real text:

```php
<?php echo $faker->realText(180); // you can specify a max number of characters
```

> Knave was standing before them, in chains, with a sigh. 'I only took the opportunity of showing off her head!' the Queen put on his spectacles and looked along the passage into the sky.

Yet you can look in the complete works of Lewis Carroll, you will never find these passages.

## How Does It Work?

The new real text generator uses a very simple algorithm called [Markov chains generator](http://blog.codinghorror.com/markov-and-you/). Here is how it works: 

1. Grab a long text, for instance Lewis Carroll's *Alice's Adventures in Wonderland*. 
2. List, for every word in the text, the words appearing immediately after this word. 

You will end up with a long index looking like the following:

```yaml
...
hours:     ['to', 'a', 'the'],
you:       ['see', 'grant', 'know', 'see', 'must', 'gave'],
everybody: ['minded', 'else', 'executed', 'minding', 'laughed'],
jumping:   ['up', 'merrily', 'about', 'up'],
executed:  ['for', 'on'],
...
```

The next step is easy: choose one key randomly in the index, which will be the first word (for instance: "everybody"). Then, choose a random word among the words following the first word (for instance: "executed"). Use this new word as a key to the index to choose the next word randomly (for instance: 'for'), and repeat until the final text has the desired length.

This will produce some perfectly English-looking text, although not quite grammatically correct. If you need a text with a more natural structure, it's possible to create an index based on two words instead of one:

```yaml
...
'hours to':  ['turn'],
'hours a':   ['day'],
'hours the': ['first'],
...
```

But correctness has a cost: randomness. There are less words following a combination of two words than a single word, so the produced text will be less random.

Faker's Markov chains generator in Faker uses a two-words index. If you want to use a one-word index, override the second parameter of the `realText()` formatter:

```php
<?php 
// generate at most 200 characters with a single-word index
echo $faker->realText(200, 1);
```

> It doesn't mind.' The Gryphon replied to measure herself in a furious passion, Alice indignantly, and the next walking away. She is the earth takes twenty-four hours to get in that it would be.

This great new formatter was [contributed by Tim Düsterhus](https://github.com/fzaninotto/Faker/pull/254). Thanks a lot to him!

## How You Can Contribute

The algorithm needs a large piece of text, for instance a novel, to build a good index. The larger the novel, the better. But too large a novel will slow down the generator execution, as the initial computing required to write the index will take time. Ideally, a novel between 300kB and 700kB if fine. 

Faker already has three locales with a real text generator, based on the following works:

* `en_EN`: *Alice's Adventures in Wonderland*, by Lewis Carroll
* `de_DE`: *Die Leiden des jungen Werther*, by Johann Wolfgang von Goethe
* `fr_FR`: *Madame Bovary*, by Gustave Flaubert

You can contribute a real text generator for other locales by following the implementation of these provider. There are a few constraints, though:

* The novel must be available with a non-commercial license
* You must include the license together with the text
* The novel must be pasted as nowdoc with word wrap to ease code review

[Project Gutenberg](http://www.gutenberg.org/) is a great source of free ebooks in all languages. Look there first for the most famous novel in your language. 

## One Last Word

There is an important thing I would like to say before you leave.

The Queen smiled and passed on. 'Who ARE you talking to?' said one of these cakes,' she thought, 'and hand round the court with a cart-horse, and expecting every moment to think this a very grave voice, 'until all the rats and--oh dear!' cried Alice, with a sigh: 'he taught Laughing and Grief, they used to say.' 'So he did, so he with his head!"' 'How dreadfully savage!' exclaimed Alice. 'That's very curious.' 'It's all his fancy, that: they never executes nobody, you know. But do cats eat bats? Do cats eat bats? Do cats eat bats?' and sometimes, 'Do bats eat cats?' for, you see.
