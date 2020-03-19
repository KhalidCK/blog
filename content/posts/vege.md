---
title: "Le bio du coin"
date: 2020-01-26T17:03:36+01:00
draft: false
---

Consommateur régulier de fruits et légumes bio, j’ai cependant peu de
boutiques à proximité (une seul à moins de 15 min).

Comment savoir si les prix sont raisonnables ?

Après quelques recherches le [RNM](https://rnm.franceagrimer.fr/accueil)
propose un jeu de données mis à jour régulièrement (merci à la
[République numérique](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000033202746&dateTexte=&categorieLien=id)).


Pour répondre à cette question, j’ai besoin des éléments suivants :

1. Récupérer périodiquement les données sur le site du RNM

2. Transformer les données pour obtenir la réponse à ma question

3. Visualiser le résultat

<!--remettre en ordre-->

## Les outils serverless d’AWS se prêtent bien à ce genre d’architecture.

1. Récupérer périodiquement les données sur le site du RNM

   ![retrieve data](/img/vegeprice/image5.png)

2. Transformer les données pour obtenir la réponse à ma question

   ![process data](/img/vegeprice/image3.png)

3. Visualiser le résultat

   ![frontend](/img/vegeprice/image1.png)

### Vocabulaire

![lambda](/img/vegeprice/image6.png) Un morceau de code. C’est une **lambda** dans le vocabulaire AWS, elle va s'exécuter au moment opportun.

![s3](/img/vegeprice/image4.png) **AWS S3**, pour le stockage. Il a l'avantage d’être simple et peu cher (de
l'ordre de 2 centimes les 10 GB par mois)

![vuejs](/img/vegeprice/image2.png) L’application [VueJS](https://vuejs.org/) qui s'exécute sur le navigateur (Firefox,
chrome …)

Le resultat: **[VegePrice.fr](https://vegeprice.fr)**

[![peek vegeprice](/img/vegeprice/peek-vegeprice.apng)](https://vegeprice.fr)

## Les offres cloud serverless permettent de passer rapidement de l’idée à la mise en oeuvre.

Cependant, il n’y a pas de solution magique

> [There ain't no such thing as a free
> lunch](https://en.wikipedia.org/wiki/There_ain%27t_no_such_thing_as_a_free_lunch))

Cette approche demande de nouvelles expertises, moins de
contrôle direct, un pricing plus compliqué…

Pour se forger une opinion,
AWS met à disposition plusieurs ressources accessible,visible sur les
["Offre gratuite
d'AWS"](https://aws.amazon.com/fr/free/?audit=2019q1&all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=tier%23always-free)
