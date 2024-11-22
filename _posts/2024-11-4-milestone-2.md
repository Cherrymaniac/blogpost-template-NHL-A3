---
layout: post
title: Milestone 2
categories: Blog IFT6758_A3
---

Edward Habelrih, Michel Wilfred Essono et Rayan Yahiaoui
# Suivi des Expériences

Tout au long de ce milestone, nous avons utilisé Weights & Biases (Wandb) pour sauvegarder et suivre nos modèles à travers leurs différentes itérations, ce qui nous a permis de comparer les résultats au fil du temps. Cet outil s’est avéré extrêmement utile, offrant à l’équipe un moyen simple et interactif de surveiller les progrès. Pour chaque exécution, nous avons enregistré les figures pertinentes ainsi que les paramètres de configuration utilisés pour entraîner le modèle. De plus, les modèles ont été sauvegardés en tant qu’artifacts associés à leurs exécutions respectives.

Voici le lien vers notre espace de travail: https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03
# Ingénierie des Caractéristiques I

## 2.1 Histogrammes des Tirs

### Distance du Filet
Nous avons généré deux histogrammes illustrant le nombre de tirs (buts et non-buts séparés) en fonction de leur distance par rapport au filet, à partir des données des saisons régulières 2016-2017 à 2019-2020 (inclus). 

![Histogrammes des Tirs - Distance](/assets/images/milestone2/Distribution_Tirs_par_Distance(2016-2019).png)

Voici les observations clés:
  - Le nombre total de tirs diminue rapidement aux alentours de 60 mètres. 
  - Plus la distance agumente, moins il est probable qu'un but soit marqué.
  - Les tirs provenant de la moitié défnesive de la patinoire sont extrêmement rares, et encore plus les buts.
  - Les tirs effectués à très courte distance (<10m) ont une fréquence élevée, ce qui reflète une proximité stratégique pour maximiser les chances de marquer.


### Angle par Rapport au Filet

Nous avons également produit deux histogrammes montrant la répartition des tirs selon leur angle relatif au filet.

![Histogrammes des Tirs - Angle](/assets/images/milestone2/Distribution_Tirs_par_Angle(2016-2019).png)

Voici les observations clés:
- La majorité des tirs sont effectués directement face au filet ou à un angle modéré (environ ±30 degrés).
- Les buts sont souvent marqués à des angles réduits (autour de 0 degré).
- La fréquence des buts diminue significativement pour des angles au-delà de ±30 degrés.
- Les angles extrêmes (±70 degrés ou plus) sont rares, et ils résultent rarement en buts, probablement en raison de la difficulté accrue de viser avec précision sous ces conditions. Le gardien a aussi moins de surface de but à couvrir pour empêcher la rondelle de rentrer plus l'angle du joueur adverse est accentué. 

### Diagramme de Dispersion 2D

Un diagramme 2D représentant la distance et l'angle a été créé pour tous les tirs.

![Diagramme de Dispersion 2D](/assets/images/milestone2/Distribution_Conjointe_Tirs_Angle_Distance(2016-2019).png)

Voici les observations clés:
- Les tirs proches du filet couvrent une plus grande variété d'angles, y compris des angles extrêmes.
- Les tirs plus éloignés ont tendance à être concentrés autour de petits angles (dû à leur distance éloignée du but l'angle de tir est réduit).
- Les zones de tirs fréquentes incluent :
  - Les tirs rapprochés du filet
  - Les tirs autour de 60m
  - Les angles proches de ±30 degrés
- Les tirs sous des angles extrêmes (>±70 degrés) ne se produisent que dans des situations spécifiques et sont souvent liés à des filets vides ou à des tirs désespérés.

L’analyse des distances et des angles des tirs met en lumière l'importance stratégique de la proximité du filet et des angles favorables dans la probabilité de marquer. La plupart des tirs sont tentés à courte distance, dans les zones de haut danger situées devant le filet, et sous des angles réduits, ce qui reflète une approche axée sur l'efficacité et la pression offensive. Les tirs effectués à longue distance, souvent depuis la ligne bleue ou au-delà, ou sous des angles extrêmes près des bandes, sont beaucoup moins fréquents et rarement convertis en buts. Cependant, ces tirs lointains ou difficiles peuvent jouer un rôle tactique en générant des rebonds ou en profitant de filets vides lors de situations désespérées en fin de match.

## 2.2 Taux de Buts par Distance et Angle

Nous avons aussi créé des figures reliant le taux de but à la distance et à l'angle du tir.

![Taux de Buts - Distance](/assets/images/milestone2/Taux_Tirs_Distance(2016-2019).png)

Voici les observations clés: 
- Le taux de buts (#buts / (#buts + #non_buts)) diminue nettement à mesure que la distance par rapport au filet augmente.
- Les tirs effectués depuis la zone de haut danger, située dans le slot ou près du cercle des mises en jeu, présentent les taux de buts les plus élevés.
- Pour les distances extrêmes, de petites fluctuations dans le taux de buts sont observées, souvent liées aux situations de filet vide, où les joueurs peuvent tenter des tirs depuis leur propre zone défensive.

![Taux de Buts - Angle](/assets/images/milestone2/Taux_Tirs_Angle(2016-2019).png)

Voici les observations clés: 
- Les tirs effectués avec un faible angle (proche de 0 degré, directement face au filet) ont le taux de conversion en buts le plus élevé.
- Les tirs effectués sous des angles supérieurs à ±30 degrés, par exemple à proximité des bandes, voient leur probabilité de marquer diminuer fortement.
- Les tirs tentés à des angles extrêmes, souvent associés à des situations de désespoir en fin de période ou de match, sont rarement convertis en buts, à l’exception de tirs déviés ou frappés dans des filets vides.

L'analyse montre clairement que la probabilité de marquer diminue avec l'augmentation de la distance et des angles extrêmes, mettant en évidence l'importance des zones de haut danger autour du filet. Les fluctuations observées à grande distance, principalement dans des situations de filet vide, soulignent l'influence des circonstances spécifiques sur la qualité des tirs. Ces résultats confirment l'importance de prendre en compte à la fois la distance et l'angle comme facteurs essentiels dans la modélisation des buts attendus, tout en intégrant des contextes tactiques des diverses équipes.

## 2.3 Buts sur Filet Vide vs Filet Non-Vide
 Finalement analyzons la relation entre le nombre de buts et la distance des tirs effectués. 

![Histogrammes - Filet Vide et Non-Vide](/assets/images/milestone2/Nb_total_tirs_par_Distance.png)

Pour les tirs sur un filet Non-Vide voici les observations clés:
- La majorité des buts sur filet non-vide sont marqués à proximité immédiate du filet, dans la zone de haut danger. Ces tirs sont souvent effectués à partir de rebonds ou de passes rapides qui laissent peu de temps au gardien pour réagir.
- Les tirs effectués à plus de 30m voient leur probabilité de conversion en but diminuer fortement, reflétant l’efficacité des gardiens à bloquer les tirs éloignés.

Pour les tirs sur un filet Vide voici les observatinos clés:
- Les tirs sur filet vide peuvent être tentés depuis presque n'importe où sur la patinoire, y compris depuis la zone défensive ou les coins éloignés.
- Ces situations résultent généralement de la décision de l'équipe adverse de retirer son gardien pour ajouter un attaquant supplémentaire en fin de match.
- Les tirs de longue distance (parfois supérieurs à 100 pieds) sont fréquents et réussis, en raison de l'absence de gardien pour défendre le filet.

L’analyse montre des différences importantes entre les buts marqués sur filet vide et ceux sur filet non-vide. Les buts sur filet non-vide sont souvent dus à des tirs précis ou des actions rapprochées où le gardien est mis sous pression. En revanche, les filets vides permettent des tirs plus risqués et éloignés, souvent tentés depuis des positions inhabituelles. Ces résultats mettent en évidence l’influence des situations de jeu sur les opportunités de marquer et soulignent l’importance de traiter ces cas différemment dans l’analyse des buts attendus, pour mieux refléter les choix tactiques en fin de match.

**IL RESTE A PROUVER LE DERNIER POINT DE CETTE SECTION** 