---
layout: post
title: "Faker 1.3 is Released"
published: true
excerpt: "The latest version of Faker, the fake data generator for PHP, comes with image generators, unique and optional modifiers, color code providers, credit card number generators, and 10 more locales. Most of that thanks to third-party contributors. Generating fake data in PHP cannot be easier."
image: /images/Credit_Cards.jpg
tags:
- faker
- php
---

<img src="/images/Credit_Cards.jpg" class="postImage"/>

Christmas is coming, and [Faker](https://github.com/fzaninotto/Faker) is ready to generate a lot of wonderful presents for you. Version 1.3 was just released, and it will make the task of generating fake data even easier. 39 contributors joined their efforts to add more locales, fix bugs, and some new features that you're going to love.

## New Features

### `unique()` and `optional()` modifiers

Version 1.3 introduces two new special providers: `unique()` and `optional()`, to be called before any other provider. `optional()` can be useful for seeding non-required fields, like a mobile telephone number ; `unique()` is required to populate fields that cannot accept twice the same value, like primary identifiers.

```php
<?php
// unique() forces providers to return unique values
$values = [];
for ($i=0; $i < 10; $i++) {
  // get a random digit, but always a new one, to avoid duplicates
  $values []= $faker->unique()->randomDigit;
}
print_r($values); // [4, 1, 8, 5, 0, 2, 6, 9, 7, 3]

// optional() sometimes bypasses the provider to return null instead
$values = [];
for ($i=0; $i < 10; $i++) {
  // get a random digit, but also null sometimes
  $values []= $faker->optional()->randomDigit;
}
print_r($values); // [1, 4, null, 9, 5, null, null, 4, 6, null]
```

See more details about these two modifiers in the [Readme](https://github.com/fzaninotto/Faker#unique-and-optional-modifiers).

### Fake Images generation

The new `Image` provider was the most requested feature since the release of Faker 1.2 earlier this year. It uses [LoremPixel](http://lorempixel.com/) to generate URLs of fake images, or to download fake images to your filesystem. Path, size, and category (one of abstract, animals, business, cats, city, food, nightlife, fashion, people, nature, sports, technics, and transport) can be customized.

Here is an example:

```php
<img src="<?php echo $faker->imageUrl(300, 200, 'cats') ?>" />
```

![Random cat](http://lorempixel.com/300/200/cats/)

Populating a user database with avatars, or a CMS with actual content thumbnails, is now very easy. See all available options in the [Readme](http://lorempixel.com/200/200/cats/).

### Color provider

Do you need to generate fake color codes? Faker 1.3 provides generators for color codes in all formats:

```php
<?php
echo $faker->hexcolor;        // '#fa3cc2'
echo $faker->rgbcolor;        // '0,255,122'
echo $faker->rgbColorAsArray; // array(0,255,122)
echo $faker->rgbCssColor;     // 'rgb(0,255,122)'
echo $faker->safeColorName;   // 'fuchsia'
echo $faker->colorName;       // 'Gainsbor'
```

### Payment provider

If you use a production database in a staging environment, you have to anonymize payment data. Fortunately, Faker 1.3 comes with specialized payment formatters:

```php
<?php
echo $faker->creditCardType                           // 'MasterCard'
echo $faker->creditCardNumber($type = null)           // '4485480221084675'
echo $faker->creditCardExpirationDate($valid = true)  // DateTime('2014-10-23 13:46:23')
echo $faker->creditCardExpirationDateString($valid = true) // '10/14'
```

Generated credit card numbers are valid, which means that they pass the format checksums. If you know a way to go even further, and generate real credit card numbers for bank accounts with actual money, together with valid expiration dates, please contact me directly, I'm interested ;)

Also, many localized providers have an International Bank Account Number (IBAN) formatter:

```php
<?php
$faker = Faker\Factory::create('fr_FR');
echo $faker->bankAccountNumber // 'FR7570117399503FN7E9T4EDH42'
```

### Formatter Autocomplete for IDEs

Faker uses PHP's magic methods to determine which formatter to use when you call `$faker->name`. This is great for localization and ease of use, but those who use an IDE expect attribute autocompletion. Faker 1.3 solves this by adding IDE insights to the Generator class. Try it: you will generate fake data faster than ever before.

Specialized providers implemented only in certain locales don't benefit from formatter autocomplete, so keep the README at hand when you want to generate new data.

## New Locales

Version 1.3 comes with 11 new locales, all contributed by volunteers. The contribution pace for localization doesn't slow down, it is just amazing. Here are the new locales, in alphabetical order:

* `el_GR` Greek (georgeharito)
* `en_AU` Australian (rcuddy)
* `en_PH` English Philippines (en_PH) (kamote)
* `en_ZA` English (South Africa) (dmfaux)
* `es_PE` Peruvian (cslucano)
* `ja_JP` Japanese (kumamidori)
* `lv_LV` Latvian (pomaxa)
* `ro_MD` Romanian (Moldova) (AlexanderC)
* `ro_RO` Romanian (calina-c)
* `uk_UA` Ukrainian (ruden)
* `zh_CN` Chinese Simplified (tlikai)

Faker is now available in **37 languages**. If yours is missing, please submit a Pull Request to add it!

## Complete Changelog

Faker 1.3 also brings a few bugfixes and minor changes, all contributing to make the library more and more robust. [The complete changelog](https://github.com/fzaninotto/Faker/releases/tag/v1.3.0) is available on GitHub - you may also want to see the [compare view](https://github.com/fzaninotto/Faker/compare/v1.2.0...v1.3.0).

## Upgrading

Faker uses composer, so all you have to do is to change the version requirement in your `composer.json`, as follows:

```json
{
  "require": {
    "fzaninotto/faker": "1.3.*"
  }
}
```

## Thank You All

Now that Faker can generate images, I can't help showing you a few pictures of the party we gave to celebrate the 1.3 release:

![Nightlife 1](http://lorempixel.com/200/200/nightlife/1)
![Nightlife 2](http://lorempixel.com/200/200/nightlife/2)
![Nightlife 3](http://lorempixel.com/200/200/nightlife/3)

![Nightlife 4](http://lorempixel.com/200/200/nightlife/4)
![Nightlife 5](http://lorempixel.com/200/200/nightlife/5)
![Nightlife 6](http://lorempixel.com/200/200/nightlife/6)

Thanks for all the contributions, and happy coding to you all!
