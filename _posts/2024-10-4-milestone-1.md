---
layout: post
title: Milestone 1
categories: Blog IFT6758_A3
---

# Question 1 : Acquisition de données

Nous allons explorer la classe `NHLDataDownloader`, son constructeur et les méthodes associées à l'acquisition de données. 
## Initialisation de la classe
Nous commençons par construire un objet NHLDataDownloader. Dans le constructeur __init__ nous définissons les attributs suivants:
* start_season et final_season définissent la plage de saisons à extraire.
* data_dir spécifie où stocker les fichiers de données.
* Les chemins de fichiers pour les données de jeu, les données des joueurs et les événements de tir sont définis à partir de datadir .

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
Dans la méthode 'get_nhl_game_data', nous avons crée une boucle qui traverse chaque saison et chaque jeu donnée à la construction de NHLDataDownloader. On construit l'URL de l'API pour chaque jeu et on récupère les données de jeu pour les stocker dans le dictionnaire `all_data`.
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



# Outil de débogage interactif: Outil piwydget


# Nettoyage des données 
Maintenant que vous avez obtenu et exploré un peu les données, nous devons formater les données de manière à faciliter l’analyse.
Dans la méthode 'parse_nhl_game_data', on:
* Lit les données de jeu stockées.
* Filtre les événements de tir (types d'événements 505 et 506).
* Extrait les détails pertinents pour chaque tir.
* Combine tous les événements de tir dans un seul DataFrame.

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


# Visualisations Simples

## 1. Comparaison des types de tirs

Nous commençons par comparer la fréquence des différents types de tirs, en visualisant à la fois le nombre total de tirs et le nombre de buts marqués pour chaque type de tir. Pour se faire nous avons décidé de répresenter ça dans un histogramme en barres ou les tirs sont mis à coté des goals marqués.

!["Nombre de tirs et de buts par type de tir"](/assets/images/Bar_typetirbut.jpg)
Le graphe ne nous aide pas vraiment à cause de la disparité dans les valeurs des données tirs/buts, nous representons donc ça en changeant l'échelle de l'axe des ordonnées en logarithmique, nous ajoutons également un graphe représentant les pourcentages sur l'axe des ordonnées opposées:
<!-- !["Sous figure ombre de tirs et de buts par type de tir"](/assets/images/Sousfigure_Bartypetirbut.jpg)"""-->
!["Nombre de tirs et de buts par type de tir (Log) et pourcentage"](/assets/images/Log_bar_typetirbut.jpg)
De ce graphe, nous observons:
* `Tir le plus dangereux` : Le tir cradle a le pourcentage de réussite le plus élevé, bien qu'il soit le moins utilisé.

* `Tir le plus commun` : Le tir du poignet est de loin le plus courant, comme le montre le nombre d'essais par rapport aux autres types de tirs. Cependant, son pourcentage de réussite n'est pas aussi élevé que celui d'autres tirs moins courants, comme le bat ou le tip in.

## Analyse de la Relation entre la Distance des Tirs et les Chances de But
!["Taux de Buts en Fonction de la Distance au But par Saison (2018-2021)"](/assets/images/Tauxdebutdistance.jpg)


## Visualisation du Pourcentage de Buts en Fonction de la Distance et des Types de Tirs
![" Pourcentage de Buts en Fonction de la Distance et des Types de Tirs"](/assets/images/Heatmap_but_distance.jpg)

# Visualisations Complexes

