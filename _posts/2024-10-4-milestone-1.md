---
layout: post
title: Milestone 1
categories: Blog IFT6758_A3
---

Edward Habelrih, Michel Wilfred Essono et Rayan Yahiaoui

# Procédure de roulement des notebooks
Veuillez rouler les notebooks du fichier `/notebooks` dans l'ordre suivant. Assurez-vous d'installer tous les modules des fichiers `requirements.txt` et `environment.yml`. Il se peut que vous ayez à en installer d'autres en roulant les notebooks, ceci est correct. 


1. `Acquisition_Traitement_Donnees.ipynb`
2. `Interactive_Widget.ipynb`
3. `Visualisations_Simples.ipynb`
4. `Visualisations_Complexes.ipynb`


# Question 1 : Acquisition de données

Dans cette section, nous expliquons comment utiliser la classe `NHLDataDownloader` du fichier `data_acquisisiton.py` pour gérer l'acquisistion des données brutes depuis l'API de la NHL. Ce processus se compose de trois parties principales: l'initialisation, la récupération des données, et le traitement des données. Nous allons élaborer d'avantage sur cette troisième étape dans la troisième section du blog. 

## Initialisation de la classe
L'initialisation de la classe `NHLDataDownloader` nécessite trois arguments:

* `start_season` et `final_season` : Ces paramètres définissent la plage des saisons NHL à récupérer (par exemple, de 2016 à 2023).
* `data_dir` (facultatif) : Ce paramètre permet de spécifier le répertoire de sauvegarde des données. Si aucun répertoire n'est fourni, le répertoire `data` est utilisé par défaut.

Les fichiers générés dans le répertoire choisi contiennent les données brutes et traitées des matchs de la NHL. Voici les fichiers clés:

1.  **nhl_game_data.json** : Contient les données brutes des matchs.
2.  **nhl_player_data.json** : Contient les noms des joueurs associés à leurs ID.
3.  **parsed_shot_events.csv** : Contient les données traitées relatives aux tirs.

Exemple d'initialisation:
```python
class NHLDataDownloader:
    def __init__(self, start_season, final_season, data_dir=None):
        self.start_season = start_season
        self.final_season = final_season
        
        #Points to the data folder
        root_directory = os.path.abspath(os.path.join(os.getcwd(), '..'))
        self.data_dir = data_dir if data_dir else os.path.join(root_directory, 'data')

        #Create directory if it doesn't already exist
        os.makedirs(self.data_dir, exist_ok=True)

        #File paths
        self.nhl_games_file_path = os.path.join(self.data_dir, 'nhl_game_data.json')
        self.nhl_players_file_path = os.path.join(self.data_dir, 'nhl_player_data.json')
        self.parsed_data_path = os.path.join(self.data_dir, 'parsed_shot_events.csv')
```

Dans cet exemple, vous pouvez initialiser une instance du téléchargeur de données comme suit :

```python
downloader = NHLDataDownloader(start_season=2016, final_season = 2023)
```

Cela configure la plage des saisons de 2016 à 2023 et sauvegardera les données dans le répertoire `data`. Si jamais ce repertoire n'existe pas, la méthode d'initialisation s'occupera de sa création.

## Récupération des données de jeu de la NHL
La méthode `get_nhl_game_data()` permet de récupérer les données brutes des matchs directement depuis l'API de la NHL. Elle effectue les étapes suivantes: 

1. **Construction de l'identifiant de match** : Chaque match NHL est identifié par un `gameId` unique, utilisé pour faire des requêtes à l'API de la NHL. Ce `gameId` est basé sur l'année de la saison et un numéro de match.

2. **Requête à l'API** : Pour chaque match, une requête HTTP est envoyée à l'API de la NHL pour récupérer les données d'évènements (par exemple, tirs, buts, pénalités, etc.).

3. **Sauvegarde des données brutes** : Les données sont stockées dans un dictionnaire (`all_data`), puis sauvegardées dans un fichier JSON (`nhl_game_data.json`), ce qui permet d'éviter une nouvelle requête lors des prochaines exécutions.

Exemple d'utilisation de la méthode `get_nhl_game_data()`

```python 
def get_nhl_game_data(self):
    all_data = {}
    for season in range(self.start_season, self.final_season + 1):
        # Code pour déterminer le nombre de matchs
        # ...
        for game_num in range(1, num_regular_season_games + 1):
            game_id = f'{season}02{game_num:04d}'
            url = f'https://api-web.nhle.com/v1/gamecenter/{game_id}/play-by-play'
            response = requests.get(url)
            game_data = response.json()
            all_data[game_id] = game_data
```

Vous pouvez l'appeler comme ceci:
```python
downloader.get_nhl_game_data()
```

Cela va télécharger et sauvegarder les données brutes de tous les matchs des saisons spécifiées dans le fichier `nhl_game_data.json`.

Cette méthode prend également en compte (en plus des parties de saison régulière) les parties des séries éliminatoires. Nous allons par le même processus bâtir le `gameId` de la partie en séries éliminatoires et faire une requête à l'API de la NHL pour acquérir les données brutes. 

```python
            # Playoff Games
            rounds = 4
            matchups_per_round = [8, 4, 2, 1]
            max_games_per_series = 7
            for round_num in range(1, rounds + 1):
                for matchup_num in range(1, matchups_per_round[round_num - 1] + 1):
                    for game_num in range(1, max_games_per_series + 1):
                        game_id = f'{season}030{round_num}{matchup_num}{game_num}'
                        url = f'https://api-web.nhle.com/v1/gamecenter/{game_id}/play-by-play'
                        print(f"Retrieving playoff data from '{url}'...")
                        response = requests.get(url)
                        if response.status_code == 200:
                            game_data = response.json()
                            all_data[game_id] = game_data
                        else:
                            print(f"No data found for playoff game {game_id}. Stopping the series.")
                            break
```

Avec ces étapes, vous avez un pipeline complet pour acquérir et traiter les données play-by-play de la NHL des saisons régulières et éliminatoires spécifiées, prêt à être utilisé pour des analyses plus approfondies.

# Outil de débogage interactif: Outil piwydget
Ceci est un outil efficace qui nous permet d'interagir avec les données en choisissant le match et les évènements d'un match d'une saison donnée.

On obtient alors une image de la patinoire montrant la position de l'évènement (démontré par un icône) avec une description de celui-ci et des informations supplémentaires telles que:
le score du match, les équipes qui se sont affrontées, la date du match ou encore la période où l'évènement s'est produit.

!["Widget interactif pour event de type Hit saison 2016-2017"](/assets/images/image.png)

Voici une brève description des différentes parties du code:
1. Gestion des données des joueurs:
    * Un dictionnaire global player_names est utilisé pour stocker les noms des joueurs déjà récupérés, afin de limiter les requêtes répétitives. Les noms des joueurs sont chargés depuis un fichier JSON `nhl_player_data.json` dans le cas de son existence.  

    * La fonction get_player_name() permet de rechercher le nom complet d'un joueur en fonction de son identifiant unique player_id. La fonction vérifie si le nom a déjà été récupéré pour éviter les appels redondants.

2. Description d'évènements:
    * Un dictionnaire `event_descriptions` permet de générer dynamiquement une description textuelle en fonction du type d'évènement (ex: un but, un tir bloqué, une pénalité, etc.).

    * Chaque type d'évènement a sa propre fonction lambda qui crée une phrase descriptive basée sur les joueurs impliqués. Par exemple, pour un but, cela indique quel joueur a marqué contre quel gardien.

3. Affichage des informations du match:
    * La fonction `get_game_info()` prend en entrée l'ID d'un match (`game_id`) et retourne les informations principales liées au match: les équipes en compétition, le score, les tirs au but (SoG), et l'heure du début du match.

    * Les informations sont formatées dans une table HTML afin d'être facilement affichées dans l'interface.

4. Affichage interactif avec widgets:
    * La dernière partie du code définit une interface avec des widgets via `VBox` (qui est un conteneur vertical pour afficher plusieurs widgets ensemble). Les widgets incluent un slider pour sélectionner l'ID du match et un autre pour ses évènements. Il y a aussi des labels pour afficher les informations du match et de l'évènement, ainsi qu'une image de la patinoire montrant la position de ces évènements.

    * La fonction `update_event_slider()` est appelée pour mettre à jour le slider des évènements en fonction des données du match sélectionné.

Gestion des données des joueurs:
```python 
player_names = {}  # Dictionnaire global pour stocker les noms des joueurs déjà récupérés
# Chargement des données des joueurs depuis nhl_player_data.json
player_file_path = os.path.join('..', 'data', 'nhl_player_data.json')
if os.path.exists(player_file_path):
        with open(player_file_path, 'r') as file:
            try:
                # Load the JSON file into the dictionary
                player_names = json.load(file)
                print(f"Loaded {len(player_names)} players from the file.")
            except json.JSONDecodeError as e:
                print(f"Error reading player data: {e}")
else:
    print(f"Player file {player_file_path} not found.")
    player_names = {}

def get_player_name(player_id: int) -> str:
    """Lookup player full name by ID from nhl_player_data."""
    # Vérifier si le nom est déjà dans le dictionnaire
    if player_id is None:
        return None

    # Vérifier si le joueur est déjà dans le dictionnaire
    if str(player_id) in player_names:
        return player_names[str(player_id)]
    
    # Effectuer une requête à l'API pour récupérer les informations du joueur
    url = f"https://api-web.nhle.com/v1/player/{player_id}/landing"
    try:
        response = requests.get(url)
        response.raise_for_status()  # Lève une erreur si la requête échoue
        player_data = response.json()
        
        # Extraire les noms du joueur (en accédant à la clé 'default')
        first_name = player_data.get('firstName', {}).get('default', 'Unknown')
        last_name = player_data.get('lastName', {}).get('default', 'Player')
        full_name = f"{first_name} {last_name}"

        # Stocker dans le dictionnaire pour éviter des appels répétés
        player_names[str(player_id)] = full_name
        
        return full_name

    except requests.RequestException as e:
        print(f"Error fetching player data: {e}")
        return "Unknown Player"
```
Description d'évènements:
```python
  # Créer une description basée sur le type d'événement
    event_descriptions = {
        "faceoff": lambda: f"{players['winning']} won a faceoff against {players['losing']}.",
        "goal": lambda: f"{players['shooting']} scored a goal against {players['goalie']}.",
        "shot-on-goal": lambda: f"{players['shooting']} took a shot on goal saved by {players['goalie']}.",
        "giveaway": lambda: f"{players['giveaway']} gave the puck away.",
        "period-start": lambda: "The period has started.",
        "blocked-shot": lambda: f"{players['blocking']} blocked a shot from {players['blocked']}.",
        "delayed-penalty": lambda: "A delayed penalty was called.",
        "failed-shot-attempt": lambda: f"{players['shooting']} attempted a shot but missed the net.",
        "shootout-complete": lambda: "The shootout has ended.",
        "stoppage": lambda: "The game was stopped.",
        "penalty": lambda: f"Penalty: {players['penalized']} committed a foul against {players['penalty']}.",
        "takeaway": lambda: f"{players['giveaway']} took the puck away.",
        "missed-shot": lambda: f"{players['shooting']} missed the net with a shot.",
        "game-end": lambda: "The game has ended.",
        "hit": lambda: f"{players['hitting']} delivered a hit on {players['hit']}.",
        "period-end": lambda: "The period has ended."
    }
```

Affichage des informations du match:
```python
def get_game_info(self, game_id):
        """Retourne les informations du match (Game ID, équipes, score, etc.)."""
        game_data = self.filtered_games.get(game_id)
        if not game_data:
            return "Données du match indisponibles"
        
        home_team = game_data['homeTeam']['name']['default']
        away_team = game_data['awayTeam']['name']['default']
        home_score = game_data['homeTeam']['score']
        away_score = game_data['awayTeam']['score']
        game_starting_time = game_data['startTimeUTC']
        home_sog = game_data['homeTeam']['sog']
        away_sog = game_data['awayTeam']['sog']

        formatted_info = f"""
        <p><b>{game_starting_time}</b></p>
        <p><b>Game ID: {game_id}; {home_team} (home) vs {away_team} (away)</b></p>
        <p><b>{game_data['periodDescriptor']['periodType']}</b></p>
        <table style="width:50%; text-align: left; border-collapse: collapse;">
           <tr>
               <th></th>
               <th style="text-align: center;">Home</th>
               <th style="text-align: center;">Away</th>
           </tr>
           <tr>
               <td><b>Teams:</b></td>
               <td style="text-align: center;">{home_team}</td>
               <td style="text-align: center;">{away_team}</td>
           </tr>
           <tr>
               <td><b>Goals:</b></td>
               <td style="text-align: center;">{home_score}</td>
               <td style="text-align: center;">{away_score}</td>
           </tr>
           <tr>
               <td><b>SoG:</b></td>
               <td style="text-align: center;">{home_sog}</td>
               <td style="text-align: center;">{away_sog}</td>
           </tr>
       </table>
       """
        return formatted_info
```

Affichage interactif avec widgets:
```python
# Conteneur pour afficher les widgets
vbox = widgets.VBox([
    game_id_slider,
    game_info_label,
    event_slider,
    even_description_label,
    rink_display_label,
    event_info_label
    
])
display(vbox)
# Initialiser l'affichage
update_event_slider()
```

En résume, ce code permet de naviguer et d'afficher les informations d'un match de hockey et ses évènements de manière visuelle et interactive.


# Nettoyage des données 
Le traitement des données brutes est un aspect essentiel de l’analyse, et cela se fait dans la méthode `parse_nhl_game_data()` de la classe `NHLDataDownloader`. Voici les étapes principales que cette méthode suit pour extraire et organiser les données relatives aux tirs dans les matchs de la NHL :


1. Vérification de l'existence des données traitées:
    * Avant de retraiter les données, la méthode vérifie si un fichier CSV contenant les évènements de tir a déjà été généré. Si ce fichier existe (`parsed_shot_events.csv`), il est directement chargé via `pd.read_csv()` pour éviter un retraitement iniutile des mêmes données.

2. Chargement des donées brutes:
    * Si les données n'ont pas encore été traitées, elles sont chargées depuis un fichier JSON (`nhl_game_data.json`), qui contient les détails bruts des matchs de la NHL. Ces données comprennent tous les évènements survenus lors des matchs.

3. Filtrage des évènements liés aux tirs
    * La méthode parcourt les évènements de chaque match en identifiant ceux liés aux tirs (types 505 pour les buts et 506 pour les shots on goal). Pour chaque tir, les détails importants, tels que l'identité du tireur, du gardien, la période du match, le type de tir, la situation de jeu (comme les avantages numériques), et les coordonnées dur tir sur la patinoire sont extraits et stockés dans un dictionnaire.

4. Gestion des données des joueurs
    * Pour enrichir les données, les identifiants des joueurs (tireurs et gardiens) sont convertis en noms complets via la fonction `get_player_name()`. Cette fonction comme dans la section précédente, évite les appels redondants à l'API de la NHL en vérifiant si le nom du joueur a déjà été récupéré ou est stocké localement dans un fichier JSON (`nhl_player_data.json`)

5. Création d'un DataFrame Pandas:
    * Une liste d'évènements de tir est accumulée pour chaque match. Cest évènements sont ensuite convertis en un DataFrame Pandas individuel pour chaque match. Ces DataFrames sont concaténés en un seul DataFrame global (`all_shot_events_df`), qui contient les évènements de tir de tous les matchs analysés.

6. Sauvegarde des données traitées:
    * Une fois tous les évènements extraits et organisés dans le DataFrame, les données sont sauvegardées dans un fichier CSV (`parsed_shot_events.csv`). Cela Permet d'éviter de refaire le traitement lors des exécutions futures.
    * Une méthode qui se nomme `save_player_names()` peut être appelé dans le cas que nous voulons sauvegardé les noms des joueurs qu'on a utilisés dans un fichier json (`nhl_player_data.json`)

``` python
    def parse_nhl_game_data(self):
        """
        Parses the NHL game data from a JSON file and filters for shot-related events.

        Returns:
            pd.DataFrame: A DataFrame containing shot-related events for all games.
        """

        if os.path.exists(self.parsed_data_path):
            print(f"Loading parsed data from {self.parsed_data_path}...")
            return pd.read_csv(self.parsed_data_path)
        
        all_shot_events_df = pd.DataFrame()
        
        with open(self.nhl_games_file_path, 'r') as json_file:
            game_data = json.load(json_file)

        # Parsing data
        for game_id, game_details in game_data.items():
            print(f"Parsing game {game_id}")
            all_plays = game_details.get('plays', [])
            shot_events = []

            for play in all_plays:
                event_type = play.get('typeCode')
                if event_type in [505, 506]:
                    shooter_id = play.get('details', {}).get('scoringPlayerId') if event_type == 505 else play.get('details', {}).get('shootingPlayerId')
                    goalie_id = play.get('details', {}).get('goalieInNetId')
                    situation_code = play.get('situationCode')
                    shot_details = {
                        'season': game_details.get('season'),
                        'gameId': game_id,
                        'eventId': play.get('eventId'),
                        'period': play.get('periodDescriptor', {}).get('number'),
                        'timeInPeriod': play.get('timeInPeriod'),
                        'eventType': play.get('typeDescKey'),
                        'teamId': play.get('details', {}).get('eventOwnerTeamId'),
                        'shooter': self.get_player_name(shooter_id),
                        'goalie': self.get_player_name(goalie_id),
                        'shotType': play.get('details', {}).get('shotType'),
                        'emptyNetAway': False if int(situation_code[0]) == 1 else True,
                        'emptyNetHome': False if int(situation_code[3]) == 1 else True,
                        'powerplayHome': True if int(situation_code[2]) > int(situation_code[1]) else False,
                        'powerplayAway': True if int(situation_code[1]) > int(situation_code[2]) else False,
                        'coordinates': (play.get('details', {}).get('xCoord'), play.get('details', {}).get('yCoord')),
                        'result': 'goal' if event_type == 505 else 'no goal'
                    }
                    shot_events.append(shot_details)

            if shot_events:
                shot_events_df = pd.DataFrame(shot_events)
                all_shot_events_df = pd.concat([all_shot_events_df, shot_events_df], ignore_index=True)

        all_shot_events_df.to_csv(self.parsed_data_path, index=False)
        print(f"Parsed data saved to {self.parsed_data_path}")
        return all_shot_events_df
```

## Extrait du DataFrame
!["df.head(10)"](/assets/images/df1.jpg)

## Discussion sur la force réelle
Si nous n'avions pas accès au données de la force réelle pour les tirs et les buts, voici comment notre équipe procéderait pour les recréer. 

Tout d'abord nous utiliserions les évènements relatifs aux pénalités. Lorsque'une pénalité est enregistrée, elle modifie la force des équipes (par exemple, un avantage numérique de 5 contre 4). Voici un exemple d'évènement de pénalité dans les données:

```
                "eventId": 47,
                "periodDescriptor": {
                    "number": 1,
                    "periodType": "REG",
                    "maxRegulationPeriods": 3
                },
                "timeInPeriod": "13:25",
                "timeRemaining": "06:35",
                "situationCode": "1551",
                "typeCode": 509,
                "typeDescKey": "penalty",
                "sortOrder": 161,
                "details": {
                    "xCoord": -90,
                    "yCoord": -12,
                    "zoneCode": "D",
                    "typeCode": "MAJ",
                    "descKey": "fighting",
                    "duration": 5,
                    "committedByPlayerId": 8474697,
                    "drawnByPlayerId": 8474709,
                    "eventOwnerTeamId": 9
                }
            },
```

Étapes pour calculer la force des équipes à partir des évènements de pénalité

1. **Identifier le type de pénalités**: Les événements de pénalité incluent un champ `typeCode` et une clé `descKey` qui décrivent le type de pénalité. Dans cet exemple, la pénalité est une "fighting" (avec `descKey: "fighting"`) et a une durée de 5 minutes (`duration: 5`). Chaque type de pénalité a une durée prédéfinie, et cela impacte la force de l'équipe pénalisée pendant cette période.


2. **Suivre le nombre de joueurs sur la glace**: Lorsqu'une pénalité est infligée, elle réduit le nombre de joueurs sur la glace pour l'équipe pénalisée. Il est nécessaire de maintenir un compteur qui suit le nombre de joueurs pour chaque équipe. Par exemple, si une équipe reçoit une pénalité mineure de 2 minutes, elle passe de 5 à 4 joueurs pendant la durée de la pénalité. Dans certains cas, la pénalité peut se terminer plus tôt si l'équipe en avantage numérique marque un but. Avec la durée de la pénalité et le moment précis où elle a été infligée, nous pouvons facilement prendre en compte ces facteurs.

3. **Mise à jour dynamique de la force des équipes**: Au fur et à mesure que les événements de jeu (tirs, buts, etc.) surviennent pendant la durée de la pénalité, nous ajustons la force des équipes en fonction de la pénalité en cours. Cela permet de connaître la force exacte des équipes au moment de chaque événement. Nous gérons également les situations où plusieurs pénalités peuvent se produire simultanément. Notre système tiendra compte de toutes ces situations. Une structure de données contenant les temps de fin de chaque pénalité nous permettra de mettre à jour le nombre de joueurs de chaque équipe lorsque la pénalité se termine.



## Caractéristiques supplémentaires
 
1. **Rebond**: Un tir peut être classé comme un "rebond" si un autre tir a eu lieu juste avant et a été arrêté ou dévié sans que le jeu n'ait été interrompu. Pour identifier un rebond, nous pourrions vérifier si un tir survient dans un court laps de temps (par exemple, dans les 5 secondes) après un autre tir de la même équipe. Si ces conditions sont remplies, le deuxième tir pourrait être classé comme un rebond.

2. **Tir en contre-attaque** : Un tir en contre-attaque se produit généralement juste après que l'équipe adverse ait perdu la possession de la rondelle. Pour l'identifier, nous pourrions examiner les événements de récupération de la rondelle ou d'interception par une équipe et vérifier si un tir est effectué rapidement après cette récupération (par exemple, dans les 10 secondes suivant le changement de possession). Si tel est le cas, le tir pourrait être classé comme une contre-attaque.

3. **Angle de tir**: En utilisant les coordonnées du tir, nous pourrions calculer l'angle entre la ligne de but et le tireur pour identifier les tirs réalisés sous un angle difficile. Ces tirs, bien qu’ayant un taux de réussite plus faible, peuvent être analysés pour déterminer si certains joueurs ou équipes réussissent mieux dans ces situations.

    L'angle peut être calculé en utilisant l'arrctangeante: 

    `angle = arctan(yCoord / abs(x_goal - xCoord))`

4. **Distance du tir par rapport au but**: En utilisant les coordonnées du tir (`xCoord` et `yCoord`) nous pourrions calculer la distance entre la position du tireur et le but en utilisant la distance euclidienne:

    `distance = sqrt((x_goal - xCoord)^2 + (y_goal - yCoord)^2)`



# Visualisations Simples

## 1. Comparaison des types de tirs

Nous commençons par comparer la fréquence des différents types de tirs, en visualisant à la fois le nombre total de tirs et le nombre de buts marqués pour chaque type de tir. Pour ce faire, nous avons décidé de représenter cela dans un histogramme en barres où les tirs sont mis à côté des buts marqués.

!["Nombre de tirs et de buts par type de tir 2022-2023"](/assets/images/Bar_typetirbut.jpg)
Le graphe ne nous aide pas vraiment à cause de la disparité dans les valeurs des données tirs/buts. Nous séparons donc cela en 2 sous-figures et ajoutons également le pourcentage de buts marqués :
!["Nombre de tirs et de buts par type de tir et pourcentage 2022-2023"](/assets/images/stackedshottype.png)
De ce graphe, nous observons:
* `Tir le plus dangereux` : Le tir "cradle" a le pourcentage de réussite le plus élevé, bien qu'il soit le moins utilisé.

* `Tir le plus commun` : Le tir "wrist" est de loin le plus courant, comme le montre le nombre d'essais par rapport aux autres types de tirs. Cependant, son pourcentage de réussite n'est pas aussi élevé que celui d'autres tirs moins courants, comme le "bat" ou le "tip in".

## Analyse de la relation entre la distance des tirs et les chances de but
Nous avons choisi de répondre à la question 2 à l'aide d'un graphique en courbes avec la distance en abscisse et le taux de probabilité de but en ordonnée.

* Taux de Buts en Fonction de la Distance au But par Saison (2018-2019):
!["Taux de Buts en Fonction de la Distance au But par Saison (2018-2019)"](/assets/images/Tauxdebutdistance2018.png)
* Taux de Buts en Fonction de la Distance au But par Saison (2019-2020):
!["Taux de Buts en Fonction de la Distance au But par Saison (2019-2020)"](/assets/images/Tauxdebutdistance2019.png)
* Taux de Buts en Fonction de la Distance au But par Saison (2020-2021):
!["Taux de Buts en Fonction de la Distance au But par Saison (2020-2021)"](/assets/images/Tauxdebutdistance2020.png)
Nous avons également décidé de tracer les trois saisons sur le même graphique pour mieux observer les variations entre elles. Cela montre clairement qu'il existe une relation inverse entre la distance et le taux de réussite d'un but. Plus un tir est proche du but, moins le gardien a de temps pour réagir, ce qui augmente la probabilité de marquer.
!["Taux de Buts en Fonction de la Distance au But par Saison (2018-2021)"](/assets/images/Tauxdebutdistance.jpg)
De ce graphe, nous observons:
* La probabilité de marquer un but selon la distance est plutôt stable par saison.
* Une augmentation du taux de but à la distance [80,90] à la saison 2020-2021.
* La probabilité de marquer à la distance [0,10] à la saison 2018-2019 est plus basse comparé aux autres saisons.

## Visualisation du Pourcentage de Buts en Fonction de la Distance et des Types de Tirs
Pour répondre à cette question, nous avons décidé de représenter la relation entre la distance, le type de tir et le taux de réussite d'un but par une heatmap.
![" Pourcentage de Buts en Fonction de la Distance et des Types de Tirs 2022-2023"](/assets/images/Heatmap_final.png)
Nous pouvons observer:
* Le "cradle" est le type de tir le plus dangereux entre [0,10], suivi par le "bat".
* De 0 à 30, les tirs "snaps" et "slaps" sont les plus dangereux.
* À une distance de 30 à 50, le "poke" est le plus dangereux avec un taux de réussite de 25-40%.
* Le "wrap around" est de loin le pire tir.

# Visualisations Complexes
Un extrait du code pour le calcul du nombre de tirs par heure de la ligue pour toutes les saisons entre 2016 et 2020 :


``` python

    for year in range(start_year, end_year + 1):
        # Create a dict object for each year. Each such dict object is a dict of teams containing their individual xy
        # shot frequencies
        shot_freq_per_team_per_season[str(year)] = {}
        league_avg = league_shot_avg(df, year)
        for team in teams_per_season[str(year)]:
            team_avg = team_shot_avg(df, year, team)
            avg_difference = team_avg - league_avg
            # smoothing results
            test_total_filter = gaussian_filter(avg_difference, sigma=sigma)

            # Filter out values that are very close to zero for plotting purposes
            test_total_filter[np.abs(test_total_filter - 0) <= threshold] = None

            # Store result
            shot_freq_per_team_per_season[str(year)][team] = test_total_filter

```

## Exportation des 5 graphiques de la zone offensive pour les Florida panthers
<b>Shot Maps pour la saison 2016-2017</b><br>
{% include NHL_plot2016-2017.html %}
<b>Shot Maps pour la saison 2017-2018</b><br>
{% include NHL_plot2017-2018.html %}
<b>Shot Maps pour la saison 2018-2019</b><br>
{% include NHL_plot2018-2019.html %} 
<b>Shot Maps pour la saison 2020-2021</b><br>
{% include NHL_plot2020-2021.html %}
<!--
!["Profil de tir Florida panthers 2016"](/assets/images/Panthers_2016.png)
!["Profil de tir Florida panthers 2017"](/assets/images/Panthers_2017.png)
!["Profil de tir Florida panthers 2018"](/assets/images/Panthers_2018.png)
!["Profil de tir Florida panthers 2019"](/assets/images/Panthers_2019.png)
!["Profil de tir Florida panthers 2020"](/assets/images/Panthers_2020.png)-->
Nous avons également ajouté l'année en option pour naviguer plus facilement entre les saisons:
{% include NHL_plot2016-2021.html %}
## Discussion
Ces graphiques montrent le profil de tir d'une équipe sur une saison donnée.
De ces graphiques, on peut observer les zones du terrain dans lesquelles une équipe a tiré plus (ou moins) que la moyenne de la ligue et également observer à quel point cette différence est marquée. Cela peut nous permettre d'avoir une idée des performances de cette équipe sur la saison. Dans le cas particulier des Florida Panthers, on voit que pour les saisons 2017-2018 et 2018-2019, ils ont tiré bien au-dessus de la moyenne dans des zones proches du but. De cela, on peut penser qu'ils ont été bien classés lors de ces 2 saisons.
    
## Analyse de l’équipe Colorado Avalanche, comparaison des cartes de tirs entre 2016-2017 et 2020-2021
Lors de la saison 2016-2017, l'équipe des Colorado Avalanche affiche un taux de tirs relativement faible devant le filet (à 10-20 pieds du but) comparé à la moyenne de la ligue à la même position. En revanche, pendant la saison 2020-2021, on observe une augmentation du taux de tirs près du filet, ce qui pourrait expliquer leur montée dans le classement entre 2016 et 2020.
!["Profil de tir Avalanche 2016"](/assets/images/Avalanche_2016.png)

!["Profil de tir Avalanche 2020"](/assets/images/Avalanche_2020.png)


## Comparaison entre Buffalo Sabres et Tampa Bay Lightning, basée sur leurs cartes de tirs
Le profil de tir des Buffalo Sabres pour les saisons 2018 à 2020 montre qu'ils n'ont pas beaucoup tiré au but lors de ces saisons comparativement à Tampa Bay, car la quasi-totalité des zones dans lesquelles ils ont tiré est en dessous de la moyenne des tirs de la ligue sur ces saisons, et d'avantage dans les zones proches du but. À l'inverse, Tampa Bay a énormément tiré au but sur ces saisons, surtout dans des zones proches du buts.
!["Profil de tir Buffalo Sabres 2018"](/assets/images/Sabres_2018.png)
!["Profil de tir tampa bay 2018"](/assets/images/Bay_2018.png)

!["Profil de tir Buffalo Sabres 2019"](/assets/images/Sabres_2019.png)
!["Profil de tir tampa bay 2019"](/assets/images/Bay_2019.png)

!["Profil de tir Buffalo Sabres 2020"](/assets/images/Sabres_2020.png)
!["Profil de tir tampa bay 2020"](/assets/images/Bay_2020.png)

Bien que ces profils de tir donnent une bonne perspective sur les performances d'une équipe, ils ne sont toutefois pas suffisants pour comprendre totalement les raisons du succès ou de l'échec d'une équipe. D'autres facteurs tels que l'identité du tireur, les zones de tir préférentielles d'une équipe, ou encore le fait que certaines équipes performent mieux à domicile qu'à l'extérieur sont d'autres paramètres qu'il faut prendre en compte pour comprendre le succès ou l'échec d'une équipe.
