---
layout: post
title: Milestone 2
categories: Blog IFT6758_A3
---

Edward Habelrih, Michel Wilfred Essono et Rayan Yahiaoui

# Ingénierie des Caractéristiques I

## 2.1 Histogrammes des Tirs

### Distance du Filet
Nous avons affiché deux histogrammes du nombre de tirs avec et sans buts à partir du jeu de données (saisons régulières 2016/17 - 2019/20) présentant leur distance par rapport au filet.

![Histogrammes des Tirs - Distance](/assets/images/milestone2/Distribution_Tirs_par_Distance(2016-2019).png)

De ce graphe, nous observons:
- Lorsque la distance dépasse 60 pieds, le nombre de tirs vers le but chute rapidement.
- Plus la distance augmente, moins il y a de chances de marquer.
- Il est très rare de tirer vers le but adverse dans sa propre moitié de patinoire, et encore moins de marquer.


### Angle par Rapport au Filet

![Histogrammes des Tirs - Angle](/assets/images/milestone2/Distribution_Tirs_par_Angle(2016-2019).png)

De ce graphe, nous observons:
- Les tireurs visent souvent directement le filet ou tirent à un angle d'environ +/- 30 degrés.
- Les buts sont le plus souvent marqués en visant directement le filet.
- Au-delà de +/- 30 degrés, le nombre de buts commence à diminuer.

### Diagramme de Dispersion 2D

![Diagramme de Dispersion 2D](/assets/images/milestone2/Distribution_Conjointe_Tirs_Angle_Distance(2016-2019).png)

De ce graphe, nous observons:
- Plus près du but, les tireurs sont plus susceptibles de tenter des tirs à grand angle.
- Plus loin du filet, les tireurs ont tendance à tirer avec un angle plus petit.
- Zones de tirs les plus fréquentes :
  - Près du but
  - Autour de 60 pieds du filet
  - Angles de +/- 30 degrés

## 2.2 Taux de Buts par Distance et Angle

![Taux de Buts - Distance](/assets/images/milestone2/Taux_Tirs_Distance(2016-2019).png)
![Taux de Buts - Angle](/assets/images/milestone2/Taux_Tirs_Angle(2016-2019).png)

Conclusions similaires aux observations précédentes :
- Plus le tireur est proche du filet et plus l'angle est petit, plus les chances de marquer sont élevées.
- Le taux de buts fluctue et augmente quand on s'éloigne du filet, probablement parce que les joueurs sont plus enclins à tirer de loin quand le filet est vide.

## 2.3 Buts sur Filet Vide vs Filet Non-Vide

![Histogrammes - Filet Vide et Non-Vide](/assets/images/milestone2/Nb_total_tirs_par_Distance.png)

De ce graphe, nous observons:
- La majorité des buts sur filet non-vide sont marqués près du filet.
- Sur filet vide, les joueurs peuvent marquer de presque n'importe où sur la patinoire.