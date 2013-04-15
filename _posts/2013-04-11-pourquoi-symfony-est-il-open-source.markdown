---
layout: post
title: Pourquoi Symfony est-il (encore) open-source ?
published: true
excerpt: "<i>English speakers: This post is based on the <a href='http://paris2013.live.symfony.com/speakers'>keynote speech I gave</a> during the Symfony Live Paris 2013 conference. It's in French, and too long to be translated. But people from the audience asked me to publish it. Don't be afraid though: this blog is still mostly in English.</i> Symfony paye une partie de votre salaire, et c'est pourtant le résultat d'un don. Mais pas forcément d'un don désintéressé. Après de petits détours philosophiques, sociologiques et économiques, nous verrons si l'Open-Source en général - et Symfony en particulier - sont l'aboutissement du rêve de doux dingues, ou l'amorce d'une nouvelle ère."
image: /images/symfony_black_03.png
---

<blockquote><i>Ce texte, un peu remanié, est issu d'une conférence d'environ 40 minutes que j'ai donnée lors du Symfony Live 2013. Sa longueur et son style en font un ovni sur ce blog - même si la thématique de la motivation de l'open-source a <a href="/2011/11/13/open-source-is-a-gift.html">déjà</a> <a href="/2012/09/12/open-source-relies-on-selfishness.html">été</a> abordée ici.</i></blockquote>

<img src="/images/symfony_black_03.png" title="Official Symfony Logo" class="postImage"/>

J'ai la chance d'être l'une des 2 seules personnes ayant (virtuellement) un [badge](https://connect.sensiolabs.com/profile/fzaninotto) "8 ans de symfony", mais je n'ai aucun mérite. C'est que Symfony m'est tombé dessus, un beau jour d'avril 2005. Je travaillais à l'époque pour Sensio. Fabien Potencier est venu me voir et m'a dit abruptement : "J'ai fait un framework. On va l'open-sourcer." Je m'aperçois que je viens de répondre à la question posée en tête de ce billet. Pourquoi Symfony est-il open-source ? Parce que Fabien en a décidé ainsi. L'exercice pourrait donc s'arrêter là, ce serait bien dommage, parce que je n'ai pas souvent l'occasion de partager ce genre de considérations. Aussi, tant que j'ai des lecteurs, permettez-moi d'étendre le sujet à une question plus intéressante.

Introduction
------------

On pourrait reformuler le sujet ainsi : "L'Open-Source, pour quoi faire ?" ou plutôt: "Pourquoi **faire** l'Open-Source ?". Faire est un verbe un peu ambigu. En fait, on peut se poser deux questions : pourquoi **utiliser** de l'open-source, et pourquoi **produire** de l'open-source ?

### L'utilisation de l'open-source : hors sujet

Répondons rapidement à la première question. Pourquoi **utiliser** l'Open-Source ? Parce que nous sommes de **vieux rachots**. Nous préférons obtenir quelque chose gratuitement plutôt que de payer pour, ce qui nous amène à utiliser Bittorrent plutôt que les services de téléchargement légal. Vous vous doutez bien que derrière, ça fait moins d'argent pour la production de films, et qu'à long terme ça risque d'appauvrir la création. On peut s'inventer des excuses, du genre: "Ça fait des décennies que l'industrie du cinéma / du disque / du jeu vidéo se fait de l'argent sur mon dos, c'est un juste retour des choses". Piètre excuse en fait, qui n'est que la légitimation d'une lâcheté, et qu'il est difficile d'ériger en vertu. Nous utilisons de l'Open-Source donc, non par conviction, mais par faiblesse.

Il y a des cas où l'open-source est plus facile à utiliser qu'un logiciel propriétaire - toute considération de prix mise à part. Quoique "facile" n'aie pas forcément le même sens pour tout le monde. Si lire une doc mal écrite, en anglais, qui vous force à installer papa maman pour tester un "hello world", et qui vous laisse dans la panade dès que vous tentez quelque chose d'un tant soit peu complexe, si faire tout ça vous parait "facile", c'est que rien n'est vraiment difficile pour vous. Mais je garderai quand même cet argument de la facilité, pourquoi pas.

Je conviens également qu'on peut parfois venir à l'Open-Source par **idéologie**. Certains ne **veulent pas** utiliser de logiciels propriétaires, parce qu'ils associent cela à un Grand Mal. Oracle, Microsoft, Dassault Systèmes font de l'argent avec du logiciel propriétaire, c'est extrêmement vulgaire de faire de l'argent. Je grossis le trait bien sûr. Et surtout, "ils nous enferment" dans leurs systèmes propriétaires, ce qui est une inquiétude assez récente, convenez-en. Car ça ne vous inquiète pas d'être meublé avec une étagère Billy pas open-source, mais ça vous fait très mal de ranger vos CD virtuels dans Windows Media Player. Je considère pour ma part que le boycott de logiciels propriétaires par conviction est une erreur, car si personne ne peut gagner de l'argent avec le logiciel, personne ici ne pourra gagner sa vie.

On peut aussi voir un danger dans l'omniprésence de l'informatique de nos jours. Et si le logiciel est partout autour de nous (il décode nos communications téléphoniques, il transmet le signal à notre pédale de frein, il comptabilise notre bulletin de vote), si donc le logiciel nous contrôle, il devient urgent de contrôler le logiciel. Là encore, je me mets en retrait de cette paranoïa, au risque de me faire des ennemis. Car je crois que le totalitarisme, s'il advient dans nos sociétés, ne viendra pas du logiciel, mais de notre indifférence à la douleur des autres.

Bref. Nous utilisons donc l'Open-Source parce que nous sommes soit des flemmards désargentés, soit des idéalistes à courte vue, c'est à dire des naïfs, soit des paranoïaques. Ce n'est pas très glorieux, mais ça me permet de me concentrer sur une partie de la question plus intéressante.

### La production de l'open-source : une vraie question

On peut donc se concentrer sur la seconde question, "Pourquoi **produire** de l'Open-Source ?". Et quand on connaît des contributeurs passionnés de bibliothèques ou de logiciels Open-Source, quand on sait tout le temps qu'ils y consacrent, la question se pose effectivement. Sacrifier ses loisirs, écrire du code dès qu'on a du temps libre, répondre continuellement à des questions d'utilisateurs sur des mailing-listes, c'est un sacré **investissement**.

Et en "open-sourçant" une librairie, on prend le risque qu'elle soit utilisée par d'autres, et même qu'elle soit utilisée **contre notre propre intérêt**. Prenez Symfony, qui est un très bon exemple. Les spectateurs du Symfony Live profitent tous de l'investissement de Fabien Potencier et de SensioLabs dans leurs travaux de tous les jours. Et ils vendent souvent, en interne ou en externe, leur expertise Symfony. Or, c'est une des activités de SensioLabs, un de ses moteurs économiques, que de vendre de l'expertise Symfony. Autrement dit, les participants du Symfony Live sont tous concurrents de SensioLabs. Et pourtant cette société continue de les inviter à partager son expérience et d'investir dans Symfony. Cette attitude incompréhensible doit pourtant bien avoir une justification logique - à moins que Fabien Potencier ne soit complètement marteau, ce qui est une hypothèse que je ne souhaite pas écarter totalement pour l'instant.

Pourquoi produire de l'open-source alors que ça nous coûte, quelles motivations se cachent derrière cet acte en apparence paradoxal, c'est la question à laquelle je me propose de répondre dans ce billet. Et nous verrons que pour résoudre cette apparente contradiction, il me faudra faire appel à la sociologie, à l'anthropologie, à la philosophie, et à l'économie. C'est que derrière une interrogation en apparence bénigne se cache peut-être une mutation profonde de notre société - mais n'allons pas trop vite.

Désintéressement individuel
---------------------------

"Pourquoi produire de l'Open-Source", disais-je, est une question vaste et difficile, et je vous propose de la réduire petit à petit à quelque chose de plus facile à résoudre. D'abord en enlevant, à nouveau, des cas particuliers.

### Les projets pas intéressants

Je pense aux projets **sans intérêt**, qui représentent, soyons francs, l'immense majorité de la production open-source de nos jours. Je classe ces projets en deux catégories.

D'abord, il y a les projets **Emmaüs**. Une librairie qu'on a utilisée pendant un certain temps, qu'on a usée jusqu'à la corde et qui n'a plus pour nous de grande valeur, comme cette vieille veste mille fois rapiécée, avec des ovales de cuir sur les coudes et une odeur persistante d'anti-mite. On la donne, cette vieille veste, parce qu'on ne veut pas la jeter, parce qu'on y est trop attaché. On se dit qu'elle peut profiter à quelqu'un d'autre, mais la vérité est qu'on la donne pour ne pas la savoir entièrement disparue. On la donne par lâcheté enfin, car une fois qu'on l'aura déposée chez Emmaüs, on se fiche comme de sa dernière chaussette de l'usage qui en sera fait. Sur GitHub, qui est une autre forme d'Emmaüs, ça donne des librairies à 1 commit, à 1 étoile, et à zéro utilisateurs.

La seconde catégorie de projets non intéressants est ce que j'appelle les **projets d'orgueil**. Prenez Sacha, 25 ans, développeur de son état. Il est tellement fier de son implémentation du tri à bulles en PHP qu'il veut que d'autres partagent sa fierté. C'est comme un peintre du dimanche qui, après avoir exposé au Grand Marché de l'Art Contemporain à Bastille, sans avoir rien pu vendre d'ailleurs, offre ses toiles à un musée, pour la **postérité**.

Comme ce peintre, Sacha le développeur publie son implémentation du tri à bulles en PHP en espérant **laisser une trace** dans l'histoire. Il le fait avec une intention d'artiste, à sens unique, qui n'accepte pas la critique. Son ego considère chaque demande de modification comme une insulte. Après tout, cette librairie est un produit fini, que dis-je un produit, une œuvre. Sa librairie ne saurait tolérer aucune retouche maintenant que la signature est apposée dans le README. Et sur GitHub, qui est une autre forme de Grand Marché de l'Art Contemporain, ça donne des librairies à 1 commit, et à 150 issues jamais fermées - et donc forcément non utilisables.

Si l'on écarte les librairies sans intérêt, ce qui correspond à la partie immergée de l'iceberg, il nous reste la partie émergée - celle qui nous intéresse.

### Les projets pas intéressés

On peut donc reformuler la question en "Pourquoi produire de l'Open-Source pour que les autres l'utilisent". Pourquoi donc, produire du code de valeur, et l'offrir à d'autres pour qu'ils puissent le réutiliser et le faire fructifier ? Pourquoi contribuer à un patrimoine commun ?

Cela ressemble à première vue à un **don**. Vous savez, cette pièce que vous donnez à un violoniste approximatif et roumain dans une rame de métro bondée. Vous ne lui donnez pas la pièce pour qu'il arrête de jouer - il vient vous voir lorsqu'il a déjà fini. Vous lui donnez **parce qu'il vous le demande**, parce que vous considérez qu'il est de votre **devoir** de répondre à cette demande, sans contrepartie. Ce type de don procède de la **pure générosité**, qui selon Descartes ne nous amène rien d'autre que de l'estime de soi.

Autant vous le dire tout de suite, je pense qu'il n'existe pas de tel don dans le monde du logiciel open-source "intéressant".

En effet, celui qui donne du code sans être intéressé à son usage par d'autres n'est pas très différent de celui qui donnait son code à Emmaüs. L'issue est souvent la même : du code mort, non entretenu, car si vous donnez sans vous soucier de ce qu'on fera de votre don, vous ignorez également tout retour d'utilisation de ce don. Autrement dit, en écartant tout à l'heure les projets sans intérêt, nous avons également écartés les projets désintéressés, jetant ainsi le bébé de la générosité avec l'eau du bain. Ce qui n'est pas si grave, puisque ces projets-là, encore une fois, personne ne les utilise.

Nous avons donc écarté sans état d'âme la plupart des logiciels open-source, qui sont produits par des individus qui ne se soucient pas de leur utilisation. C'est que l'open-source est un système d'échange. On ne peut pas l'envisager uniquement sous le point de vue de l'individu. Pour partager un logiciel open-source, il faut au moins être deux.

Donner pour recevoir
--------------------

Car le don de l'open-source n'est pas sans contrepartie. Nous ne sommes pas au pays des bisounours. Pour vous dire la vérité, je suis convaincu que derrière une apparente générosité, se cache souvent une attitude beaucoup plus **intéressée**. Ce qui n'exclue pas le don, notez-le bien.

### Don et contre-don

D'ailleurs, selon Marcel Mauss, qui était sociologue, **tous les dons** sont intéressés. Autrement dit, même sans le savoir, on attend toujours quelque chose en retour d'un don. C'est que la personne à qui on donne n'est pas passive. On utilise d'ailleur un verbe d'action pour décrire son attitude : recevoir. Et la réception du don implique une forme de réciprocité, que Mauss appelle "contre-don", et qu'il a théorisé dans les années 1920. Cette réciprocité n'est pas forcément matérielle. D'ailleurs, le plus souvent, le contre-don, le produit du don, est **un nouveau lien social**.

Mauss, qui était aussi anthropologue, a beaucoup observé les sociétés dites primitives. Il décrit quantité de scènes de don qui suivent des codes sociaux souvent très stricts. Exemple : Maurice (j'ai changé les noms, mais vous allez reconnaitre la situation), Maurice donc rend visite à Gérard dans sa hutte. Maurice apporte avec lui une tête de bouc qu'il trouve très décorative. Il l'offre à Gérard, qui l'accroche sur le mur, entre les chiures de chauve-souris et une scène de chasse peinte au pochoir. Le don de Maurice, sans qu'il se l'avoue forcément, est intéressé : **créer un lien** entre lui et Gérard. Car cette tête de bouc, c'est en quelque sorte une partie de lui-même. En l'accrochant au mur, Gérard se souviendra de lui. Maurice profite d'ailleurs de sa visite pour parler d'une fuite de boue dans sa caverne. Gérard se sent obligé de lui proposer de l'aider à la réparer. Et ils finissent l'après-midi en bricolant bras dessus-bras dessous. Dans cette histoire, le don sert quasiment de **contrat** qui lie deux êtres l'un à l'autre.

Cette contrepartie, ce **contre-don**, c'est une des **motivations** de l'Open-Source : créer du lien avec une communauté de développeurs.

Ça passe notamment par des échanges entre individus : je te corrige un bug, tu m'écris un peu de doc, on s'est ainsi créé une dette réciproque. On le voit aussi en creux. Souvenez-vous : vous avez trouvé une librairie qui faisait presque tout ce que vous voulez. Mais plutôt que de l'utiliser, vous avez choisi de la **redévelopper**, pour être maître des choix techniques. C'est autre manière d'éviter d'être redevable à l'auteur de la librairie initiale.

Le contre-don passe aussi par des échanges **entre groupes**. Dans le cas de l'Open-source, ces échanges sont encore assez compétitifs. Le grand Manitou de Symfony rencontre le grand Mammamouchi de Drupal, chacun est accompagné de sa tribu, ça se passe probablement lors d'une table ronde dans une grande conférence. Pour créer du lien, le grand Manitou de Symfony se croit obligé de dire que l'interface d'administration de Drupal est "canon", et il accompagne ce compliment d'un badge "SensioLabs UI Expert". Le compliment est une autre forme de don, qui honore celui qui le donne au moins autant que celui qui le reçoit. En retour, le grand Mammamouchi de Drupal se croit obligé de dire que le composant de sécurité de Symfony est "extrêmement bien fichu", ce qui est au mieux, un pieux mensonge.

Mais revenons-en au lien social que crée le don.

Nos communautés open-source nous permettent, très simplement, de nous **connaitre**. Dans un monde de plus en plus déshumanisé, c'est un moyen comme un autre de trouver des gens avec qui on a des points communs. C'est un peu comme les clubs Tupperware de nos mamans. Une fois le lien créé, une fois la dette contractée, on pourra toujours l'actionner en temps voulu. C'est tellement vrai que GitHub, qui est à la base un outil de travail, est devenu un **réseau social** de développeurs. J'insiste sur le mot **social**. Sur GitHub, on discute, on se rencontre, on rigole, bref, on se fait des relations. C'est pas très différent de Facebook quand on y pense. Ou même de Meetic. Mais je m'égare.

### Générosité et solidarité

Le don dans l'open-source est très rarement désintéressé donc, mais on n'y gagne pas que des amis. On y gagne aussi à se décharger de son propre travail, car on bénéficie de l'apport, du support de la communauté. En open-sourçant une librairie, je m'attends à ce que des inconnus me remontent des rapports de bugs. Il peut arriver que des inconnus me soumettent des patchs pour corriger ces bugs, testent des cas limites. Bref, je m'attends à pouvoir consolider ma librairie **à moindre coût**. Ça veut dire que le don de code, loin d'être fondé sur une **vertu** qui est la générosité, est souvent fondé sur un **vice**, qui est l'égoïsme. Je ne donne pas pour l'intérêt des autres, je donne pour mon propre intérêt.

Cette forme de don intéressé porte un nom bien précis : c'est la **solidarité**. Ainsi, je choisis de prendre une assurance auto, non pas pour que ma prime permette de réparer les voitures des **autres adhérents**, mais pour que les primes des autres adhérents payent les réparations de **ma voiture** lorsque j'aurai un accident. L'assurance, comme le syndicalisme et l'open-source, sont des chaînes de solidarité, qui mettent en commun des égoïsmes pour le bien du groupe. Notez que la solidarité est plus efficace que la générosité, tout simplement parce que l'égoïsme est bien plus répandu que l'altruisme.

Donc je contribue à l'open-source parce que j'en profite aussi. Au passage, on s'aperçoit que ce qui motive la **production** de l'Open-Source rejoint ce qui en motive **l'utilisation**. Souvenez-vous du début de mon exposé. Égoïsme, flemmardise, naïveté. Le système de l'Open-Source a le don de s'appuyer sur ces travers individuels pour créer une vertu collective. Avouez que c'est déjà un petit miracle.

Mon discours peut faire croire que l'open-source devient condamnable, parce que basée sur la solidarité qui est **moralement inférieure** à la générosité pure. Je souhaite corriger ce malentendu. Car à mon sens, la morale n'a rien à voir là-dedans. Les philosophes nous enseignent que la morale, c'est ce qui nous pousse à faire des choses que nous ne sommes pas obligés de faire, mais que nous aimerions que tout le monde fasse. Or nul n'est besoin de morale pour s'aider l'un l'autre en passant par la solidarité. Autrement dit : l'open-source sait créer du bien commun, sans que la morale soit impliquée une seule seconde. Rien ne vous interdit d'en avoir - c'est d'ailleurs mieux, à mon avis. Mais ce n'est pas **nécessaire**.

### Mais qui donne au juste ?

Je vous propose une dernière justification du fait que l'open-source ne soit pas un don de pure générosité. C'est qu'on ne peut donner que ce que l'on **possède**. Or, dans la plupart des cas, les développeurs n'ont pas la **propriété** du code qu'ils écrivent. Cette propriété, ils l'ont cédée par contrat à leur employeur, ou à leur client. Ce n'est donc pas le **développeur** qui choisit d'open-sourcer une librairie, mais le Directeur Technique ou le Directeur Informatique. Car c'est lui qui **possède** le logiciel et qui peut choisir d'en abandonner les droits de propriété à la communauté open-source. Et quand je parle de Directeur Technique, je parle d'une personne **morale** plus que d'une personne **physique**. Il (ou elle) représente ainsi sa société, et les intérêts de sa société. Et une société n'a aucun intérêt à être généreuse et à donner sans retour, car le but premier d'une société est de faire du **profit**.

Ça vous choque peut-être mais ce n'est pas grave, car ce système, qu'on appelle le capitalisme, fait tourner le monde tel que nous le connaissons, produisant au passage une quantité de richesse faramineuse. Le capitalisme élève au global le niveau de vie des habitants de la planète - même si c'est au prix d'un accroissement des inégalités.

C'est pourquoi les entreprises "sponsors" de projets open-source sont légion : SensioLabs pour Symfony bien sûr, mais aussi 37Signals pour Ruby on Rails, Acquia pour Drupal, Canonical pour Ubuntu, ou encore eBay pour Magento. L'open-source, pour ces sociétés, est un **investissement**.

Donc encore une fois, rendre libre une base de code qui est la propriété d'une entreprise, c'est un acte **intéressé**, qui attend quelque chose en retour. Il n'y a rien de mal à cela. Il n'y a rien de bien non plus. En fait le bien et le mal, qui sont des valeurs **morales**, sont d'un ordre étranger à l'entreprise.

L'open-source dans l'économie de marché
---------------------------------------

Restons dans une logique d'échange, mais sortons si vous le voulez bien de la logique du don, qui est un échange toujours gratuit (même si non désintéressé), pour envisager la production de l'open-source sous l'éclairage des échanges marchands. Car une partie de la réponse à la question "pourquoi produire l'open-source ?" est à trouver dans le monde de l'entreprise. Si nous avons fait un détour par la philosophie, nous voici à présent en plein dans une logique économique.

### L'open-source n'est pas capitaliste

Et c'est un nouvel angle très intéressant qui s'offre à nous. Car la production d'open-source se pose en alternative à un autre mode d'échange. Un mode d'échange dominant dans notre société capitaliste : le **commerce**. Exemple typique de transaction commerciale : j'aime cette table que tu as construite, je te donne de l'argent en échange. Je perds de l'argent mais je gagne une table ; tu perds une table mais tu gagnes de l'argent. Nous sommes tous les deux gagnants dans cet échange. C'est pourquoi le commerce est un mode d'échange si populaire : chacun y trouve son compte.

Et l'open-source ? Quelle alternative propose l'open-source à ce mode d'échange bien rôdé ? Ça ne peut pas se réduire à supprimer l'argent, ça n'aurait aucun sens. J'aime cette table open-source que tu as construite, je la prends sans rien te donner en échange. Je n'ai rien perdu mais tout gagné. Tu as perdu une table et tu n'as rien gagné en échange. Ça ne marche pas. Il doit donc y avoir quelque chose d'autre que la simple gratuité. Sous l'angle de l'échange, l'open-source n'est donc pas réductible à la formule "Free (as in beer)".

En fait, l'open-source ne rentre pas bien dans les canons du capitalisme. Selon Marx (je parle de Karl, pas Groucho), le capitalisme repose sur trois piliers : le premier est la possession de l'appareil de production (la propriété privée). Le second, c'est la libre concurrence. Le dernier, le salariat. Or, dans le monde open-source, personne ne possède le logiciel, puisque tout le monde peut se l'approprier, n'importe qui peut le revendre, ou le "forker".

La libre concurrence existe de fait dans l'open-source, puisque la mise à disposition des sources met tout le monde au même niveau. Mais le problème, dans le logiciel libre, n'est pas d'avoir accès au bon produit sans entrave commerciale. Le problème est de trouver le bon produit dans un océan de produits médiocres. Il n'y a qu'à essayer de chercher une bibliothèque de templating en JavaScript pour se rendre compte que la libre concurrence, dans ce domaine, ne garantit pas la réussite du meilleur.

Enfin, le salariat, ou l'assujettissement d'un travailleur par celui qui possède l'appareil de production, est un mode de travail de moins en moins répandu chez les informaticiens. En période de quasi-plein emploi, en effet, les informaticiens sont toujours plus nombreux à s'établir comme indépendants, qui est un statut plus rémunérateur. Je n'ai pas retrouvé la source de cette statistique, mais je crois que le taux d'indépendants dans les métiers informatiques en France est de plus de 30%, là où la moyenne dans les autres métiers est autour de 12%.

L'open-source n'est donc pas un mode d'échange capitaliste. Il est pourtant abondamment utilisé par les sociétés, qui sont la colonne vertébrale du système capitaliste. Comment comprendre cette opposition ?

### Open-source et valeur ajoutée

Les entreprises recherchent du profit, c'est leur raison d'être. Et **le fait est** qu'elles trouvent du profit, ou de la valeur, dans l'open-source. L'open-source crée de la **valeur ajoutée**.

Vous êtes tous ici des témoins de cette création de valeur. **Vos sociétés** gagnent de l'argent grâce à l'open-source. L'open-source crée par exemple de nouvelles opportunités de service. Car si je choisis d'utiliser Symfony, je devrai trouver des développeurs connaissant déjà ce framework pour m'assister. Je vais donc payer une société de service ou un indépendant pour m'assister dans cette tâche.

L'open-source a considérablement amélioré notre **productivité**. Au lieu de réinventer la roue en permanence, nous assemblons des composants libres, souvent de plus en plus interopérables. L'open-source a également considérablement réduit les **coûts de possession et de production** informatique. Elle ouvre ainsi la porte à de nouveaux acteurs qui n'ont pas besoin d'un gros investissement pour toucher une clientèle **mondiale**.

En accélérant le développement, l'emploi de bibliothèques open-sources permet aussi d'éditer **plus vite** de nouveaux produits. Facebook, Twitter et Google sont les exemples les plus souvent cités de sociétés ayant créé une valeur gigantesque en un temps record, en s'appuyant sur des composants open-source. Notez d'ailleurs que toutes ces sociétés, aujourd'hui, sont également contributrices de **l'écosystème** open-source, parce qu'elles ont compris que là était leur intérêt.

L'échange gratuit de code a donc sa place dans un système capitaliste, parce qu'il crée de la **valeur ajoutée**. Et il arrive aussi qu'il en détruise. Depuis Git, Microsoft a beaucoup plus de mal à vendre du Team Foundation Server. Depuis Magento, IBM a du mal à vendre du WebSphere Commerce. Depuis Gimp... Adobe n'a pas plus de mal à vendre Photoshop, mais vous avez déjà essayé d'utiliser GIMP ? Revenons à la destruction de valeur. Elle ne concerne pas que les vendeurs de logiciels. L'open-Source a donné naissance aux géants du web, qui ont balayé des **secteurs entiers** de l'économie. Je pense à Amazon qui a quasiment détruit le secteur de librairie, je pense à Google Maps et aux GPS qui ont détruit le secteur de la carte papier, et il y en a d'autres.

C'est que l'Open-Source est un outil puissant, et comme le disait un grand économiste aujourd'hui disparu, "With great power comes great responsibility". Un autre économiste, Joseph Schumpeter, a théorisé cela dans les années 40 : ça s'appelle la **destruction créatrice**. L'innovation porte la croissance économique sur le long terme, même si ça implique dans l'immédiat des dégâts importants sur l'activité des entreprises, et donc sur les emplois, et donc sur notre société.

### Un contrepoids économique

L'open-source a donc pleinement sa place dans le système capitaliste, puisqu'elle peut créer et détruire de la valeur ajoutée, ou autrement dit, du profit. L'open-source fait se rencontrer l'économie du don et l'économie de marché, alors que tout les oppose. C'est aussi parce que l'économie de marché, laissée libre et sans limitation, a amené des dérives. L'une de ces dérives est la **financiarisation**, où il n'y a même plus de marchandise dans l'échange commercial, juste des produits financiers. En quelque sorte, l'open-source prend le contrepied de cette tendance. L'open-source propose exactement l'inverse : un échange de marchandise (certes dématérialisée) **sans enjeu financier**. Et ainsi, l'open-source ramène le capitalisme à un équilibre salutaire.

Produire l'open-source : un acte politique ?
--------------------------------------------

Voir l'open-source comme un contrepoids des dérives du capitalisme revient à admettre que nous avons besoin de **limiter** le domaine de l'économie de marché par un autre domaine, qui prendrait davantage en compte les intérêts collectifs. Ce domaine, c'est celui du **politique**. Je pense que l'open-source, au-delà de son action sur les entreprises, a un effet sur notre société. C'est donc un instrument politique.

### La nécessité du politique

Imaginez un instant que nous laissions les entreprises décider du futur de l'open-source. Elles risqueraient de la réduire à sa dimension de création de valeur. Elles risqueraient d'en faire un instrument de croissance, certes redoutablement efficace, mais plus très humain. Elles mettraient sans  doute de côté tout l'aspect création de lien social, à moins que ça profite à la gestion des ressources humaines, qui sert elle-même, pas à notre bien être, mais la création de profit. Je pense à Oracle par exemple, dont l'acquisition de **produits phares** de l'écosystème open-source (MySQL, Java, OpenOffice) a quand même laissé un goût amer.

Plus généralement, la politique est nécessaire pour limiter les dérives des marchands, des scientifiques, des techniciens. On a déjà tenté de libérer le commerce du contrôle du politique, ça s'appelle **l'ultra libéralisme**. Laissez-faire les marchés, ils se réguleront tous seuls, disait Milton Friedman, prix Nobel d'économie en 1976. Il n'a malheureusement pas vécu assez longtemps pour voir la chute de Lehman Brothers, et une crise quasiment sans précédent dont l'occident peine à se relever. Comme les économistes, les scientifiques repoussent sans cesse les limites du possible. Ça rend d'autant plus indispensable de fixer les limites de **l'acceptable**.

Quels sont les instruments de contrôle dont la société dispose pour éviter les dérives de la sphère commerciale ? Il n'y en a pas beaucoup. Le plus efficace est **la loi**. Et la loi, c'est vous et moi, le peuple souverain, qui la décidons. Vous me direz que la loi, outil national, n'est pas des plus efficaces pour contrôler les grandes sociétés d'aujourd'hui, qui sont **multinationales**. Et vous aurez raison. Vous me direz également que votre petite voix n'a pas le pouvoir de changer la loi. Et vous aurez tort. Car si votre voix ne compte pas, si votre voix ne permet pas d'adapter la loi, alors nous vivons dans une dictature. Mais pas une dictature causée par le putsch d'un illuminé. Une dictature causée par l'abandon du pouvoir, ce qui à mon sens est mille fois pire.

Il existe un autre moyen, moins efficace, pour faire pression sur les entreprises. C'est le **lobbying**. Voyez comment des groupes de pression arrivent à faire plier Facebook lorsqu'il décide unilatéralement de rendre publiques des données qui étaient jusqu'ici privées. Mais la seule chose qui oblige vraiment les entreprises à reculer, dans ce cas, c'est la force du nombre. Et si le nombre existe pour faire du lobbying, je ne vois pas pourquoi il n'existerait pas pour élire des députés qui lui ressemblent. On en revient donc au peuple souverain, vous et moi, qui pouvons, qui **devons** décider ensemble de l'avenir de l'open-source.

### L'action politique

L'action politique ne se réduit pas à voter, puis à espérer que nos gouvernants fassent le bon choix. Nous pouvons tous, individuellement, œuvrer pour le collectif. Et c'est là la plus grande force de l'open-source. Elle a un pouvoir collectif totalement **démesuré** par rapport à l'effort qu'elle implique. Comparez une seconde l'effet de la publication d'un livre de thèses politiques avec l'effet de la publication d'un framework open-source comme Symfony. Dans un cas, vous attirez l'attention de vos compatriotes sur des problèmes. Vous avancez des revendications pour que d'autres (les législateurs) puissent **peut-être** résoudre ce problème. Dans l'autre cas, vous produisez des **solutions**, immédiatement applicables par le plus grand nombre à des problèmes **concrets**. Contribuer une librairie peut permettre à des collectivités, au même titre que des entreprises, de dépenser moins et de produire davantage de services - médical, social, militaire, judiciaire, éducatif.

L'open-source, née dans le code, essaime dans de nombreux autres domaines. On voit des encyclopédies open-source (avec Wikipedia), des modèles 3D open-source (vous connaissez SketchFab ?), des recettes de cuisine open-source (avez-vous déjà bu du OpenCola ?), et demain quoi ? Une fusée interstellaire open-source ? Un gouvernement open-source ? La démocratisation du savoir, la mise à disposition de tous de la connaissance de chacun, gratuitement, ce mouvement est lancé. Il ne s'arrêtera pas de sitôt. La production open-source est en train de transformer notre société.

L'action politique, c'est le contraire de la passivité, c'est la réaction à l'apathie. C'est ouvrir un pont entre le domaine privé et le domaine publique, se laisser l'opportunité de devenir un parmi les autres. **Etre entre** se dit en latin "inter esse", et c'est de cette racine que vient le mot "intérêt", comme le souligne Hannah Arendt dans "La condition Humaine". L'intérêt nous relie les uns aux autres en un seul peuple, nous fait avancer ensemble. L'open-source, c'est notre **intérêt**.

Tout reste à inventer dans l'action politique via l'open-source, et c'est aussi ça qui est excitant. Nous pouvons à nouveau **changer le monde**, non pas en manifestant dans les rues, mais en produisant des outils, en partageant des recettes techniques, en assemblant les inventions d'autres créateurs. Les possibilités sont immenses. On pourrait dire qu'une nouvelle ère s'ouvre à nous grâce à l'open-source. Richard Stallman, qui a fondé le mouvement de l'open-source dans les années 80, était sans doute loin de se douter que ses modestes intentions allaient déboucher sur une **révolution**.

Conclusion: Un monde open-source
--------------------------------

Révolution, le mot est lâché, juste à temps pour ma conclusion. Encore une fois, on ne parle pas de révolution d'ordre **moral**. Produire de l'open-source ne fera pas avancer la bonté, ni la vérité d'ailleurs. L'open-source doit se voir comme un échange, d'abord entre individus, pour créer du lien, ensuite entre sociétés, pour créer de la valeur, sans passer par des échanges marchands. N'ayez pas peur que ce soit votre intérêt personnel ou commercial qui dicte votre envie d'en faire partie. Le résultat est là : la mise en commun de nos égoïsmes, sur des bases intelligentes, prépare une ère nouvelle.

Et surtout, produire de l'open-source nous permet de reprendre la main, d'avoir un effet notable sur l'évolution de notre société, d'avoir une action politique enfin, dans une époque où le repli sur l'individu provoque des dégâts considérables sur le tissu social.

La puissance de l'open-source est **redoutable**. **Votre** contribution open-source peut profiter à des **milliers** de développeurs, qui eux-mêmes produiront des centaines de nouveaux outils s'appuyant sur votre travail. Et quand tout le monde aura accès à l'ensemble de la connaissance humaine, à l'ensemble des outils et techniques nés de cette connaissance, vivrons-nous dans la même société ? Je pense que non. Je pense que ce sera une société très différente. Mais c'est sur vous que repose la responsabilité d'en faire une société meilleure, plus équilibrée, plus belle et plus forte. Continuez à faire de l'open-source. Vos enfants vous remercieront.

<blockquote><i>Merci d'être resté jusqu'au bout ! Vos remarques et questions sont les bienvenues.</i></blockquote>
