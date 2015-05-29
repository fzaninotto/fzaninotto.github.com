---
layout: post
title: "Faker 1.5 is Released"
published: true
excerpt: "After almost one year of work by more than 70 contributors, Faker, the fake data generator for PHP, is released in version 1.5. With more than 100 changes, Faker is now richer, faster, and more polyglot than ever. Read on to see what's new."
image: /images/crowd_small.png
tags:
- faker
- php
---

Yep, it's here. Almost a year after the previous release, Faker 1.5 has been released, with a ton and a half of new fake data, ridiculously useful new formatters, new locales, and bug fixes. Ready to dive in?

<a href="https://www.flickr.com/photos/29106784@N02/3767180666" title="Festival Crowd by Shane Kelly (ballinascreen.com), sur Flickr"><img src="/images/crowd.jpg" style="width:100%" alt="Festival Crowd"/></a>

## New Formatters

Faker 1.5 includes a bunch of new formatters, to help you generate even more data types:

```php
$faker->shuffle('hello, world') // 'rlo,h eoldlw'
$faker->shuffle(array(1, 2, 3)) // array(2, 1, 3)
$faker->asciify('Hello ***')    // 'Hello R6+'
$faker->regexify('[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}') // sm0@y8k96a.ej
$faker->password                // 'k&|X+a45*2['
$faker->swiftBicNumber          // RZTIAT22263
$faker->isbn13                  // '9790404436093'
$faker->isbn10                  // '4881416324'
$faker->currencyCode            // EUR
$faker->biasedNumberBetween($min = 10, $max = 20, $function = 'sqrt') // 12
$faker->imageUrl($width, $height, 'cats', true, 'Faker') // 'http://lorempixel.com/800/400/cats/Faker', the url of a cat image with the word "Faker" in it
```

Let me focus on just three of them: `shuffle`, `regexigy`, and `biasedNumberBetween`.

`shuffle` already exists in PHP. The problem is that the native `shuffle()` function doesn't rely on the same randomizer as Faker. Faker's randomizer, powered by `mt_rand()`, uses the Mersenne Twister algorithm to provide more random, and seedable data. Faker's `shuffle` uses Faker's randomizer, together with the [Fisher-Yates algorithm](http://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle), and works both on strings and arrays. It's just a million times better than the native version.

```php
// try that, and you'll get exactly the same random data
$faker = Faker\Factory::create();
$faker->seed(5);
for ($i=0; $i < 10; $i++) {
  $faker->shuffle('hello, world');
}
// le ldrhwolo,
// lr,h oldeolw
// wllod lo,hre
// dh owo,rllel
// drleo wlh,lo
//  dewolrll,oh
// wl edoollh,r
// lowd, lhrelo
//  rolwd,lloeh
// ohole,dlwl r
```

`regexigy` takes a regular expression as parameter, and returns a random string satisfying this regular expression. If the "string with wildcard" formatters (`numerify('Hello ###')`, `lexify('Hello ???')`, `bothify('Hello ##??')`, `asciify('Hello ***')`) aren't enough for you, you can always use this powerful formatter.

```php
$faker->regexify('\w')       // k
$faker->regexify('(a|b)')    // b
$faker->regexify('[aeiou]')  // o
$faker->regexify('[a-z]')    // p
$faker->regexify('[a-z1-9]') // w
$faker->regexify('a*b+c?')   // abc
$faker->regexify('a{2}')     // aa
$faker->regexify('a{2,3}')   // aa
$faker->regexify('[aeiou]{2,3}') // ui
$faker->regexify('[a-z]{2,3}') // rw
$faker->regexify('(a|b){2,3}') // abb
$faker->regexify('\.\*\?\+') // .*?+
$faker->regexify('[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}') // a8%1-_@zvk.sgha
```

`regexify` supports a subset of the RegExp syntax, usually enough to match your needs. But Unicode, negated classes, unbounded ranges, subpatterns, back references, assertions, recursive patterns, and comments are not supported. Escaping support is extremely fragile.

This formatter is also VERY slow. Use it only when no other formatter can generate the fake data you want. For instance, prefer calling `$faker->email` rather than `regexify` with the previous regular expression.

Also note than `bothify` can probably do most of what `regexify` does, but much faster. For instance, for a dummy email generation, try `$faker->bothify('?????????@???.???')`.

`biasedNumberBetween($min, $max, $function)` returns a random number between two boundaries, but with a non-uniform chance. You can pass a distribution function to have more chances to get a number close to the start, to the end, or to the middle.

The algorithm creates two doubles, x ∈ [0, 1], y ∈ [0, 1) and checks whether the return value of `$function` for x is greater than or equal to y. If this is the case the number is accepted and x is mapped to the appropriate integer between `$min` and `$max`. Otherwise two new doubles are created until the pair is accepted.

```php
$faker->biasedNumberBetween(1, 10, ['\Faker\Provider\Biased', 'unbiased']) // 5
$faker->biasedNumberBetween(1, 10, ['\Faker\Provider\Biased', 'linearLow']) // 3
$faker->biasedNumberBetween(1, 10, ['\Faker\Provider\Biased', 'linearHigh']) // 7
```

`$function` can be any callable. The limit is your imagination!

## New Locales

People from all around the world use Faker. Version 1.5 comes with close to 60 locales, including 17 new ones:

* Arabic (`ar_JO`)
* Austrian (`at_AT`)
* Belgium (`be_BE`)
* English for New Zealand (`en_NZ`)
* Uganda (`en_UG`)
* Spanish for Venezuela (`es_VE`)
* Persian (`fa_IR`)
* Indonesian (`id_ID`)
* Georgian (`ka_GE`)
* Kazakh (`kk_KZ`)
* Korean (`ko_KR`)
* Nepali (`ne_NP`)
* Norwegian (`no_NO`)
* Slovenian (`sl_SI`)
* Swedish (`sv_SE`)
* Vietnamese (`vi_VN`)
* Traditional Chinese (`zh_TW`)

## Third-Party Libraries and Formatters Based on Faker

I love when people create new formatters, but Faker's destiny isn't to host them all. The core Faker repository should provide the providers and formatters required for most usages, but not all. Now, if you create a particularly smart Faker provider for a rare use case, send me a pull request and I'll mention it [in the README](https://github.com/fzaninotto/Faker#third-party-libraries-extendingbased-on-faker). Here is a list of tools and formatters that you can already use:

* [BazingaFakerBundle](https://github.com/willdurand/BazingaFakerBundle): Put the awesome Faker library into the Symfony2 DIC and populate your database with fake data.
* [FakerServiceProvider](https://github.com/EmanueleMinotto/FakerServiceProvider): Faker Service Provider for Silex
* [faker-cli](https://github.com/bit3/faker-cli): Command Line Tool for the Faker PHP library
* [AliceFixturesBundle](https://github.com/h4cc/AliceFixturesBundle): A Symfony2 bundle for using Alice and Faker with data fixtures. Abled to use Doctrine ORM as well as Doctrine MongoDB ODM.
* [Factory Muffin](https://github.com/thephpleague/factory-muffin): enable the rapid creation of objects (PHP port of factory-girl)
* [CompanyNameGenerator](https://github.com/fzaninotto/CompanyNameGenerator): Generate names for English tech companies with class
* [datalea](https://github.com/spyrit/datalea) A highly customizable random test data generator web app
* [newage-ipsum](https://github.com/frequenc1/newage-ipsum): A new aged ipsum provider for the faker library inspired by http://sebpearce.com/bullshit/
* [xml-faker](https://github.com/prewk/xml-faker): Create fake XML with Faker
* [faker-context](https://github.com/denheck/faker-context): Behat context using Faker to generate testdata
* [CronExpressionGenerator](https://github.com/swekaj/CronExpressionGenerator): Faker provider for generating random, valid cron expressions.

## And More

Between Faker 1.4 and 1.5, more than 100 pull requests were merged. They're all listed in [the CHANGELOG file](https://github.com/fzaninotto/Faker/blob/master/CHANGELOG.md). Suffice to say that they make Faker more stable, faster, and easier to use. For instance, your IDE will know how to suggest more formatters, you will be able to seed the generator properly, you will get more up to date user agents, color names in Dutch, or get valid fake emails whatever the locale.

Faker 1.5 works on PHP 5.3.3 through PHP 7.0. Update your local installation using `composer`, there is no BC break.

## Thank You Thank You Thank You Thank You Thank You Thank You Thank You All

I didn't generate the section title with Faker. I didn't use copy/paste either. I typed it all. That's how much I want to thank the 70+ contributors who fixed bugs, sent pull requests, reviewed code, commented, helped newcomers, etc. These people simply made Faker better. They deserve to be mentioned here. Please give a huge round of applause to the Faker 1.5 crowd:

* [aivus](http://github.com/aivus)
* [ajbdev](http://github.com/ajbdev)
* [alesf](http://github.com/alesf)
* [AlexCutts](http://github.com/AlexCutts)
* [ankitpokhrel](http://github.com/ankitpokhrel)
* [asika32764](http://github.com/asika32764)
* [behramcelen](http://github.com/behramcelen)
* [belendel](http://github.com/belendel)
* [bessl](http://github.com/bessl)
* [byan](http://github.com/byan)
* [daveblake](http://github.com/daveblake)
* [deerawan](http://github.com/deerawan)
* [denheck](http://github.com/denheck)
* [DIOHz0r](http://github.com/DIOHz0r)
* [endelwar](http://github.com/endelwar)
* [fonsecas72](http://github.com/fonsecas72)
* [fzaninotto](http://github.com/fzaninotto)
* [gido](http://github.com/gido)
* [gietos](http://github.com/gietos)
* [glagola](http://github.com/glagola)
* [GrahamCampbell](http://github.com/GrahamCampbell)
* [halaxa](http://github.com/halaxa)
* [huy95](http://github.com/huy95)
* [igorsantos07](http://github.com/igorsantos07)
* [ihsanudin](http://github.com/ihsanudin)
* [ikwattro](http://github.com/ikwattro)
* [ivanmirson](http://github.com/ivanmirson)
* [jadb](http://github.com/jadb)
* [JasonMortonNZ](http://github.com/JasonMortonNZ)
* [JeroenDeDauw](http://github.com/JeroenDeDauw)
* [JonathanKryza](http://github.com/JonathanKryza)
* [julien](http://github.com/julien)
* [killerog](http://github.com/killerog)
* [kix](http://github.com/kix)
* [kletellier](http://github.com/kletellier)
* [kumamidori](http://github.com/kumamidori)
* [lintaba](http://github.com/lintaba)
* [Lisso](http://github.com/Lisso)
* [lperto](http://github.com/lperto)
* [MatissJanis](http://github.com/MatissJanis)
* [miclf](http://github.com/miclf)
* [mikehaertl](http://github.com/mikehaertl)
* [nazar](http://github.com/nazar)
* [netcarver](http://github.com/netcarver)
* [pauledenburg](http://github.com/pauledenburg)
* [paulvalla](http://github.com/paulvalla)
* [pearlc](http://github.com/pearlc)
* [phaza](http://github.com/phaza)
* [philsturgeon](http://github.com/philsturgeon)
* [piotrantosik](http://github.com/piotrantosik)
* [Ragazzo](http://github.com/Ragazzo)
* [ronanguilloux](http://github.com/ronanguilloux)
* [schmengler](http://github.com/schmengler)
* [semanser](http://github.com/semanser)
* [SpaceK33z](http://github.com/SpaceK33z)
* [stelgenhof](http://github.com/stelgenhof)
* [stof](http://github.com/stof)
* [stoutZero](http://github.com/stoutZero)
* [svrnm](http://github.com/svrnm)
* [swekaj](http://github.com/swekaj)
* [terion](http://github.com/terion)
* [tharoldD](http://github.com/tharoldD)
* [TimWolla](http://github.com/TimWolla)
* [TomasVotruba](http://github.com/TomasVotruba)
* [TomK](http://github.com/TomK)
* [totophe](http://github.com/totophe)
* [tzhuan](http://github.com/tzhuan)
* [ulrikjohansson](http://github.com/ulrikjohansson)
* [wizardjedi](http://github.com/wizardjedi)
* [YerlenZhubangaliyev](http://github.com/YerlenZhubangaliyev)
* [ysramirez](http://github.com/ysramirez)
* [ZAYEC77](http://github.com/ZAYEC77)
* [zoli](http://github.com/zoli)
* [zrashwani](http://github.com/zrashwani)

## A Final (Pass)Word

I recently received a file containing over 10,000,000 stolen passwords, leaked from a famous gaming network. Please check on the following list if your own password hasn't been compromised:

* fx'W+XB"V=
* [aYIf~
* 5>i6M[!]
* zzu"O`9"=$>_7@P+J\8=
* yJ7H/}w059N=)4QR
* i0K\3IL)gN`H=|In$k
* oUb:OK>u}/XK[LQ
* uZ3~]OB6I`hfDohm'0|
* _IZGRz7vCGdD$9*zKv/
* v2wgLZu}HN4o>?>K-
* '=cvDQ/
* X>4/9A~=?#rGIdWG|1,"
* Qf}6k|$<QN
* bI=mYH'b94qn8.
* B.{q&xjE=A
* password
* %(^o1j4/
* `k(O$XufMs
* Gmb\6b
* <H;F3^;lvp-IaXq.}F[
* Sjkuv-
* QEf_11//;&y
* @4llOmdrd*Q9fknMJZU
* CEp`N9k6;')(hF((.GS
* 1Sfsg6
* COq/T9\C(&4L?Y8bAO
* ta{G44uJ1JHX
* q,<:9f{+nP
* GgOjX6{uMK$&1a+6O)
* PAR8kW#>_s`!
* 0@[w:RTD~8pHf
* ,w"w{&}3f?0/adL[

Happy faking!
