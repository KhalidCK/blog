---
title: "Quand prendre le métro à Paris ?"
date: 2018-04-10T20:44:00+02:00
draft: false
---


À Paris, le métro est une nécessité pour la majorité de ses habitants.
Il est composé de 14 lignes principales qui s'étendent sur près de 220
km. En moyenne, entre deux stations il y a 500m. Il a beaucoup
d'avantages, mais un inconvénient de taille : il est *extrêmement*
fréquenté.

Si l'on souhaite éviter la foule, il est communément admis **d'éviter**
les horaires suivants :

* Le matin entre 8 et 9h
* Le soir entre 17 et 19h

Existe-t-il des données pour confirmer ce constat empirique ? Est-il
vrai dans tous les jours de la semaine, toute l'année et pour toutes les
lignes de métro ?

*Pour les explorateurs:* [une visualisation PowerBI](https://app.powerbi.com/view?r=eyJrIjoiNDg0NWRhNTYtMGY1Zi00ZjA5LTlhYTctNDQyYjgyMmI3ZTEwIiwidCI6IjkwYzdhMjBhLWYzNGItNDBiZi1iYzQ4LWI5MjUzYjZmNWQyMCIsImMiOjh9)

**Obtenir les données**
-----------------------

Après quelque recherche sur le net,
[iledefrance-mobilites](https://www.iledefrance-mobilites.fr/)
à récemment publiés des *datasets* qui pourrait nous aider dans notre
problématique.

Il y a deux types de dataset disponibles : l'un décrit le nombre de
voyageurs annuels, l'autre le pourcentage pour chaque heure du nombre de
billets/titres de transport validés.

Après quelques manipulations et nettoyages des données, les
détails sont disponibles sur mon
[github](https://github.com/KhalidCK/metro-paris/tree/master/notebooks),
on peut commencer l'interrogation de ces dernières.

À quoi ressemble la répartition du nombre de voyageurs chaque mois
(janvier = 1 ...)

![monthly traveler in millions](/img/metro/monthly-traveler.png)

On observe sans surprise une diminution en août ; Paris est connu pour
être « vide » après le 15 août.

Comment les voyageurs se répartissent-ils sur les différentes lignes ?

Une visualisation pertinente est le *swarm plot.* Il permet de
représenter toutes les données, plutôt que d'utiliser des agrégations.

![daily passenger distribution](/img/metro/daily-passenger-distribution.png)


Chaque point représente le nombre de passagers pendant une journée en
2017.

Explorons maintenant le deuxième dataset.

Les données sont divisées en 5 profils :

> ● Dimanche, jours fériés et ponts
>
> ● Jour ouvré en période de vacances scolaires
>
> ● Jour ouvré hors période de vacances scolaires
>
> ● Samedi en période de vacances scolaires
>
> ● Samedi en période de vacances scolaires

Le taux de validation par heure est défini comme :

"le nombre de validations pour une heure et une station spécifique
divisé par le nombre total de validations dans la journée"

Pour chaque jour le pourcentage a donc pour total 100.

Une vue d'ensemble :

![average-metro-user-per-hour](/img/metro/average-metro-user-per-hour.png)

Pour chaque profil :

![facet-profile](/img/metro/facet-grid-user-per-hour.png)

**Du bon sens ?**
-----------------

Il semble que la vision empirique se confirme en **moyenne**. Cependant,
l'exploration des données (cf *[visualisation
PowerBI](https://app.powerbi.com/view?r=eyJrIjoiNDg0NWRhNTYtMGY1Zi00ZjA5LTlhYTctNDQyYjgyMmI3ZTEwIiwidCI6IjkwYzdhMjBhLWYzNGItNDBiZi1iYzQ4LWI5MjUzYjZmNWQyMCIsImMiOjh9)
)* permet d'observer que la tendance n'est pas confirmée pour toutes les
stations (exemples ?) et, que prendre le métro à des heures différentes
pour celles-ci permet d'éviter la foule
