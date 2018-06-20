---
title: "Leboncoin : location Lilloise"
date: 2018-04-10T20:44:00+02:00
draft: false
---

En matière de location d'appartements, le site Leboncoin (LBC) est une
plateforme permettant de nombreux échanges entre les propriétaires et
locataires potentiels. Il rassemble un nombre élevé d'annonces venant
aussi bien de particuliers que de professionnels.

LBC présente une interface classique qui permet d'entrer des critères et
retourne une liste de biens à partir de ces derniers.

Dans l'exemple ci-dessus, 400 résultats ont été trouvés pour les
critères sélectionnés suivants :

>3 pièces à Lille

![listing-leboncoin](/img/homebot/lbc-liste.png)

Afin de naviguer plus facilement dans cette masse de résultats,on aura
tendance à chercher le bouton permettant de visualiser les résultats sur
une carte interactive...et continuer de le chercher un certain temps...

## Absence de carte

LBC n'offre pas la possibilité d'afficher les résultats d'une recherche
sur une carte interactive.

Il est possible d'essayer de limiter le nombre d'annonces retourné en
utilisant des mots clés, par exemple le nom d'un quartier.

Il faut alors cliquer sur chacun des liens pour obtenir la localisation
du bien (latitude,longitude).

La lecture des annonces proposées sur LBC montre que les propriétaires
sont assez frileux à révéler l'emplacement précis de leur bien et ne
partagent souvent qu'un nom de rue dans la description de l'annonce,
dans ces cas il n'existe pas de localisation géographique associée.

![pas-de-localisation](/img/homebot/lbc-carte-generique.png)

Il est alors intéressant de s'interroger sur le moyen d'automatiser
l'extraction de ces données. afin de cibler beaucoup plus rapidement les
annonces susceptibles d'intéresser un utilisateur ?

## Apprendre à lire à la machine

Extraire une adresse pour une machine n'est pas, techniquement, quelque
chose d'évident. Il n'y a pas de modèle fixe qui décrit la structure
d'une voie de façon précise.A cela s'ajoute le fait que ces adresse soient saisi
manuellement par une personne : un être humain n'a pas la régularité d'une machine.

Le Deep Learning permet d'appréhender les cas de données non structurés
de façon pertinente.

La problématique que l'on souhaite traiter se nomme [**N**amed
**E**ntity
**R**ecognition](https://en.wikipedia.org/wiki/Named_entity_recognition)
(NER)

On montre à notre algorithme un certain nombre d'exemples qui lui permet
d'**apprendre** à reconnaître les critères que l'on souhaite extraire,
par exemple une adresse. On combine également à ce résultat quelques
heuristiques. La machine est ensuite capable d'identifier plusieurs
aspects d'une annonce :

><div class="entities" style="line-height: 2.5"></br>Loue bel appartement dans résidence 
<mark class="entity" style="background: #ddd; padding: 0.45em 0.6em; margin: 0 0.25em; line-height: 1; border-radius: 0.35em; box-decoration-break: clone; -webkit-box-decoration-break: clone">
    rue Catel Beghin
    <span style="font-size: 0.8em; font-weight: bold; line-height: 1; border-radius: 0.35em; text-transform: uppercase; vertical-align: middle; margin-left: 0.5rem">ADDR</span>
</mark>
 (ADDRESSE) au 
<mark class="entity" style="background: #ddd; padding: 0.45em 0.6em; margin: 0 0.25em; line-height: 1; border-radius: 0.35em; box-decoration-break: clone; -webkit-box-decoration-break: clone">
    4ème étage
    <span style="font-size: 0.8em; font-weight: bold; line-height: 1; border-radius: 0.35em; text-transform: uppercase; vertical-align: middle; margin-left: 0.5rem">ETAGE</span>
</mark>
 (ETAGE) avec un grand balcon et une place de parking</br>Entrée avec rangements, séjour avec parquet, balcon, cuisine entièrement équipée (avec lave-vaisselle et four notamment), salle de bains, wc, 2 chambres.</br>Charges mensuelles 80€ Loyer mensuel : 900€ hors charges</br>Disponible à partir du 
<mark class="entity" style="background: #bfe1d9; padding: 0.45em 0.6em; margin: 0 0.25em; line-height: 1; border-radius: 0.35em; box-decoration-break: clone; -webkit-box-decoration-break: clone">
    1er Août 2018
    <span style="font-size: 0.8em; font-weight: bold; line-height: 1; border-radius: 0.35em; text-transform: uppercase; vertical-align: middle; margin-left: 0.5rem">DATE</span>
</mark>
 (DATE DISPONIBILITE) .</br>Rafraichissement de l'appartement sera effectué en 
<mark class="entity" style="background: #ddd; padding: 0.45em 0.6em; margin: 0 0.25em; line-height: 1; border-radius: 0.35em; box-decoration-break: clone; -webkit-box-decoration-break: clone">
    Juillet
    <span style="font-size: 0.8em; font-weight: bold; line-height: 1; border-radius: 0.35em; text-transform: uppercase; vertical-align: middle; margin-left: 0.5rem">MOIS</span>
</mark>
 (MOIS) avant l'entrée des nouveaux
</div>

## Carte interactive

Le résulat est disponible [ici](http://emknext.surge.sh/)

<a href="http://emknext.surge.sh">
<img src="/img/homebot/demo.gif" alt="Homebot">
</a>
