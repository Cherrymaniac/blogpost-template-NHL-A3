---
layout: post
title: Milestone 1
categories: Blog IFT6758_A3
---

# Question 1 : Acquisition de données

Dans cette section, nous détaillons le fonctionnement de la classe NHLDataDownloader qui gère l'acquisition des données brutes depuis l'API de la NHL. Elle se compose de trois parties principales : l'initialisation, la récupération des données, et le traitement des données.

## Initialisation de la classe
L'initialisation de la classe `NHLDataDownloader` se fait à l'aide de trois arguments :

* start_season et final_season : Ces paramètres définissent la plage des saisons NHL à récupérer (par exemple, de 2016 à 2023).
* data_dir (facultatif) : Ce paramètre permet de spécifier le répertoire de sauvegarde des données. Si aucun répertoire n'est fourni, le répertoire courant est utilisé par défaut.

Les fichiers clés sont générés automatiquement dans le répertoire choisi :

1.  nhl_game_data.json : Contient les données brutes des matchs.
2.  nhl_player_data.json : Contient les noms des joueurs associés à leurs ID.
3.  parsed_shot_events.csv : Contient les données traitées relatives aux tirs.

```python
class NHLDataDownloader:
    def __init__(self, start_season, final_season, data_dir=None):
        self.start_season = start_season
        self.final_season = final_season
        self.data_dir = data_dir if data_dir else os.getcwd()
        self.nhl_games_file_path = os.path.join(self.data_dir, 'nhl_game_data.json')
        self.nhl_players_file_path = os.path.join(self.data_dir, 'nhl_player_data.json')
        self.parsed_data_path = os.path.join(self.data_dir, 'parsed_shot_events.csv')
```
## Récupération des données de jeu de la NHL
La méthode `get_nhl_game_data` permet de récupérer les données de jeu directement depuis l'API de la NHL. Cette méthode effectue les étapes suivantes :

1. Construction de l'identifiant de match : Chaque match NHL est identifié par un `gameId`, qui est utilisé pour faire des requêtes à l'API de la NHL. Ce `gameId` est basé sur l'année de la saison et un numéro de match.
2. Requête à l'API : Pour chaque match, une requête HTTP est envoyée à l'API de la NHL pour récupérer les événements du match.
3. Sauvegarde des données brutes : Les données sont stockées dans un dictionnaire local nommé `all_data`, puis sauvegardées dans un fichier JSON (`nhl_game_data.json`) pour être utilisées lors des étapes ultérieures de traitement des données.

 `all_data`.
```python 
def get_nhl_game_data(self):
    all_data = {}
    for season in range(self.start_season, self.final_season + 1):
        # ... (code to determine number of games)
        for game_num in range(1, num_regular_season_games + 1):
            game_id = f'{season}02{game_num:04d}'
            url = f'https://api-web.nhle.com/v1/gamecenter/{game_id}/play-by-play'
            response = requests.get(url)
            game_data = response.json()
            all_data[game_id] = game_data
```

Cette méthode prend également en compte (en plus des parties de saison régulière) les parties des séries éliminatoires. Cette approche permet d'acquérir une grande quantité de données pour les saisons spécifiées, couvrant ainsi tous les matchs joués au cours de ces saisons. Bref, la classe `NHLDataDownloader` permet d'automatiser la récupération de données depuis l'API de la NHL, et de structurer ces données en vue de leur traitement et analyse future.

# Outil de débogage interactif: Outil piwydget


# Nettoyage des données 
Le traitement des données brutes est un aspect essentiel de l’analyse, et cela se fait dans la méthode `parse_nhl_game_data` de la classe `NHLDataDownloader`. Voici les étapes principales que cette méthode suit pour extraire et organiser les données relatives aux tirs dans les matchs de la NHL :



* Chargement des données de jeu : La méthode commence par vérifier si un fichier CSV contenant les événements de tir a déjà été généré. Si c’est le cas, ce fichier est chargé pour éviter de retraiter les mêmes données. Sinon, elle procède à l'extraction des données à partir du fichier JSON qui contient les données brutes des matchs, précédemment sauvegardé par la méthode `get_nhl_game_data`.

* Filtrage des événements de tir : À partir des données brutes de chaque match, la méthode parcourt chaque événement (play) pour identifier ceux liés aux tirs, c’est-à-dire les événements de type 505 (but) et 506 (tir raté). Une fois identifiés, ces événements sont filtrés et les détails importants, comme l'identité du tireur, du gardien, le type de tir, et la situation du jeu, sont extraits.

* Gestion des données des joueurs : Pour enrichir les données des événements, la méthode fait appel à `get_player_name` qui associe les identifiants des joueurs (ID) à leurs noms complets. Cette méthode appelle l'API de la NHL pour récupérer les noms des joueurs à partir de leur ID si ceux-ci ne sont pas déjà stockés dans un fichier local (`nhl_player_data.json`). Une fois le nom récupéré, il est ajouté au dictionnaire des joueurs pour des requêtes futures plus rapides qui a pour but d'éviter les requêtes redondantes à l'API. 

* Création d’un DataFrame : Pour chaque match, les événements de tir sont stockés dans une liste. À la fin de l'extraction des tirs pour un match, cette liste est convertie en un DataFrame Pandas. Ces DataFrames individuels sont ensuite concaténés en un seul DataFrame global qui regroupe tous les tirs des saisons spécifiées.

* Sauvegarde des données traitées : Une fois que tous les événements de tir sont extraits et organisés dans le DataFrame, les données sont sauvegardées dans un fichier CSV pour éviter de répéter le traitement lors des exécutions futures.

``` python
def parse_nhl_game_data(self):
    all_shot_events_df = pd.DataFrame()
    with open(self.nhl_games_file_path, 'r') as json_file:
        game_data = json.load(json_file)
    for game_id, game_details in game_data.items():
        all_plays = game_details.get('plays', [])
        shot_events = []
        for play in all_plays:
            event_type = play.get('typeCode')
            if event_type in [505, 506]:
                # ... (code to extract shot details)
                shot_events.append(shot_details)
        if shot_events:
            shot_events_df = pd.DataFrame(shot_events)
            all_shot_events_df = pd.concat([all_shot_events_df, shot_events_df], ignore_index=True)
```

Grâce à ce processus, les données brutes de la NHL sont transformées en un format plus exploitable, permettant ainsi une analyse plus approfondie, comme l'exploration des tirs et des buts par type ou la comparaison de la performance des joueurs.


# Visualisations Simples

## 1. Comparaison des types de tirs

Nous commençons par comparer la fréquence des différents types de tirs, en visualisant à la fois le nombre total de tirs et le nombre de buts marqués pour chaque type de tir. Pour se faire nous avons décidé de répresenter ça dans un histogramme en barres ou les tirs sont mis à coté des goals marqués.

!["Nombre de tirs et de buts par type de tir"](/assets/images/Bar_typetirbut.jpg)
Le graphe ne nous aide pas vraiment à cause de la disparité dans les valeurs des données tirs/buts, nous representons donc ça en changeant l'échelle de l'axe des ordonnées en logarithmique, nous ajoutons également un graphe représentant les pourcentages sur l'axe des ordonnées opposées:
!["Nombre de tirs et de buts par type de tir (Log) et pourcentage"](/assets/images/shottypelog.png)
De ce graphe, nous observons:
* `Tir le plus dangereux` : Le tir cradle a le pourcentage de réussite le plus élevé, bien qu'il soit le moins utilisé.

* `Tir le plus commun` : Le tir du poignet est de loin le plus courant, comme le montre le nombre d'essais par rapport aux autres types de tirs. Cependant, son pourcentage de réussite n'est pas aussi élevé que celui d'autres tirs moins courants, comme le bat ou le tip in.

## Analyse de la Relation entre la Distance des Tirs et les Chances de But
Nous avons choisi de répondre à la question 2 à l'aide d'un graphique en courbes avec la distance en abscisse et le taux de probabilité de but en ordonnée. Nous avons également décidé de tracer les trois saisons sur le même graphique pour mieux observer les variations entre elles. Cela montre clairement qu'il existe une relation inverse entre la distance et le taux de réussite d'un but. Plus un tir est proche du but, moins le gardien a de temps pour réagir, ce qui augmente la probabilité de marquer.
!["Taux de Buts en Fonction de la Distance au But par Saison (2018-2021)"](/assets/images/Tauxdebutdistance.jpg)
De ce graphe, nous observons:
* Le taux de probabilité de marquer un but selon la distance est stable par saison.
* Une augmentation du taux de but à la distance [80,90] à la saison 2020-2021.

## Visualisation du Pourcentage de Buts en Fonction de la Distance et des Types de Tirs
Pour répondre à cette question; nous avons décidé de représenter la relation entre la distance, le type de tir et le taux de réussite de marquage d'un but par une heatmap.
![" Pourcentage de Buts en Fonction de la Distance et des Types de Tirs"](/assets/images/Heatmap_final.png)
Nous pouvons observer:
* Le cradle est le type de tir le plus dangereux entre [0,10], le tir bat est second.
* De 0 à 30, les tirs snaps et slaps sont les plus dangereux.
* A une distance de 40 à 50, le poke est le plus dangereux avec taux de réussite de 40%.
# Visualisations Complexes
    
## Analyse de l’équipe Colorado Avalanche, comparaison des cartes de tirs entre 2016-2017 et 2020-2021
Lors de la saison 2016-2017, l'équipe de Colorado Avalanche affiche un taux de tirs relativement faible devant le filet (à 10-20 pieds du but) comparé à la moyenne de la ligue à la même position. En revanche, pendant la saison 2020-2021, on observe une augmentation du taux de tirs près du filet, ce qui pourrait expliquer leur montée dans le classement entre 2016 et 2020.

## Comparaison entre Buffalo Sabres et Tampa Bay Lightning, basée sur leurs cartes de tirs



