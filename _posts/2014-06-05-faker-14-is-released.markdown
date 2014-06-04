---
layout: post
title: "Faker 1.4 is Released"
published: true
excerpt: "Faker, the fake data generator for PHP, was just updated to version 1.4. Grab the latest performance improvements, new providers, new locales, and bug fixes by updating right away!"
image: /images/bigdata.jpg
tags:
- faker
- php
---

<img src="/images/bigdata.jpg" class="postImage"/>

Six months after the previous release, here is a better and improved [Faker](https://github.com/fzaninotto/Faker)! 36 different developers contributed to this release, whether to add more locales, fix bugs, or to push new features.

## New Features

### Real Text Generator

I've already blogged about it, and this is the major highlight of Faker 1.4. [Faker now offers a `realTest` formatter](/2014/03/04/faker-generates-real-text.html), based on Markov Chains, to generate "almost understandable" text for your preferred locale.

```php
<?php
$faker = Faker\Factory::create('en_US');
echo $faker->realText(); // generates a random string of 200 characters at most
```

> Alice, as the jury had a little door about fifteen inches high: she tried the effect of lying down with wonder at the stick, and held out its arms folded, frowning like a telescope. And so it was.

### Slug Formatter

Need more than a domain name? Now the `url` formatter includes random slugs. And you can generate unique slugs quite easily by combining the `unique()` modifier together with the new `slug` formatter:

```php
<?php
echo $faker->url;
// 'http://www.skilesdonnelly.biz/aut-accusantium-ut-architecto-sit-et.html'
echo $faker->unique()->slug;
// 'aut-repellat-commodi-vel-itaque-nihil-id-saepe-nostrum'
```

### First Name Gender Methods

The `firstName` formatter is great, but sometimes you want more control - for instance if other fake data for a given person depends on their sex. Now you can generate gender specific first names easily;

```php
<?php
echo $faker->firstNameMale;    // 'Maynard'
echo $faker->firstNameFemale;  // 'Rachel'
```

### More Network Formatters

The Internet provider was completed to offer all the network information you may need to generate.

```php
<?php
echo $faker->ipv4;       // '109.133.32.252'
echo $faker->localIpv4;  // '10.242.58.8'
echo $faker->ipv6;       // '8e65:933d:22ee:a232:f1c1:2741:1f10:117c'
echo $faker->macAddress; // '43:85:B7:08:10:CA'
```

### Local File Provider

The new `file` formatter copies a random file from a given directory to the target directory, and returns the fullpath or filename. That's a great way to create random attachements to your fixtures.

```php
<?php
echo $faker->file($sourceDir = '/tmp', $targetDir = '/tmp');
// '/path/to/targetDir/13b73edae8443990be1aa8f1a483bc27.jpg'
echo $faker->file($sourceDir, $targetDir, false);
// '13b73edae8443990be1aa8f1a483bc27.jpg'
```

### EAN Barcode Provider

Need to generate a barcode? Faker's got you covered.

```php
<?php
echo $faker->ean13; // '4006381333931'
echo $faker->ean8;  // '73513537'
```

## New Locales

4 new locales appear in this release. That makes a total of **42 locales** covered by Faker! If yours is missing, please [submit a pull request](https://github.com/fzaninotto/Faker/blob/master/CONTRIBUTING.md).

* `bn_BD` Bengali (masnun)
* `fr_CA` French Canadian (marcaube)
* `hu_HU` Hungarian (sagikazarmark)
* `me_ME` Montenegrian (ognjenm)

In addition, existing locales were developped, harmonized, and tested. 

And of course, there are all the locale specific formatters (see [the Readme](https://github.com/fzaninotto/Faker#language-specific-formatters)) for more details.

* `cs_CZ\Address` (`region`)
* `cs_CZ\Company` (`ico`)
* `cs_CZ\DateTime` (`monthNameGenitive`, `formattedDate`)
* `da_DK\Person` (`cpr`)
* `da_DK\Address` (`kommune`, `region`)
* `da_DK\Company` (`cvr`, `p`)
* `fr_FR\Company` (`siren`, `siret`)
* `fr_FR\Address` (`departmentName`, `departmentNumber`, `department`, `region`)
* `ja_JP\Person` (`kanaName`, `firstKanaName`, `lastKanaName`)
* `pl_PL\Person` (`pesel`, `personalIdentityNumber`, `taxpayerIdentificationNumber`)
* `pl_PL\Company` (`regon`, `regonLocal`)
* `pl_PL\Payment` (`bank`, `bankAccountNumber`)
* `pt_PT\Person` (`taxpayerIdentificationNumber`)
* `ro_RO\Person` (`cnp`)
* `ro_RO\PhoneNumber` (`tollFreePhoneNumber`, `premiumRatePhoneNumber`)

## Complete Changelog

Faker 1.4 also brings a few performance improvements, bugfixes and minor changes. [The complete changelog](https://github.com/fzaninotto/Faker/releases/tag/v1.4.0) is available on GitHub - you may also want to see the [compare view](https://github.com/fzaninotto/Faker/compare/v1.3.0...v1.4.0).

## Upgrading

Faker uses composer, so all you have to do is to change the version requirement in your `composer.json`, as follows:

```json
{
  "require": {
    "fzaninotto/faker": "1.4.*"
  }
}
```

## Thank You All

I wanted to tell you how deeply fond of the Faker community I am. So many contributors with such great ideas give their time to enhance and extend the Fake data generator for PHP. 

So I decided to write a poem for all Faker developers. Faker users can feel concerned, too!

> English, who wanted leaders,

> And had been of late much accustomed

> Ao usurpation and conquest. Edwin and Morcar,

> The earls of Mercia and Northumbria --

> "' 'Ugh!' said the Gryphon, and,

> taking Alice by the whole pack of cards:

> The Knave 'Turn them over!' 

> The Knave shook his head sadly.

> 'Do I look like it?' he said.

> (Which he certainly did NOT, being made entirely of cardboard.)

> 'All right, so far,' said the Gryphon,

> And, taking Alice by the soldiers, 

> Who of course you know why it's called a.
