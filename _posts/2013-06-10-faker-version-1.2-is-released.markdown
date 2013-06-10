---
layout: post
title: 'Faker Update: Version 1.2 Is Released'
published: true
excerpt: More than 7 months after the previous release, Faker version 1.2 is now available. Thanks to the work of 35 contributors, this new version provides 12 new locales, new types of random data, and more robustness.
image: /images/fake.jpg
---

<img src="/images/fake.jpg" title="Image © 2010-2013 CloudTimes, source: http://cloudtimes.org/2012/12/30/the-true-business-value-of-big-data/" class="postImage"/>


More than 7 months after the previous release, I have the great pleasure to introduce version 1.2 of [Faker](https://github.com/fzaninotto/Faker), the fake data generator for PHP. Thirty-five contributors from all around the globe collaborated to add 12 new locales, new types of random data, and more robustness thanks to a few bugfixes. As usual, the [Changelog](https://github.com/fzaninotto/Faker/blob/master/CHANGELOG) is in the repository, and if it's not enough, you can still use [the GitHub compare view](https://github.com/fzaninotto/Faker/compare/v1.1.0...v1.2.0).

## Upgrading

Faker uses [composer](https://packagist.org/packages/fzaninotto/faker), so all you have to do is to change the version requirement in your `composer.json`, as follows:

{% gist 3117dabe32e25f319d3a %}

## New locales

Thanks to the wonderful work of the contributors, Faker is now available in [27 languages](https://github.com/fzaninotto/Faker/tree/master/src/Faker/Provider). The new languages available in version 1.2 are, in alphabetical order:

* `da_DK`: Danish
* `en_CA`: Canadian English
* `es_ES`: Spanish
* `fi_FI`: Finnish
* `fr_BE`: Belgian French
* `hy_AM`: Armenian
* `is_IS`: Islandic
* `nl_BE`: Belgian Dutch
* `nl_NL`: Dutch
* `pt_BR`: Brazilian Portuguese
* `tr_TR`: Turkish
* `ua_UA`: Ukrainian

## New providers

```
# Faker\Provider\Base
randomDigitNotNull       // 5
randomNumber($from, $to) // 39049
randomFloat($nbMaxDecimals = NULL, $min = 0, $max = NULL) // 48.8932

# Faker\Provider\Internet
safeEmailDomain          // 'example.org'

# Faker\Provider\Uuid
uuid                     // '7e57d004-2b97-0e7a-b45f-5387367791cd'

# Faker\Provider\File
fileExtension            // 'avi'
mimeType                 // 'video/x-msvideo'

# Faker\Provider\da_DK\Person
cpr                      // '051280-2387'

# Faker\Provider\da_DK\Address
kommune                  // 'Frederiksberg'
region                   // 'Region Sjælland'

# Faker\Provider\da_DK\Company
cvr                      // '32458723'
p                        // '5398237590'
```

## Thank You All

Quite unexpectedly, I just received an email from Hong-Kong listing the names of the 48,145 persons who downloaded Faker. I don't know how the sender got it, but it gives me the opportunity to thank you all. So without further ado, my warm thanks to:

* Chet Walker, Jackelineside
* Wyman Herman, Ansleyfurt
* Violante Palumbo, San Tommaso
* Anselmo Cattaneo, Settimo Giacobbe laziale
* Celia Lebrón, Los Velasco de la Sierra
* Manon Wagner, Hoareau-sur-Gregoire
* Margret Austermühle B.Eng., Feldkirchen
* Tomáš Nguyen, South Pavlaton
* JUDr. Patrik Šimonovič DSc., Skačany
* Eduard Kopecký, West Miloš
* Marko Gadžić, Pančevo
* Maja Zuérius Boxhorn van Miggrode, Andijk
* Juan Pablo Barrera, Puerto Alonso
* Љубинко Докић, Смедерево
* Nahia Villarreal, Villa Murillo
* Евсеев Тарас Савельев, Солнечногорск
* Yasmine Lacroix, Alost (Aalst)
* Dn. Jana De la fuente Segundo, Las Pérez
* Комнен Влачић, Пожаревац
* Esther Miðvík Emmanúelsdóttir, Hafnarfjörður
* Аврам Стевчић, Лесковац
* Bertrand-Pénélope Lamy, Maury
* Божинка Катић, Ваљево
* Irene Pablo Dias, Giovane d'Oeste
* RSDr. Alojz Marián Ph.D., Dražice
* Tyree Jakubowski, New Andreport
* Françoise Da Costa, LemaireBourg
* Tristano Romano, Negri lido
* Julien Navarro-Chauveau, Girard
* Dr doc. Damian Sadowski, South Kacperfurt
* (truncated for brevity)