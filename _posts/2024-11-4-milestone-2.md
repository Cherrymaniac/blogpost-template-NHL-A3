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

# Ingénierie des Caractéristiques II

Le code intègre déjà plusieurs caractéristiques pertinenntes issues des donnéees dispoinibles. En effet celui-ci peut se retrouver dans le fichier ```feature_engineering.py``` sous l'onglet ```src``` de notre repository.

**Caractéristiques à inclure à partir des données existantes: **

Commençons d'abord avec des caractéristiques de base.

1. Secondes de jeu (Game seconds):
  - **Colonne créée** : ```gameSeconds```
  - **Explication** : Nombre total de secondes écoulées dans le match depuis le début, calculé à partir de la période et de l’heure de l’événement avec la fonction ```add_game_seconds()```.
  - **Code** : 
     ```python
    def add_game_seconds(self):
        """
        Adds a column to the DataFrame representing the total game seconds elapsed from the start of the game to the current event.
        """
        def calculate_game_seconds(row):
            try:
                # Extract minutes and seconds from the timeInPeriod
                minutes, seconds = map(int, row['timeInPeriod'].split(":"))
                time_elapsed = minutes * 60 + seconds
                # Add the time for completed periods before the current one
                total_seconds = (row['period'] - 1) * 1200 + time_elapsed  #20-minute periods (1200 seconds)
                return total_seconds
            except ValueError:
                return None 
      ```
2. Période de jeu (Game period) :
  - **Colonne existante** : ```period```
  - **Explication** : Numéro de la période dans laquelle l’événement a eu lieu.

3. Coordonnées (x, y): 
  - **Colonnes créées** : ```xCoord``` et  ```yCoord```
  - **Explication** : Coordonnées exactes du tir sur la glace, extraites des données brutes par ```calculate_shot_distance_and_angle()```

4. Distance du tir (Shot distance) :
  - **Colonne créée** : ```shotDistance```
  - **Explication** : Distance euclidienne en mètres entre la position du tir et le filet, calculée dans ```calculate_shot_distance_and_angle()```

5. Type de tir (Shot type) :
  - **Colonne existante** : ```shotType```
  - **Explication** : Type de tir qui a été effectué (wrist-shot, back-hand, slap-shot, etc...)

6. Angle du tir (Shot angle) :
  - **Colonne créée** : ```shotAngle```
  - **Explication** : Angle du tir par rapport à la ligne centrale du filet, calculé dans ```calculate_shot_distance_and_angle()```. Le schéma ci-dessous démontre la manière dont nos angles de tirs sont représentés pour les deux côtés de la patinoire.

  ![Angle Schema](/assets/images/milestone2/shot_angle_schema.png)

  - **Code** :
    ```python
          def calculate_shot_distance_and_angle(self):
          """
          Calculates the Euclidean distance of each shot from the net based on the offensive side,
          accounting for shots originating from different zones (offensive, neutral, defensive).
          """
          def get_distance_and_angle(row):
              try:
                  stripped = row['coordinates'].strip("()")
                  x_str, y_str = stripped.split(",")
                  x_shot, y_shot = int(x_str), int(y_str)
              #Missing values are handled by returning None
              except ValueError:
                  return None, None
              
              # Determine net coordinates based on offensive side of the team shooting
              if row['offensiveSide'] == 'right':
                  x_net, y_net = 89, 0
              elif row['offensiveSide'] == 'left':
                  x_net, y_net = -89, 0
              else:
                  return None, None  # Unknown side

              # Calculate Euclidean distance
              if (row['offensiveSide'] == 'right' and x_shot < 0) or (row['offensiveSide'] == 'left' and x_shot > 0):
                  #If the shot is in neutral or defensive zone for example
                  distance = math.sqrt((abs(x_shot) + abs(x_net))**2 + y_shot**2)

              else:
                  distance = math.sqrt((x_shot - x_net)**2 + (y_shot)**2)
              
              #Neglect shots behind net
              if x_shot > 89 or x_shot < -89:
                  return distance, None
              # Calculate the angle of the shot relative to y = 0 (centerline)
              angle = math.degrees(math.atan2(y_shot, abs(x_net - x_shot)))

              # Adjust the sign of the angle based on the side
              if row['offensiveSide'] == 'right':
                  angle = -angle  # Reverse the angle sign for left offensive side

              return x_shot, y_shot, distance, angle

          # Apply the function to each row and create a new column 'shotDistance'
          self.df[['xCoord', 'yCoord', 'shotDistance', 'shotAngle']] = self.df.apply(lambda row: pd.Series(get_distance_and_angle(row)), axis=1)
    ```

**Ajout des informations sur l’événement précédent: **

Le code inclut aussi des méthodes dédiées pour enrichir chaque évènement avec des informations sur l'évènement précédent. 

1. Dernier type d'événement (Last event type) :
  - **Colonne créée**: ```lastEventType```
  - **Explication**: Type de l’événement précédent (ex. tir, mise en jeu), calculé dans ```add_previous_event_features()```
2. Coordonnées du dernier événement (x, y) :
  - **Colonne créée**: ```lastEventXCoord``` et ```lastEventYCoord```
  - **Explication**: Coordonnées de l’événement précédent, extraites des données de jeu, calculé dans ```add_previous_event_features()```
3. Temps écoulé depuis le dernier événement (Time elapsed since last event) :
  - **Colonne créée**: ```timeElapsedSinceLastEvent```
  - **Explication**: Temps écoulé en secondes entre l’événement précédent et l’événement courant. Ceci est calculé dans ```add_previous_event_features()```
4. Distance depuis le dernier événement (Distance from the last event) :
  - **Colonne créée**: ```distanceFromLastEvent```
  - **Explication**: Distance euclidienne en mètres entre les coordonnées de l’événement précédent et celles de l’événement actuel. Ceci est calculé dans ```add_previous_event_features()```
  - **Code**:
      ```python
        def add_previous_event_features(self):
            """
            Adds information about the previous event for each shot, including:
            - Last event type
            - Coordinates of the last event (x, y)
            - Time elapsed since the last event (seconds)
            - Distance from the last event
            """

            # Pre-fetch game data for all unique game IDs in the DataFrame
            unique_game_ids = self.df['gameId'].unique()
            game_data_cache = {game_id: self.game_data.get(str(game_id), {}).get('plays', []) for game_id in unique_game_ids}

            last_event_types = []
            last_event_x_coords = []
            last_event_y_coords = []
            time_elapsed_list = []
            distance_from_last_event = []

            for _, row in self.df.iterrows():
                game_id = str(row['gameId'])
                event_id = row['eventId']
                current_time = row['timeInPeriod']
                x_coord = row['xCoord']
                y_coord = row['yCoord']

                # Initialize defaults
                last_event_type = None
                last_x = None
                last_y = None
                elapsed_time = None
                distance = None

                # Fetch plays for the current game from the cache
                all_plays = game_data_cache.get(game_id, [])    

                # Find the index of the current event in all_plays, with additional criteria for unique identification
                current_index = next(
                    (i for i, play in enumerate(all_plays)
                    if play.get('eventId') == event_id
                    and play.get('timeInPeriod') == current_time
                    and (play.get('details', {}).get('xCoord'), play.get('details', {}).get('yCoord')) == (x_coord, y_coord)),
                    None
                )

                # Null check for current_index
                if current_index is not None:
                    if current_index > 0:
                        prev_event = all_plays[current_index - 1]
                        prev_time = prev_event.get('timeInPeriod')
                        prev_period = prev_event.get('periodDescriptor', {}).get('number')

                        #Ensure previous event is from the same period
                        if prev_period is not None and prev_period == row['period']:  
                            last_event_type = prev_event.get('typeDescKey')
                            last_x = prev_event.get('details', {}).get('xCoord')
                            last_y = prev_event.get('details', {}).get('yCoord')
                        
                            #Calculate time elapsed
                            if prev_time and current_time:
                                try:
                                    curr_minutes, curr_seconds = map(int, current_time.split(":"))
                                    prev_minutes, prev_seconds = map(int, prev_time.split(":"))
                                    elapsed_time = (curr_minutes * 60 + curr_seconds) - (prev_minutes * 60 + prev_seconds)
                                except ValueError:
                                    elapsed_time = None

                            # Calculate distance from the last event
                            try:
                                last_x = int(last_x) if last_x is not None else None
                                last_y = int(last_y) if last_y is not None else None
                                if last_x is not None and last_y is not None:
                                    distance = math.sqrt((x_coord - last_x)**2 + (y_coord - last_y)**2)
                            except (ValueError, TypeError):
                                distance = None  
                        else: 
                            # If the previous event is from a different period, set default values
                            last_event_type = "Start of period"
                            last_x = None
                            last_y = None
                            elapsed_time = 0
                            distance = 0
                    else:
                        # If this is the first event of the game or period, set default values
                        last_event_type = "Start of game"
                        last_x = None
                        last_y = None
                        elapsed_time = 0
                        distance = 0
                # Append results to lists
                last_event_types.append(last_event_type)
                last_event_x_coords.append(last_x)
                last_event_y_coords.append(last_y)
                time_elapsed_list.append(elapsed_time)
                distance_from_last_event.append(distance)


            # Add the new columns to the DataFrame
            self.df['lastEventType'] = last_event_types
            self.df['lastEventXCoord'] = last_event_x_coords
            self.df['lastEventYCoord'] = last_event_y_coords
            self.df['timeElapsedSinceLastEvent'] = time_elapsed_list
            self.df['distanceFromLastEvent'] = distance_from_last_event
        ```

**Caractéristiques supplémentaires:**

Trois nouvelles caractéristiques basées sur l'état du jeu et les événements précédents sont également calculées :

1. Rebond (Rebound):
  - **Colonne créée**: ```rebound```
  - **Explication**: Indique si l’événement précédent était un tir, ce qui pourrait signaler un rebond, calculé dans ```previous_event_analysis()```

2. Changement d'angle du tir (Change in shot angle) :
  - **Colonne créée**: ```changeInShotAngle```
  - **Explication**: Différence entre l’angle du tir actuel et celui du tir précédent (ceci est calculé uniquement pour les rebonds). Ceci est calculé dans la méthode ```previous_event_analysis()```.

3. Vitesse (Speed):
  - **Colonne créée** : speed
  - **Explication**: Vitesse en mètres par seconde depuis le dernier évènement. Distance parcourue entre l’événement précédent et l’événement actuel, divisée par le temps écoulé. Ceci est aussi calculé dans la méthode ```previous_event_analysis()```.
  - **Code**:
      ```python
        def previous_event_analysis(self):
            """
            Adds three new features to the DataFrame:
            - Rebound (bool): True if the last event was also a shot, otherwise False.
            - Change in shot angle: The change in shot angle relative to the previous shot, only calculated for rebounds.
            - Speed ('vitesse'): The distance from the previous event divided by the time elapsed since the previous event.
            """
            rebounds = []
            shot_angle_changes = []
            speeds = []

            for idx, row in self.df.iterrows():
                # Initialize default values
                rebound = False
                shot_angle_change = None
                speed = None
                last_angle = 0

                # Determine if the last event was a shot (rebound)
                last_event_type = row['lastEventType']
                if last_event_type == 'shot-on-goal':
                    rebound = True

                    # Calculate change in shot angle
                    if pd.notnull(row['lastEventXCoord']) and pd.notnull(row['lastEventYCoord']) and pd.notnull(row['shotAngle']):
                        try:
                            # Calculate the angle of the previous shot relative to the net
                            if row['offensiveSide'] == 'right':
                                x_net, y_net = 89, 0
                            elif row['offensiveSide'] == 'left':
                                x_net, y_net = -89, 0
                            else:
                                last_angle = None

                            if last_angle is not None:
                                last_angle = math.degrees(math.atan2(row['lastEventYCoord'], abs(x_net - row['lastEventXCoord'])))
                                # Adjust the sign of the angle based on the side
                                if row['offensiveSide'] == 'right':
                                    last_angle = -last_angle  # Reverse the angle sign for left offensive side

                                shot_angle_change = abs(row['shotAngle'] - last_angle)

                        except (ValueError, TypeError):
                            shot_angle_change = None

                # Calculate speed if time elapsed is available          
                if pd.notnull(row['timeElapsedSinceLastEvent']) and row['timeElapsedSinceLastEvent'] > 0:
                    if pd.notnull(row['distanceFromLastEvent']):
                        speed = row['distanceFromLastEvent'] / row['timeElapsedSinceLastEvent']  


                # Append calculated values to lists
                rebounds.append(rebound)
                shot_angle_changes.append(shot_angle_change)
                speeds.append(speed)
            
            # Add the new columns to the DataFrame
            self.df['rebound'] = rebounds
            self.df['changeInShotAngle'] = shot_angle_changes
            self.df['speed'] = speeds   
        ```

**Création de caractéristiques personnalisées**:

Nous avons aussi créé des caractéristiques personalisées pour nous aider dans notre traitement de données.

1. Home or Away: 
  - **Colonne créée**: ```HomeVsAway```
  - **Explication**: Le statut Home or Away de l'èquipe en train d'effectuer le tir.

2. Home Team Id et Away Team Id:
  - **Colonne créée**: ```homeTeamId``` et ```awayTeamId```
  - **Explication**: Les identifiants de l'équipe Home et Away pour la joute actuelle.
  - **Code**: 
      ```python 
        def add_team_ids(self):
          """
          Adds home and away team IDs to the DataFrame by extracting them from the game data JSON file.
          """
          home_ids = []
          away_ids = []
          self.df['gameId'] = self.df['gameId'].astype(str)
          
          for _, row in self.df.iterrows():
              game_id = row['gameId']
              game_details = self.game_data.get(game_id, {})
              home_team_id = game_details.get('homeTeam', {}).get('id')
              away_team_id = game_details.get('awayTeam', {}).get('id')
              
              # Append team IDs or None if not available
              home_ids.append(int(home_team_id) if home_team_id is not None else None)
              away_ids.append(int(away_team_id) if away_team_id is not None else None)

          # Add the home and away team IDs as new columns in the DataFrame
          self.df['homeTeamId'] = home_ids
          self.df['awayTeamId'] = away_ids

          # Ensure columns are of integer type, fill NaN with a default value if necessary
          self.df['homeTeamId'] = self.df['homeTeamId'].fillna(0).astype(int)
          self.df['awayTeamId'] = self.df['awayTeamId'].fillna(0).astype(int)
      ```

3. But sur filet vide (Empty Net Goal):
  - **Colonne créée**: ```emptyNetGoal```
  - **Explication**: Détermine si le but a été marqué sur un filet vide.
  - **Code**:
      ```python 
        def add_empty_net_goal_column(self):
          """
          Adds a column to the DataFrame indicating if a goal was scored on an empty net.
          """
          def is_empty_net_goal(row):
              if row['eventType'] == 'goal':  # Check if the event is a goal
                  if row['emptyNetHome'] and row['teamId'] != row['homeTeamId']:
                      # Goal scored against home team (home net is empty)
                      return 1
                  elif row['emptyNetAway'] and row['teamId'] != row['awayTeamId']:
                      # Goal scored against away team (away net is empty)
                      return 1
              return 0

          # Apply the function to each row and create a new column 'emptyNetGoal'
          self.df['emptyNetGoal'] = self.df.apply(is_empty_net_goal, axis=1)
      ```

4. Côté Offensive (Offensive Side):
  - **Colonne créée**: ```offensiveSide```
  - **Explication**: Côté offensif (droite ou gauche) de l'équipe en train de tirer.
  - **Code**:
      ```python 
        def determine_offensive_side(self):
          """
          Determines the offensive side (left or right) for the home and away teams based on the first non-neutral
          shot of the first period, considering which team took the shot.
          """
          # Limit to the first 5 unique games for testing
          all_game_ids = self.df['gameId'].unique()

          for game_id in all_game_ids:
              game_shots = self.df[self.df['gameId'] == game_id]
              home_team_side = 'unknown'
              away_team_side = 'unknown'

              # Fetch the first non-neutral shot from the first period
              for _, shot in game_shots.iterrows():
                  if shot['period'] == 1:
                      # Fetch play details from game data
                      game_details = self.game_data.get(str(game_id), {})
                      all_plays = game_details.get('plays', [])
                      play = next((p for p in all_plays if p.get('eventId') == shot['eventId']), None)

                      if play:
                          zone_code = play.get('details', {}).get('zoneCode')
                          x_coord = play.get('details', {}).get('xCoord')
                          shooting_team_id = shot['teamId']

                          if zone_code and zone_code != 'N' and x_coord is not None:
                              # Determine sides based on which team is shooting
                              if shooting_team_id == shot['homeTeamId']:
                                  # Home team shot
                                  if x_coord < 0 and zone_code == 'D':
                                      home_team_side = 'right'
                                      away_team_side = 'left'
                                  elif x_coord < 0 and zone_code == 'O':
                                      home_team_side = 'left'
                                      away_team_side = 'right'
                                  elif x_coord > 0 and zone_code == 'D':
                                      home_team_side = 'left'
                                      away_team_side = 'right'
                                  elif x_coord > 0 and zone_code == 'O':
                                      home_team_side = 'right'
                                      away_team_side = 'left'
                              elif shooting_team_id == shot['awayTeamId']:
                                  # Away team shot
                                  if x_coord < 0 and zone_code == 'D':
                                      away_team_side = 'right'
                                      home_team_side = 'left'
                                  elif x_coord < 0 and zone_code == 'O':
                                      away_team_side = 'left'
                                      home_team_side = 'right'
                                  elif x_coord > 0 and zone_code == 'D':
                                      away_team_side = 'left'
                                      home_team_side = 'right'
                                  elif x_coord > 0 and zone_code == 'O':
                                      away_team_side = 'right'
                                      home_team_side = 'left'
                              break  # Stop after determining the sides

              # Update the DataFrame with the determined sides based on the period
              def get_offensive_side(row):
                  if row['gameId'] == game_id:
                      if row['teamId'] == row['homeTeamId']:
                          # Home team logic with modulo operation
                          return home_team_side if row['period'] % 2 == 1 else ('left' if home_team_side == 'right' else 'right')
                      elif row['teamId'] == row['awayTeamId']:
                          # Away team logic with modulo operation
                          return away_team_side if row['period'] % 2 == 1 else ('left' if away_team_side == 'right' else 'right')
                  return 'unknown'
              
              # Add the column to the DataFrame
              self.df.loc[self.df['gameId'] == game_id, 'offensiveSide'] = self.df[self.df['gameId'] == game_id].apply(get_offensive_side, axis=1)
      ```

**Création et soumission d'un sous-ensemble de données**: 

Le code fournit une méthode ```log_filtered_dataframe()``` pour : 
- Filtrer les données par ID de match (ex. : Winnipeg vs Washington, gameId = 2017021065).
- Créer un artefact dans Weights & Biases contenant ce sous-ensemble en tant que table.
- **Code**:
    ```python
  def log_filtered_dataframe(df, game_id, project_name="my_project"):
      """
      Filters the DataFrame for the specified game ID, creates a Weights & Biases artifact,
      and logs the DataFrame as a table.
      
      Args:
          df (pd.DataFrame): The DataFrame to filter and log.
          game_id (str): The game ID to filter the DataFrame.
          project_name (str): The name of the Weights & Biases project.
      """
      # Filter DataFrame for the specified game_id
      df['gameId'] = df['gameId'].astype(str)
      filtered_df = df[df['gameId'] == game_id]

      #Initialize a Weights & Biases run
      run = wandb.init(project=project_name, name=f"Filtered_Data_Run_{game_id}")

      # Create a Weights & Biases artifact
      artifact = wandb.Artifact(
          name="wpg_v_wsh_2017021065",
          type="dataset"
      )

      #CSV path - searching under data directory
      root_directory = os.path.abspath(os.path.join(os.getcwd(), '..'))
      data_dir = os.path.join(root_directory, 'data')
      filtered_df.to_csv(os.path.join(data_dir, "wpg_v_wsh_2017021065.csv"), index=False)
      csv_path = os.path.join(data_dir, "wpg_v_wsh_2017021065.csv")

      # Add the CSV file to the artifact
      artifact.add_file(csv_path)

      # Add data to the artifact as a table
      my_table = wandb.Table(dataframe=filtered_df)
      artifact.add(my_table, "wpg_v_wsh_2017021065")

      # Log the artifact
      run.log_artifact(artifact)
      run.finish()
    ```

    **Lien vers le run**: https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03/runs/copvpit7

    Ce lien contient notre artifact des données filtrées pour le match de Winnipeg vs Washington qui s'est déroulé le 12 mars 2018. 


