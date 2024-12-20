---
layout: post
title: Milestone 2
categories: Blog IFT6758_A3
---

Edward Habelrih, Michel Wilfred Essono et Rayan Yahiaoui
# Suivi des Expériences

Tout au long de ce milestone, nous avons utilisé Weights & Biases (Wandb) pour sauvegarder et suivre nos modèles à travers leurs différentes itérations, ce qui nous a permis de comparer les résultats au fil du temps. Cet outil s’est avéré extrêmement utile, offrant à notre équipe un moyen simple et interactif de surveiller les progrès. Pour chaque exécution, nous avons enregistré les figures pertinentes ainsi que les paramètres de configuration utilisés pour entraîner le modèle. De plus, les modèles ont été sauvegardés en tant qu’artifacts associés à leurs exécutions respectives.

Voici le lien vers notre espace de travail: https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03
# Ingénierie des Caractéristiques I

## 2.1 Histogrammes des Tirs

### Distance du Filet
Nous avons généré deux histogrammes illustrant le nombre de tirs (buts et non-buts séparés) en fonction de leur distance par rapport au filet, à partir des données des saisons régulières 2016-2017 à 2019-2020 (inclus). 

![Histogrammes des Tirs - Distance](/assets/images/milestone2/Nb_total_tirs_par_Distance.png)

Voici les observations clés:
  - Le nombre total de tirs diminue rapidement aux alentours de 50 mètres du but respectif. 
  - Plus la distance agumente, moins il est probable qu'un but soit marqué. En effet, on remarque la plus grande concentration de buts entre 0 à 10 mètres du but.
  - Les tirs provenant de la moitié défensive de la patinoire sont extrêmement rares, et encore plus les buts.
  - Les tirs effectués à très courte distance (<10m) ont une fréquence élevée, ce qui reflète une proximité stratégique pour maximiser les chances de marquer. En effet, que le taux de buts vs tirs est le plus élevé à ces distances.


### Angle par Rapport au Filet

Nous avons également produit deux histogrammes montrant la répartition des tirs selon leur angle relatif au filet. Le schéma ci-dessous démontre la manière dont nos angles de tirs sont représentés pour les deux côtés de la patinoire. 

![Angle Schema](/assets/images/milestone2/shot_angle_schema.png)

![Histogrammes des Tirs - Angle](/assets/images/milestone2/Distribution_Tirs_par_Angle(2016-2019).png)

Voici les observations clés:
- La majorité des tirs sont effectués directement face au filet ou à un angle modéré (environ ±40 degrés).
- Les buts sont souvent marqués à des angles réduits. À 0 degrés on remarque la plus grande quantité de buts et la tendance des buts suit une distribution normale. 
- La fréquence des buts diminue significativement pour des angles au-delà de ±40 degrés.
- Les observations de tirs à des angles extrêmes (±70 degrés ou plus) sont rares, et ils résultent rarement en buts. Ceci est probablement dû en raison de la difficulté accrue de viser avec précision sous ces conditions. Le gardien a aussi moins de surface de but à couvrir pour empêcher la rondelle de rentrer. 

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
- Les tirs sous des angles extrêmes (>±70 degrés) ne se produisent que dans des situations spécifiques et sont souvent liés à des tirs désespérés ou pour une tentative de déviation de tir.

L’analyse des distances et des angles des tirs met en lumière l'importance stratégique de la proximité du filet et des angles favorables dans la probabilité de marquer. La plupart des tirs sont tentés à courte distance, dans les zones de haut danger situées devant le filet, et sous des angles réduits, ce qui reflète une approche axée sur l'efficacité et la pression offensive. Les tirs effectués à longue distance, souvent depuis la ligne bleue ou au-delà, ou sous des angles extrêmes près des bandes, sont beaucoup moins fréquents et rarement convertis en buts. Cependant, ces tirs lointains ou difficiles peuvent jouer un rôle tactique en générant des rebonds ou en profitant de filets vides lors de situations désespérées en fin de match. Les tirs provenant de loin peuvent également être le résultat d'un dégagement de l'équipe en désavantage numérique pour sortir la rondelle de leur zone. 

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
 Finalement analysons la relation entre le nombre de buts et la distance des tirs effectués. 

![Histogrammes - Filet Vide et Non-Vide](/assets/images/milestone2/Distribution_Tirs_par_Distance(2016-2019).png)

Pour les tirs sur un filet Non-Vide voici les observations clés:
- La majorité des buts sur filet non-vide sont marqués à proximité immédiate du filet, dans la zone de haut danger. Ces tirs sont souvent effectués à partir de rebonds ou de passes rapides qui laissent peu de temps au gardien pour réagir.
- Les tirs effectués à plus de 30m voient leur probabilité de conversion en but diminuer fortement, reflétant l’efficacité des gardiens à bloquer les tirs éloignés.

Pour les tirs sur un filet Vide voici les observatinos clés:
- Les tirs sur filet vide peuvent être tentés depuis presque n'importe où sur la patinoire, y compris depuis la zone défensive ou les coins éloignés.
- Ces situations résultent généralement de la décision de l'équipe adverse de retirer son gardien pour ajouter un attaquant supplémentaire en fin de match. Étant donné que l'équipe avec le filet vide bénéficie d'un joueur supplémentaire (non gardien) sur la glace, l'équipe adverse est contrainte de se débarrasser rapidement de la rondelle pour éviter de la perdre. Cela explique la répartition variée des buts provenant de différentes distances.  
- Les tirs de longue distance (parfois supérieurs à 100 pieds) sont fréquents et réussis, en raison de l'absence de gardien pour défendre le filet.

L’analyse montre des différences importantes entre les buts marqués sur filet vide et ceux sur filet non-vide. Les buts sur filet non-vide sont souvent dus à des tirs précis ou des actions rapprochées où le gardien est mis sous pression. En revanche, les filets vides permettent des tirs plus risqués et éloignés, souvent tentés depuis des positions inhabituelles. Ces résultats mettent en évidence l’influence des situations de jeu sur les opportunités de marquer et soulignent l’importance de traiter ces cas différemment dans l’analyse des buts attendus, pour mieux refléter les choix tactiques en fin de match.

Nous avons mené une analyse approfondie des données pour identifier d’éventuelles anomalies. La tâche a été répartie équitablement entre les trois membres de notre équipe, chacun examinant 40 matchs, pour un total de 120 matchs analysés. Lors de cette vérification, nous avons minutieusement examiné les coordonnées (x, y), les types de tirs et les autres caractéristiques associées aux événements.

De plus, nous avons utilisé le GameCenter de la LNH ainsi que des vidéos sur YouTube pour valider nos observations en visionnant les clips vidéo des buts pour chaque match analysé. Cette approche nous a permis de confirmer que les événements enregistrés dans les données reflètent fidèlement les situations réelles sur la glace.

Cependant, cette analyse nous a révélé une anomalie notable. Par exemple, les données de l'API suggèrent que James van Riemsdyk a marqué un but depuis le côté gauche de la patinoire, ce qui est incorrect. En visionnant la vidéo à 3:10 minutes, il est clairement visible que le but a été marqué depuis le côté droit de la patinoire, contredisant ainsi les coordonnées fournies par l’API. En effet, nous pouvons voir que les coordonnées de la patinoire pour son tir (dernière ligne de l'image ci-dessous) ne sont pas justes.

![Anomalie](/assets/images/milestone2/anomaly.png)

Lien vers la vidéo: https://www.youtube.com/watch?v=liPQYJVSXpw&start=190

Probablement que nous aurons trouvé d'autres situations similaires, mais cela demande une couverture d'analyse beaucoup plus grande! 

# Modèles de base
En utilisant uniquement la caractéristique distance pour évaluer notre modèle de base de regression logistique,on remarque que le modèle va parfaitement prédire les cas dans lesquels il n'y a pas de but.Mais pour les cas avec but, il échoue à systématiquement.Tel que le présente la figure ci-dessous.

![Matrice de confusion du modèle de regression logistique sur la caractéristique distance](/assets/images/milestone2/confusion_matrix_logreg_dist.png)
La raison de cette disparité dans les performances du modèle pour prédire les deux est tout d'abord dû au déséquilibre dans la répartition des données des classes. En effet, tel que le montre la figure ci-dessous, le ratio entre les données de la classe 0 (no goal) et de la classe 1 (goal) est quasiment de 10 en faveur de classe 0. Cet état de fait entraîne des biais dans le modèle lors de l'entrainement.

La seconde raison pour cette grande disparité réside dans le fait de l'utilisation d'une seule caractéristique pour entrainer le modèle. En utilisant une seule caractéristique,le modèle aura moins de matière pour aller chercher les informations sous-jacentes dans les données comme on va le voir dans les modèles des sections prochaines.

![Expression du déséquilibre des classes](/assets/images/milestone2/class_distribution.png)
## Courbes ROC (ROC Curves)

Ce graphique évalue la capacité des modèles à distinguer entre les tirs réussis et non réussis, basé sur le taux de vrais positifs (TPR) et le taux de faux positifs (FPR).

**Interprétation** :
Lorsque les caractéristiques ```Distance``` et ```Angle``` sont utilisées ensemble, le modèle montre de meilleures performances avec une AUC de 0.71, indiquant une bonne capacité de discrimination.
Cependant, lorsque les caractéristiques ```Distance``` et ```Angle``` sont utilisées chacunes seules pour entrainer le modèle, on obtient des AUC de 0.69 et 0.56 respectivement. Ceci démontre une performance correcte mais tout de fois inférieure.
Le modèle aléatoire quant à lui a une AUC de 0.49, qui est exactement proche du hasard ou même d'un "coin flip".

![La courbe ROC](/assets/images/milestone2/roc_curve.png)
## Taux de Buts (Goal Rate)

Ce graphique montre la proportion de buts marqués (goals/(shots + goals)) en fonction des centiles.

**Interprétation** :
Les modèles ```Distance``` et ```Distance``` + ```Angle``` prédisent des proportions de but marqués quasiment similaires peu importe le centile. Le modèle entrainé uniquement sur la caractéristique ```angle``` prédit des proportions de but marqués inférieurs aux deux modèles précédents environ à partir du 55ème centile.
Étant donné que 10% des tirs sont des buts, on s'attend donc à ce qu'un bon modèle puisse donner une probabilité élevée de but à partir environ du 90ème centile.
Avec cela, on peut donc conclure que les modèles ```Distance``` et ```Distance``` + ```Angle``` sont meilleurs que le modèle simplement ```Angle```.

![Le taux de buts](/assets/images/milestone2/goal_rate_plot.png)
## Pourcentage Cumulatif de Buts (Cumulative % of Goal)

Ce graphique montre la proportion cumulée de buts en fonction des centiles de probabilité.

**Interprétation** :
Le modèle ```Distance``` + ```Angle``` capture les buts les plus probables plus efficacement (courbe plus proche de 1 en premier).
Les modèles ```Distance``` et ```Angle``` suivent de près, tandis que le modèle ```Random``` est linéaire (aucune distinction entre les probabilités).
Cela indique que ```Distance``` + ```Angle``` est plus performant pour identifier les tirs les plus susceptibles de rentrer dans le filet.

![La proportion cumulée de buts](/assets/images/milestone2/cum_rate_plot.png)
## Courbe de Calibration (Calibration Curve)

Cette courbe montre la calibration des modèles. Une courbe parfaitement calibrée suit la ligne pointillée (idéale).

**Interprétation** :
Le modèle ```Distance``` + ```Angle ``` semble mieux calibré dans les premiers centiles, ce qui signifie que ses probabilités prédites correspondent mieux à la proportion observée de buts.
Les modèles basés uniquement sur ```Distance``` ou ```Angle``` semblent moins bien calibrés, avec une sous-évaluation ou surévaluation selon le centile.
Le modèle ```Random``` reste constant, sans corrélation avec les résultats réels.

![Le diagramme de fiabilité](/assets/images/milestone2/calibration_curve.png)

Voici le lien vers notre modèle de base sur wandb:https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03/runs/80pxxjvs?nw=nwusermwessono


# Ingénierie des Caractéristiques II

Dans cette section, nous allons caractéristiques pertinentes issues des donnéees dispoinibles. En effet celui-ci peut se retrouver dans le fichier ```feature_engineering.py``` sous l'onglet ```src``` de notre repository.

## Caractéristiques à inclure à partir des données existantes

1. Secondes de jeu (Game seconds):
  - **Colonne créée** : ```gameSeconds```
  - **Explication** : Nombre total de secondes écoulées dans le match depuis le début, calculé à partir de la période et du temps écoulé avec la fonction ```add_game_seconds()```.
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
  - **Explication** : Coordonnées exactes du tir sur la glace, extraites des données brutes par ```calculate_shot_distance_and_angle()```.

4. Distance du tir (Shot distance) :
  - **Colonne créée** : ```shotDistance```
  - **Explication** : Distance euclidienne en mètres entre la position du tir et le filet, calculée dans ```calculate_shot_distance_and_angle()```.

5. Type de tir (Shot type) :
  - **Colonne existante** : ```shotType```
  - **Explication** : Type de tir qui a été effectué (wrist-shot, back-hand, slap-shot, etc...)

6. Angle du tir (Shot angle) :
  - **Colonne créée** : ```shotAngle```
  - **Explication** : Angle du tir par rapport à la ligne centrale du filet, calculé dans ```calculate_shot_distance_and_angle()```. 
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

## Ajout des informations sur l’événement précédent

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

## Caractéristiques supplémentaires

Trois nouvelles caractéristiques basées sur l'état du jeu et les événements précédents sont également calculées :

1. Rebond (Rebound):
  - **Colonne créée**: ```rebound```
  - **Explication**: Indique si l’événement précédent était un tir, ce qui pourrait signaler un rebond, calculé dans ```previous_event_analysis()```. Ceci est une valeur booléenne.

2. Changement d'angle du tir (Change in shot angle) :
  - **Colonne créée**: ```changeInShotAngle```
  - **Explication**: Différence entre l’angle du tir actuel et celui du tir précédent (calculé uniquement pour les rebonds). Ceci est calculé par la méthode ```previous_event_analysis()```.

3. Vitesse (Speed):
  - **Colonne créée** : speed
  - **Explication**: Vitesse en mètres par seconde depuis le dernier évènement. Distance parcourue entre l’événement précédent et l’événement actuel, divisée par le temps écoulé. Ceci est aussi calculé par la méthode ```previous_event_analysis()```.
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

## Création de caractéristiques personnalisées 

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
  - **Explication**: Côté offensif (droite ou gauche) sur la patinoire de l'équipe en train de tirer. Celui-ci change pour les deux équipes à chaque période.
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

## Création et soumission d'un sous-ensemble de données**

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

# Modèles avancés

Le code lié à cette section se retrouve dans ```advanced_models.py``` sous le répertoire ```src```. 

## Modèle de base

Pour compléter cette section, nous avons entraîné un classificateur XGBoost en utilisant uniquement les caractéristiques de ```distance``` et ```angle```. L'objectif de cette expérience était de comparer les performances de ce modèle avec la ligne de base établie dans la partie précédente à l'aide de la régression logistique. La configuration de l'entraînement a été réalisée avec une division 80/20 des données d'entraînement et de validation. Aucun réglage des hyperparamètres n'a été effectué à ce stade, le modèle XGBoost ayant été utilisé avec des paramètres par défaut. La configuration des paramètres par défaut peuvent tous être observés à ce lien:
https://xgboost.readthedocs.io/en/stable/parameter.html

**Lien vers le run:** https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03/runs/gamngm0h?


Voici les graphiques obtenus pour ce premier modèle:

![ROC base model](/assets/images/milestone2/ROC Curve Display_base.png)

La courbe ROC présente une AUC de 0.72, ce qui indique que le modèle est capable de différencier correctement les buts et les non-buts dans environ 72 % des cas. Bien que supérieure à la performance d'un classificateur aléatoire (AUC = 0.5), cette AUC est encore modérée. Cela peut indiquer que les caractéristiques utilisées (distance et angle) fournissent des informations utiles mais ne suffisent pas à capturer toute la complexité de la tâche. Le modèle montre une bonne discrimination pour des seuils faibles (proches de 0.2-0.4), mais la pente de la courbe suggère qu'il pourrait bénéficier d'une augmentation des caractéristiques explicatives ou d'un réglage des hyperparamètres.

![Goal Rate base model](/assets/images/milestone2/Goal Rate_base.png)

Le graphique du taux de buts montre une diminution progressive du taux de buts des percentiles supérieurs (100, 90) vers les percentiles inférieurs (10, 0). Par exemple :
  - Les tirs classés dans le centile supérieur (90-100) présentent un taux de buts d'environ 30 %, ce qui indique que le modèle identifie correctement les tirs de haute qualité.
  - En revanche, les percentiles inférieurs (0-10) montrent un taux de buts proche de 5 %, soulignant que le modèle attribue de faibles probabilités aux tirs moins susceptibles de réussir.

Cependant, une transition plus marquée entre les percentiles moyens et supérieurs pourrait refléter un modèle encore mieux calibré ou capable de capturer davantage de nuances dans les données.

![Cumulative Goal Rate base model](/assets/images/milestone2/Cumulative Goal Rate_base.png)

La courbe de la proportion cumulée des buts indique que les tirs classés dans les percentiles supérieurs contiennent une proportion importante des buts :
  - Environ 80 % des buts sont contenus dans les 30 % les plus probables (percentile 70 et plus), ce qui montre que le modèle est performant pour concentrer les buts dans les catégories de haute probabilité.
  - Cette courbe met également en lumière une opportunité : dans les percentiles intermédiaires (40-70), la proportion des buts n’est pas entièrement exploitée, suggérant que des caractéristiques supplémentaires pourraient aider à mieux capturer ces situations.


![Calibration Curve base model](/assets/images/milestone2/Calibration Curve_base.png)

La courbe de calibration révèle que le modèle est globalement bien calibré mais montre des variations :
  - Pour les probabilités basses (0.0 à 0.2), les prédictions du modèle sous-estiment légèrement la probabilité réelle de succès des tirs.
  - À l’inverse, pour les probabilités moyennes (0.4 à 0.6), une sur-estimation est visible. Cela peut être dû à la simplicité des caractéristiques utilisées, qui limitent la capacité du modèle à différencier efficacement les tirs moyens des tirs de haute qualité.

Ces analyses confirment que le modèle XGBoost de base exploite efficacement les caractéristiques de distance et d’angle pour prédire la probabilité qu’un tir soit un but. Cependant, des améliorations sont possibles en intégrant davantage de caractéristiques contextuelles et en ajustant les hyperparamètres.

## Modèle avec les caractéristiques de la Partie 4

Dans le cadre de l’entraînement d’un classificateur XGBoost avec toutes les caractéristiques développées dans la Partie 4, une optimisation approfondie des hyperparamètres a été réalisée afin d'améliorer les performances globales du modèle. Ces caractéristiques comprenaient des informations contextuelles telles que le type d’événement précédent, les coordonnées, le temps écoulé, la vitesse, le rebond et le changement d’angle, en plus des caractéristiques fondamentales comme la distance et l’angle. L’objectif était d’exploiter la richesse de ces données pour surpasser les modèles basiques évalués précédemments.

Pour obtenir les meilleures performances, une optimisation bayésienne a été mise en œuvre pour ajuster les hyperparamètres, notamment max_depth (profondeur maximale des arbres), learning_rate (taux d’apprentissage), n_estimators (nombre d’arbres), subsample (fraction des échantillons utilisée pour chaque arbre), et colsample_bytree (fraction des caractéristiques utilisée pour chaque arbre). Une validation croisée stratifiée a été employée pour maximiser l’AUC-ROC. Aussi, trois boosters disponibles dans XGBoost ont été testés : gbtree, dart, et gblinear.

**Lien vers le run:** https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03/runs/k7dxw7d0?

Voici le résultat de notre validation croisée.

![Cross-val F2](/assets/images/milestone2/cross_val_results_F2.png)

Voici nos meilleurs paramètres obtenus.

![ParamsF2](/assets/images/milestone2/bhp_f2.png)


Le booster gbtree s’est avéré le plus performant, avec une AUC de 0.754, démontrant sa capacité à capturer les interactions complexes entre les caractéristiques. Il est particulièrement bien adapté aux données non linéaires, où des relations complexes existent entre les variables, comme la vitesse et le changement d’angle. À l’inverse, dart, qui utilise un mécanisme de dropout pour régulariser, a montré des performances légèrement inférieures, mais dans le même champ. Bien qu’il puisse être avantageux pour des ensembles de données plus vastes, il a ici sous-performé en raison de la structure des données. Enfin, gblinear, un modèle linéaire généralisé, n’a pas réussi à exploiter la complexité des interactions des données, obtenant une AUC bien inférieure, proche de 0.65.

![ROC model 2](/assets/images/milestone2/ROC_F2.png)

La courbe ROC du modèle optimisé présente une AUC de 0.75, marquant une amélioration significative par rapport au modèle basique (AUC = 0.72). Cela montre que le modèle est mieux capable de différencier les tirs qui sont des buts de ceux qui ne le sont pas. La forme convexe de la courbe, en particulier dans les zones critiques de faibles taux de faux positifs, indique une meilleure discrimination des buts. Cette amélioration résulte de l’intégration de caractéristiques contextuelles telles que la vitesse, le rebond et le type d’événement précédent, qui capturent davantage de nuances dans les données.

![Goal Rate model 2](/assets/images/milestone2/GR_F2.png)

Le graphique du taux de buts montre une priorisation plus efficace des tirs de haute qualité par le modèle optimisé :
  - Les tirs classés dans le centile supérieur (90-100) atteignent un taux de buts proche de 100 %, ce qui est une amélioration remarquable par rapport au modèle basique (30 %). Ceci pourrait potentiellement du overfitting, mais ça reste à voir dans la section des tests.
  - En revanche, les centiles inférieurs (0-10) affichent un taux de buts proche de 5 %, ce qui est cohérent avec une attribution correcte de faibles probabilités aux tirs moins susceptibles de réussir.

Ces résultats confirment que le modèle optimisé est capable de mieux hiérarchiser les tirs selon leur probabilité de réussite, surtout dans les percentiles les plus élevés. Toutefois, une légère amélioration dans les percentiles intermédiaires (40-70) pourrait encore être explorée pour capturer davantage de nuances.

![Cumulative model 2](/assets/images/milestone2/CGR_F2.png)

La courbe de la proportion cumulée des buts révèle que le modèle optimisé concentre encore mieux les buts dans les percentiles supérieurs :
  - 90 % des buts sont contenus dans les 40 % des tirs les plus probables, contre seulement 80 % dans le modèle basique.
  - La courbe est plus proche de l’idéal dans les percentiles supérieurs, confirmant que le modèle utilise efficacement les nouvelles caractéristiques pour prédire les buts.

Cependant, dans les percentiles intermédiaires (30-70), il reste une marge d’amélioration pour capturer les buts classés comme probabilité moyenne.

![Calibration curve model 2](/assets/images/milestone2/CC_F2.png)

La courbe de calibration montre une correspondance quasi-parfaite entre les probabilités prédites et les fréquences réelles des buts :
  - Contrairement au modèle basique, les probabilités basses (0.0 à 0.2) sont correctement estimées, et les probabilités moyennes (0.4 à 0.6) ne présentent plus de sur-estimation significative.
  - Cette amélioration indique que l’optimisation des hyperparamètres a permis au modèle d’être non seulement plus performant, mais aussi mieux calibré, rendant ses prédictions plus fiables.

Comparé au modèle de base XGBoost utilisant uniquement les caractéristiques de distance et angle avec une AUC de 0.72, le modèle optimisé montre une nette amélioration, atteignant une AUC de 0.754, grâce à l'ajout de caractéristiques supplémentaires et à l'optimisation des hyperparamètres. Le taux de buts pour les percentiles supérieurs (90-100) passe de 30 % à 35 %, indiquant une meilleure identification des tirs de haute qualité. De plus, la proportion cumulée des buts reste concentrée dans les 30 % les plus probables, mais avec une répartition plus précise des probabilités, reflétant un modèle mieux calibré. Enfin, la courbe de calibration du modèle optimisé est plus proche de la ligne idéale, réduisant les écarts entre les probabilités prédites et les probabilités observées, ce qui démontre une amélioration globale de la performance et de la fiabilité du nouveau modèle.  

## Sélection de caractéristiques supplémentaires

Dans cette prochaine section, nous allons explorer des techniques de sélection de caractéristiques pour simplifier nos caractéristiques d'entrées. Nous avons employé deux algorithmes: SelectKBest et Shap.

SelectKBest est une technique simple mais efficace pour sélectionner les caractéristiques en fonction de tests statistiques. Ici, la fonction f_classif a été utilisée, basée sur l’ANOVA, pour calculer l’importance des caractéristiques en mesurant leur capacité à discriminer les classes. Les scores attribués par cette méthode ont été utilisés pour trier les caractéristiques par pertinence. Les dix meilleures caractéristiques selon ces scores ont été retenues pour construire un modèle plus léger et efficace. Cela a permis d’éliminer les caractéristiques redondantes ou peu pertinentes tout en réduisant la dimensionnalité du problème.

![Top KBest](/assets/images/milestone2/select k best features.png)

Nous avons utilisé la méthode SelectKBest pour identifier les 10 caractéristiques les plus pertinentes pour le modèle. Parmi celles-ci, la caractéristique shotDistance se démarque nettement avec un score de 7307.169, indiquant son influence majeure sur les prédictions du modèle. D'autres caractéristiques importantes, comme rebound, speed et powerplayHome, contribuent également de manière significative, mais dans une moindre mesure. Une optimisation des hyperparamètres a été réalisée pour améliorer les performances du modèle en utilisant ces caractéristiques sélectionnées. 

Cependant, le score final ROC_AUC obtenu était de 74.7, inférieur à celui obtenu avec la sélection basée sur SHAP (AUC de 0.75498) et légèrement supérieur au modèle avec les caractéristiques de la Partie 4 (AUC de 0.754).

La méthode SelectKBest a permis de réduire efficacement la dimensionnalité en se concentrant sur les corrélations statistiques entre chaque caractéristique et la variable cible. Toutefois, cette méthode manque de l'interprétabilité au niveau des instances que fournit SHAP.

SHAP (SHapley Additive exPlanations) est une méthode basée sur la théorie des jeux pour expliquer les prédictions des modèles en attribuant une importance à chaque caractéristique. Il calcule les contributions marginales de chaque caractéristique en considérant toutes les combinaisons possibles, ce qui fait une approche robuste pour interpréter des modèles complexes. 

La principale différence entre ces deux techniques est la relation entre les caractéristiques. SelectKBest est une méthode de sélection de caractéristiques basée uniquement sur une statistique univariée (comme le test ANOVA), évaluant chaque caractéristique indépendamment de toutes les autres. En revanche, SHAP prend en compte les interactions entre les caractéristiques et attribue des valeurs d'importance en fonction de leur contribution au modèle global. 

Analysons en premier lieu notre meilleur modèle qui a été roulé avec l'analyse SHAP pour choisir les top 10 caractéristiques et qui a ensuite subi une validation croisée exactement comme dans la section précédente pour effectuer l'entraînment du meilleur modèle.

![Top Shap features](/assets/images/milestone2/SHAP_TOP10.png)

Le tableau montre les caractéristiques les plus importantes pour le modèle XGBoost optimisé, avec leurs valeurs moyennes SHAP. La caractéristique la plus influente est shotDistance, qui a une valeur moyenne SHAP significative de 0.7289. Cette caractéristique est suivie par yCoord (0.2592) et shotType (0.2152), entre autres. Ces résultats indiquent que la distance du tir et la position sur l'axe Y ont un impact notable sur la probabilité de succès d'un tir. Les autres caractéristiques, telles que shotAngle et speed, confirment également leur importance dans le contexte du hockey.

![Shap HP](/assets/images/milestone2/shapHP.png)

On peut également voir les hyper-paramètres optimaux suite à la validation croisée performée avec l'optimisation Bayes.

![SHAP roc](/assets/images/milestone2/SHAProc.png)

La courbe ROC est similaire au résultat précédent, cependant encore une fois la sélection de ce modèle en tant que notre meilleur XGBoost s'est joué dans les nombres décimaux. 

![SHAP GR](/assets/images/milestone2/SHAPgr.png)

Le graphique du taux de buts montre une nette corrélation entre les percentiles supérieurs des probabilités prédites et le taux de réussite des tirs. Les tirs classés dans les 10 % supérieurs présentent un taux de buts proche de 30 %, ce qui reflète une bonne identification des tirs de haute qualité.

![SHAP CGR](/assets/images/milestone2/shapCGR.png)

Ce graphique met en évidence que plus de 80 % des buts sont regroupés dans les 30 % les plus probables. Cela confirme que le modèle attribue correctement des scores de haute probabilité aux tirs susceptibles de réussir.


![SHAP CC](/assets/images/milestone2/SHAPcc.png)

Le graphique montre que le modèle est bien calibré pour des probabilités faibles à modérées, mais il surestime légèrement pour des probabilités élevées. Cela peut être attribué à la complexité des interactions entre les caractéristiques.


Par rapport aux autres modèles testés, l’approche utilisant SHAP s’est avérée être la meilleure grâce à sa capacité à identifier les caractéristiques les plus pertinentes tout en améliorant la performance globale. Avec une AUC de 0.75, SHAP dépasse le modèle de base (AUC de 0.72) et les modèles optimisés par validation croisée, tout en simplifiant les données d’entrée en sélectionnant seulement 10 caractéristiques clés comme shotDistance, yCoord et shotType. Contrairement à SelectKBest, qui sélectionne des caractéristiques sans interprétation, SHAP offre une transparence unique en attribuant une importance précise à chaque caractéristique pour chaque prédiction, ce qui améliore l’interprétabilité et la robustesse du modèle. De plus, la calibration du modèle SHAP est bien ajustée, réduisant les biais observés dans les autres approches.

Voici le lien de notre meilleur modèle de la famille XGBoost: https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03/runs/vje687th

# Faites de votre mieux!

## Q6_Random_forest
Voici les graphiques obtenus pour le modèle RandomForest:
![ROC CURVE RF](/assets/images/milestone2/roc_curve_RF.png)
La courbe ROC montre une performance globale acceptable avec une aire sous la courbe (AUC) autour de 0,73. Cela indique que le modèle est capable de discriminer correctement entre les classes positives et négatives dans environ 73 % des cas, mais reste inférieur aux modèles optimisés comme SHAP.
![Goal Rate RF](/assets/images/milestone2/GoalRateCurve_RF.png)
La courbe "Goal Rate" montre une chute rapide du taux de buts dans les percentiles les plus élevés. Les shots avec une probabilité élevée (percentiles supérieurs) sont significativement plus précis, mais la courbe descend de façon progressive, suggérant une corrélation modérée entre les probabilités prédites et les buts réels.
![Proportion Cumulee RF](/assets/images/milestone2/CumulativeGoalRate_RF.png)
La courbe cumulative montre une bonne couverture des buts dans les percentiles supérieurs, atteignant environ 80 % des buts avec les 50 % les plus probables. Cela reflète que le modèle capture bien les événements les plus probables, mais avec une précision légèrement inférieure par rapport à d'autres approches.
![Calibration Curve RF](/assets/images/milestone2/Calibration_Curve_RF.png)
La courbe de calibration montre que les probabilités prédites sont légèrement sous-calibrées pour les faibles probabilités et deviennent plus alignées avec les observations pour des probabilités élevées. Cependant, des ajustements pourraient encore améliorer l'alignement, notamment pour les bins intermédiaires.
### Prétraitement des données
Nous avons commencé par traiter les données pour garantir leur qualité et leur pertinence. Pour les colonnes catégorielles avec de nombreuses valeurs distinctes, nous avons utilisé un encodage de fréquence pour transformer chaque catégorie en une proportion au sein du jeu de données. Pour les colonnes binaires, nous avons appliqué un encodage one-hot, ce qui facilite leur interprétation par le modèle. Les données numériques manquantes ont été imputées en remplaçant les valeurs manquantes par la médiane de chaque colonne
#### Colonnes spécifiques et transformations

- **shotType** :
  - Encodage de fréquence pour transformer chaque catégorie en sa proportion dans le jeu de données. Cela capture l'importance relative de chaque type de tir tout en réduisant la dimensionnalité.

- **lastEventType** :
  - Encodage de fréquence appliqué pour convertir les types d'événements précédents en valeurs normalisées représentant leur occurrence.

- **HomevsAway** et **offensiveSide** :
  - Utilisation de l'encodage one-hot avec `drop='first'` pour éviter la multicolinéarité. Cela crée des variables binaires pour chaque catégorie, en éliminant une catégorie de référence.

- **shooter** :
Le taux de réussite d’un joueur face à un gardien est une caractéristique clé pour déterminer si un tir va réussir ou non. Nous avons utilisé un encodage cible avec lissage pour éviter le surapprentissage. Nous avons développé un encodage cible personnalisé (PlayerTargetEncoder) pour calculer un taux de réussite lissé pour chaque joueur.
```python
class PlayerTargetEncoder(BaseEstimator, TransformerMixin):
    def __init__(self, smoothing=10):
        self.smoothing = smoothing
        self.player_stats = {}
        self.global_mean = None

    def fit(self, X, y):
        if isinstance(X, pd.DataFrame):
            # Gestion des colonnes pour les tireurs et les gardiens
            for column in X.columns:
                self.player_stats[column] = {}
                
                player_counts = X[column].value_counts()
                # Calcul de la moyenne globale pour ce type de joueur
                self.global_mean = np.mean(y)
                
                for player in player_counts.index:
                    mask = (X[column] == player)
                    shots = np.sum(mask)
                    goals = np.sum(y[mask])
                    
                    # Taux de réussite lissé
                    smoothed_rate = (goals + self.smoothing * self.global_mean) / (shots + self.smoothing)
                    self.player_stats[column][player] = smoothed_rate
        
        return self

    def transform(self, X):
        if isinstance(X, pd.DataFrame):
            result = np.zeros((len(X), len(X.columns)))
            
            for idx, column in enumerate(X.columns):
                result[:, idx] = X[column].map(self.player_stats[column]).fillna(self.global_mean)
            
            return result
        
        return X.map(self.player_stats).fillna(self.global_mean).to_numpy().reshape(-1, 1)
 ```

- **Caractéristiques numériques** (`shotDistance`, `shotAngle`, etc.) :
Le modèle Random Forest n'a pas besoin de standardisation ou de normalisation; nous avons donc décidé de conserver les valeurs originales en utilisant la méthode 'passthrough', permettant ainsi au modèle d'interpréter directement ces valeurs.

- **Caractéristiques binaires** (`emptyNetGoal`, `rebound`) :
  - Conversion directe en entiers (0 ou 1) sans transformation complexe.

### Stratégies de gestion des données

#### Sous-échantillonnage

Nous avons décidé d'utiliser le sous-échantillonnage après avoir essayé le suréchantillonnage et une combinaison des deux, car le sous-échantillonnage a donné de meilleurs résultats. Ceci était crucial en raison du déséquilibre significatif entre le nombre de tirs et de buts (ratio de 10:1). Sans sous-échantillonnage, le modèle avait tendance à prédire majoritairement des zéros plutôt que des uns.
Un RandomUnderSampler avec un ratio de 0.4 a été utilisé pour rééquilibrer les classes et réduire la surreprésentation de la classe majoritaire. Ce ratio a été déterminé après avoir évalué plusieurs métriques (accuracy, recall, precision, F1, ROC AUC) sur différents taux d'échantillonnage, afin d'observer leur évolution.
!["Evolution des differentes metriques selon le taux d'Undersampling"](/assets/images/milestone2/SamplingStrategy.png)
#### Imputation
- Pour les colonnes numériques comme `speed` et `distanceFromLastEvent`, nous avons utilisé la médiane pour remplacer les valeurs manquantes par des valeurs contextuellement pertinentes.
- Nous avons également drop changeinShotAngle car trop de valeurs manquantes.
### Caractéristiques dérivées

Nous avons créé plusieurs caractéristiques dérivées pour enrichir notre modèle :
- `shots_period_cumsum` : Nombre cumulatif de tirs par période et par équipe.
- `cumulative_possession_time` : Temps de possession cumulatif. L'idée derrière cette caractéristique est que l'équipe ayant le plus de possession contrôle davantage le jeu et a donc plus de chances de marquer.
- `time_since_last_shot` : Temps écoulé depuis le dernier tir. Plusieurs tirs consécutifs ont plus de chances de se traduire par un but.
- `consecutive_penalties` : Nombre consécutif de pénalités. Plus une équipe accumule de pénalités, plus elle est désavantagée, ce qui facilite les opportunités de tir pour l'équipe adverse.
- `score_differential` : Différence de score au moment du tir, en excluant le tir en question pour éviter tout problème de fuite de données (data leakage). Cette caractéristique a été calculée en cumulant le score puis en appliquant un décalage d'une ligne (shift).
Comme nous pouvons le voir sur l'histogramme ci-dessous: 
!["Top 20 des caracteristiques les plus importantes"](/assets/images/milestone2/Top20Carac.png)
- Comme le montre l'histogramme, les variables ayant le plus d'impact sur la décision de l'arbre incluent : la distance au but (plus un joueur est proche du but, plus ses chances de marquer augmentent), la coordonnée y, et l'état du but (vide ou non).
- Parmi les nouvelles caractéristiques, seule shooter a eu un impact notable sur les performances(un meilleur joueur a plus de chance de marquer), time_since_last_shot a aussi un impact équivalent à l'angle du tir. Nous avons également essayé d'ajouter des caractéristiques basées sur le taux de victoire/défaite/nuls au cours de la saison, mais cela n'a pas eu d'influence significative sur le modèle. 
### Pondération des classes

Pour le `RandomForestClassifier`, nous avons attribué un poids différent à chaque classe, trouvant qu'un poids de 1:2 était optimal :
  - Classe 0 (non-but) : Poids 1
  - Classe 1 (but) : Poids 2

Cela permet de donner plus d'importance aux événements de but, rares mais cruciaux.

### Pipeline de prétraitement

Notre pipeline combine plusieurs transformateurs :

- Encodage cible pour les tireurs.
- Transformation numérique 'passthrough'.
- Encodage one-hot pour les caractéristiques catégorielles avec peu de catégories.
- Conservation des caractéristiques binaires.

### Optimisation des hyperparamètres
Nous avons utilisé `RandomizedSearchCV` pour explorer :
- Nombre d'estimateurs.
- Profondeur maximale des arbres.
- Nombre minimal de samples pour le split.
- Nombre de features considérées.
- Et autres paramètres de régularisation.

### Validation
Nous avons également essayé la validation croisée stratifiée avec `StratifiedKFold` avec 10 splits. Ce qui a légerement amélioré la qualité du modèle.
```python 
# Configuration de la validation croisée
cv_splitter = StratifiedKFold(n_splits=10, shuffle=True, random_state=42)
```
Comme métrique d'évaluation, nous avons choisi score ROC_AUC. Nous avons également experimenté avec une version personnalisé du Fbeta score car la precision et le recall du modèle étaient bas. 
```python 
def custom_scorer(y_true, y_pred_proba, beta=1.0):
    thresholds = np.arange(0.1, 0.9, 0.05)
    best_score = 0
    
    for threshold in thresholds:
        y_pred = (y_pred_proba >= threshold).astype(int)
        precision = precision_score(y_true, y_pred)
        recall = recall_score(y_true, y_pred)
        
        # F-beta score pour donner plus de poids à la précision ou au rappel
        if precision + recall > 0:
            score = (1 + beta**2) * (precision * recall) / (beta**2 * precision + recall)
            best_score = max(best_score, score)
            
    return best_score
```

Cette approche détaillée et nuancée nous a permis de construire un modèle prédictif avec un score ROC_AUC de 0.77,un recall de 60% et une précision assez basse de 22%. Pour améliorer le modèle, l'ajout de nouvelle features semble nécessaire.

**Lien vers le run**: https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03/runs/d45pn2k2

## Q6_KNN (K-Nearest Neighbors)

**Lien vers le run:** https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03/runs/b1n377fy?

Voici les graphiques obtenus pour le modèle KNN:
![ROC CURVE KNN](/assets/images/milestone2/roc_curve_KNN.png)
La courbe indique une AUC d’environ 0.65, ce qui reflète une capacité modérée du modèle à distinguer les classes positives et négatives. Ce score est nettement inférieur à celui obtenu avec SHAP (0.75) et démontre que ce modèle est moins performant que les approches précédentes.
![Goal Rate KNN](/assets/images/milestone2/GoalRateCurve_KNN.png)
Le modèle montre un taux de conversion élevé pour les tirs dans les percentiles supérieurs, atteignant près de 40 % pour les tirs les mieux classés. Cependant, le taux chute rapidement pour les autres percentiles, suggérant que le modèle a des difficultés à bien classifier les tirs ayant des probabilités moyennes.
![Proportion Cumulee KNN](/assets/images/milestone2/CumulativeGoalRate_KNN.png)
La courbe montre que les 20 % des meilleurs percentiles capturent environ 70 % des buts, un résultat correct mais inférieur comparé aux modèles optimisés précédemment, où une meilleure couverture des buts était atteinte avec les percentiles supérieurs.
![Calibration Curve KNN](/assets/images/milestone2/Calibration%20Curve_KNN.png)
Les prédictions ne sont pas bien calibrées. Par exemple, pour une probabilité moyenne prédite de 0.6, la fraction de vrais positifs est souvent surestimée. Cette mauvaise calibration reflète un écart significatif entre les scores du modèle et la réalité observée, ce qui limite son utilité pour des décisions basées sur des probabilités. 
### Prétraitement des données
Les principales différences dans le prétraitement pour KNN incluent :
- **Standardisation des caractéristiques numériques** :
  - Contrairement au Random Forest, KNN est sensible à l'échelle des données. Nous avons utilisé un StandardScaler afin de standardiser toutes les colonnes numériques(`shotDistance`, `shotAngle`, etc.), une étape cruciale pour les modèles basés sur des distances, comme KNN. 
```python
numeric_transformer = Pipeline(steps=[
    ('scaler', StandardScaler())
])
```
## Modèle et paramètres spécifiques à KNN

Le modèle KNN, contrairement à Random Forest, repose fortement sur le choix de l'hyperparamètre `k` (nombre de voisins) et de la métrique de distance. Voici les hyperparamètres explorés :

- **n_neighbors** : Nombre de voisins (k).
- **weights** :
  - `uniform` : Tous les voisins ont le même poids.
  - `distance` : Les voisins proches ont plus d'impact.
- **metric** : Métrique utilisée pour calculer les distances (`euclidienne`, `manhattan`, `minkowski`).
- **p** :
  - `p=1` : Distance de Manhattan.
  - `p=2` : Distance euclidienne.
- **leaf_size** : Paramètre influençant la recherche rapide des voisins.

```python
param_grid = {
    'classifier__n_neighbors': [3, 5, 7, 9, 11, 13, 15],
    'classifier__weights': ['uniform', 'distance'],
    'classifier__metric': ['euclidean', 'manhattan', 'minkowski'],
    'classifier__p': [1, 2],
    'classifier__leaf_size': [20, 30, 40]
}
```
## Tests du nombre de voisins (k)
Nous avons exploré les performances du modèle en fonction du nombre de voisins (`k`).

 Les résultats ont montré que :
!["KNN performance selon le nombre de voisins"](/assets/images/milestone2/KNN_per_neighbors.png)
À partir du graphique, nous pouvons observer que le modèle KNN a des difficultés à gérer un **déséquilibre des classes**, ce qui affecte ses performances selon les différentes métriques :

### Accuracy
- L'accuracy reste stable autour de **0.8**, mais cette métrique peut être trompeuse en cas de déséquilibre des classes.
### Precision (Précision positive)
- La précision est relativement **basse**, autour de **0.2 à 0.3**, ce qui indique que le modèle génère un nombre important de **faux positifs**.
- Cela indique que le modèle a du mal à identifier correctement les échantillons appartenant à la classe minoritaire.
### Recall (Rappel)
- Le rappel est très variable, oscillant fortement en fonction de `k`, ce qui souligne une dépendance importante au choix du nombre de voisins.
- Cela montre que la capacité du modèle à détecter les échantillons de la **classe minoritaire** dépend fortement du **nombre de voisins (k)**.
- Cette instabilité est un signe supplémentaire des difficultés du modèle à gérer le déséquilibre des classes.

### ROC AUC (Aire sous la courbe ROC)
- La courbe **ROC AUC** monte légèrement avec l'augmentation de `k`, puis se stabilise autour de **0.7**.
- Bien que cette valeur indique une capacité modérée du modèle à distinguer les classes, elle reste limitée par le déséquilibre des classes.

Le KNN montre une forte sensibilité au déséquilibre des classes, se traduisant par une précision faible et un recall instable. Bien que l'accuracy et le ROC AUC soient relativement stables, ils ne suffisent pas à compenser les lacunes du modèle sur la classe minoritaire. En résumé, bien que le sous-échantillonnage ait aidé à équilibrer les données, KNN semble limité pour ce problème en raison de sa forte dépendance à la densité locale des données.

## Q6_MLP (Multi layer perceptron)

### Préparation des données
Nous avons utilisé un ensemble de données comportant des informations sur les tirs, telles que la distance du tir, l'angle, les coordonnées, et d'autres variables contextuelles comme le type d'événement précédent et le temps écoulé depuis cet événement.

Les données ont été nettoyées et transformées comme suit :

Conversion des colonnes temporelles en secondes.
Encodage des variables catégoriques (lastEventType, shotType) en utilisant leur fréquence relative dans l'ensemble de données.
Imputation des valeurs manquantes avec des stratégies adaptées : moyenne pour les colonnes numériques et valeur la plus fréquente pour les colonnes catégoriques.

### Équilibrage des classes
Pour traiter le problème de déséquilibre entre les classes :
Nous avons procéder tout d'abord par Suréchantillonnage SMOTE : la classe minoritaire a été augmentée pour représenter 20 % de la classe majoritaire.
Puis par un Sous-échantillonnage aléatoire : les classes majoritaires ont été réduites pour équilibrer les proportions.
Ces techniques garantissent que le modèle ne privilégie pas systématiquement la classe majoritaire.

### Construction du modèle
Pipeline de traitement
Nous avons conçu un pipeline modulaire permettant de combiner :

- La prétraitement des données (scalage, encodage).
- La sélection de caractéristiques (avec SelectFromModel basé sur un LinearSVC).
- La classification avec un MLP.
- Architecture du modèle
- Le MLP est paramétré avec les hyperparamètres suivants :

```python
 def pipeline(classifier,feature_selection,encoder):

    enc = {
        'Label': OrdinalEncoder(handle_unknown='use_encoded_value', unknown_value=-1),
        'OneHot': OneHotEncoder(handle_unknown='ignore')
    }
    numeric_transformer = Pipeline([('Impt', SimpleImputer(strategy='mean')),('scaler', StandardScaler()),]) #Scaling of numerical col.
    categorical_transformer = Pipeline([('Impt', SimpleImputer(strategy='most_frequent')),('encoder', enc[encoder]),]) #Encoding of categorical col.  
    preprocessor = ColumnTransformer(
        transformers=[
            ("Numerical_transform", numeric_transformer, make_column_selector(dtype_include="number")),
            ("Categorical_transform", categorical_transformer, make_column_selector(dtype_exclude="number")),
        ]
    )  
    return Pipeline(steps=[('preprocessor', preprocessor)] + [('feature_select', feature_selection)] + [('classifier', classifier)])

classifer=MLPClassifier(hidden_layer_sizes='hidden_layer_sizes', 
                        activation = 'activation',solver='solver',
                        alpha='alpha',learning_rate='learning_rate',
                        max_iter=1000)
feature_selection= SelectFromModel(estimator=LinearSVC(C=0.1, penalty="l1", dual=False))
ecoder='Label'
pipe = pipeline(classifer,feature_selection,ecoder)

parameter_space = {
    'classifier__hidden_layer_sizes': [(50,50,50), (50,100,50), (10,100,10)],
    'classifier__activation': ['tanh', 'relu'],
    'classifier__solver': ['sgd', 'adam'],
    'classifier__alpha': [0.05,0.001,0.0001,0.00001,0.00001],
    'classifier__learning_rate': ['constant','adaptive'],
}

```
!["Courbe ROC "](/assets/images/milestone2/ROC_MLP.png)
La courbe ROC du modèle MLP montre une AUC de 0.762, ce qui indique que le modèle performe mieux qu'un classificateur aléatoire (AUC = 0.5) mais reste en deçà de certains autres modèles testés. Cela suggère que le modèle capture certaines relations non linéaires dans les données, mais que sa capacité prédictive pourrait être limitée par un surajustement ou un réglage insuffisant des hyperparamètres.

!["Taux de buts"](/assets/images/milestone2/GR_MLP.png)
Le graphique du taux de réussite montre que le modèle prédit des probabilités plus élevées pour les buts dans les percentiles supérieurs, mais ce taux diminue rapidement après le 20e percentile. Cela reflète une puissance prédictive modérée, le modèle ayant du mal à différencier efficacement les buts dans les percentiles moyens et inférieurs.

!["Proportion cumulée de buts"](/assets/images/milestone2/CGR_MLP.png)
Le graphique du pourcentage cumulatif de buts montre une accumulation progressive des buts à mesure que le percentile des probabilités diminue. Cela confirme que le modèle MLP classe correctement une grande partie des buts dans les percentiles élevés. Cependant, le rythme d'accumulation est plus lent comparé à des modèles plus optimisés, ce qui suggère une efficacité de classement sous-optimale.
!["Diagramme de fiabilité"](/assets/images/milestone2/CC_MLP.png)


La courbe de calibration montre que les probabilités prédites par le modèle MLP s'écartent de la ligne idéale diagonale, en particulier pour les probabilités prévues élevées. Le modèle a tendance à surestimer les probabilités dans les plages intermédiaires et à légèrement les sous-estimer aux extrêmes, ce qui indique un besoin d'amélioration dans la calibration.

Voici le lien de notre meilleur modèle MLP: https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03/runs/zpt0bx5j?nw=nwusermwessono

### Conclusion

En résumé, le modèle MLP a été choisi comme le meilleur car il offre une meilleure performance globale, avec une AUC de 0.762, surpassant les résultats obtenus avec le KNN et le Random Forest. Contrairement à ces derniers, le MLP capture mieux les relations complexes et non linéaires dans les données, ce qui en fait un modèle plus adapté pour cette tâche. De plus, les courbes de calibration et de taux de buts montrent une meilleure cohérence dans la prédiction des probabilités, renforçant la fiabilité du modèle. 


# Évaluer sur l'ensemble de test

Dans cette section, nous évaluons les performances de plusieurs modèles sur l'ensemble de test final. Nous utilisons d'abord les trois modèles simples développés précédemment, suivis d'un modèle de perceptron multicouche (MLP) personnalisé, optimisé pour cette tâche. Enfin, nous explorons un modèle XGBoost, accompagné de l'outil SHAP pour une sélection efficace des caractéristiques. Cette approche nous permet d'analyser la robustesse et l'efficacité de chaque méthode dans le cadre de notre problématique.

Nous utilisons enfin les ensembles de tests générés dans les premières sections afin d'èvaluer le meilleur de nos modèles.

**Résultats sur l'ensemble de test saison régulière 2020-2021**:

!["ROC - reg"](/assets/images/milestone2/roc_test_r.png)

La courbe ROC montre que le modèle XGBoost a la meilleure aire sous la courbe (AUC = 0.76), indiquant une meilleure performance globale pour séparer les classes positives et négatives. Il est suivi de près par le modèle de régression logistique utilisant les caractéristiques combinées (logreg_comb, AUC = 0.71) et celui utilisant uniquement la distance (logreg_dist, AUC = 0.70). Les modèles MLP (AUC = 0.63) et logreg_ang (AUC = 0.56) sont moins performants.

!["GR - reg"](/assets/images/milestone2/gr_test_r.png)

Le taux de buts en fonction des percentiles de probabilité montre que XGBoost reste supérieur, surtout dans les percentiles les plus élevés. Les modèles logreg_comb et logreg_dist suivent une tendance proche et cohérente, avec une performance stable. Les modèles MLP et logreg_ang montrent des fluctuations importantes, ce qui suggère une plus grande instabilité dans leurs prédictions pour les percentiles supérieurs.

!["CC - reg"](/assets/images/milestone2/cc_test_r.png)

Dans la courbe de calibration, XGBoost est relativement bien calibré pour les probabilités plus élevées. Cependant, pour les probabilités basses et moyennes, il semble s'écarter de la ligne de calibration parfaite. Le modèle MLP montre une tendance plus erratique, suggérant un besoin d'ajustement. Les modèles logreg_dist et logreg_comb présentent des comportements intermédiaires mais ne sont pas aussi proches de la calibration idéale.

!["CG - reg"](/assets/images/milestone2/cgr_test_reg.png)

Sur cette courbe, XGBoost domine encore, indiquant qu'il capte la majorité des buts de manière plus efficace à travers les percentiles. Logreg_comb et logreg_dist suivent une trajectoire similaire mais légèrement moins performante. MLP, bien qu'il présente une progression correcte, est globalement moins performant. Enfin, logreg_ang est le moins performant avec une faible proportion cumulée.

XGBoost s'impose comme le modèle le plus performant sur l'ensemble de test, suivi de logreg_comb et logreg_dist. Les performances des modèles MLP et logreg_ang sont inférieures, nécessitant potentiellement un ajustement ou des améliorations dans leur configuration.

En général, les modèles fonctionnent moins bien sur l'ensemble de test que sur l'ensemble de validation. Cela peut être attribué au sur-apprentissage ou à des différences entre les distributions des ensembles de données. Par exemple, bien que le MLP soit un modèle plus complexe et théoriquement capable de mieux capturer les relations non linéaires dans les données, il n'a pas atteint les performances attendues sur l'ensemble de test. Cela suggère que le MLP pourrait avoir surappris les caractéristiques spécifiques des données d'entraînement ou de validation, mais échoue à généraliser efficacement. 

**Résultats sur l'ensemble de test de série éliminatoire**:

!["ROC - p"](/assets/images/milestone2/roc_test_p.png)

Dans les séries éliminatoires, le modèle XGBoost reste le meilleur avec une AUC de 0.74, montrant une bonne capacité à distinguer les classes. Cependant, son score est légèrement inférieur à celui observé pour la saison régulière. Les modèles logreg_comb (AUC = 0.69) et logreg_dist (AUC = 0.68) maintiennent des performances similaires à celles de la saison régulière, mais le modèle MLP (AUC = 0.65) reste en retrait, confirmant des difficultés à généraliser aux séries. Enfin, logreg_ang est toujours le modèle le moins performant avec une AUC de 0.57.

!["GR - p"](/assets/images/milestone2/gr_test_p.png)

Sur cette courbe, le modèle XGBoost montre à nouveau une performance stable, bien que les taux de buts tendent à être légèrement moins distincts entre les modèles dans les séries éliminatoires. Logreg_comb et logreg_dist offrent des performances compétitives. Cependant, MLP et logreg_ang présentent encore des fluctuations importantes, indiquant des prédictions moins fiables.

!["CC - reg"](/assets/images/milestone2/cc_test_p.png)

La calibration des modèles dans les séries éliminatoires révèle que XGBoost reste relativement bien calibré pour les hautes probabilités, mais moins précis pour les basses probabilités. Les modèles logreg_comb et logreg_dist montrent un comportement légèrement amélioré comparé à la calibration dans la saison régulière. Cependant, le modèle MLP reste mal calibré, ce qui peut expliquer ses performances limitées dans d'autres métriques.

!["CG - reg"](/assets/images/milestone2/cgr_test_p.png)

La proportion cumulée des buts montre une tendance similaire à celle de la saison régulière, avec XGBoost en tête, suivi des modèles logreg_comb et logreg_dist. Ces derniers montrent une capacité à suivre les performances de XGBoost de manière satisfaisante. MLP et logreg_ang présentent une performance inférieure, avec une difficulté à capturer efficacement les buts cumulés.

Les résultats pour les séries éliminatoires confirment une légère baisse des performances globales des modèles par rapport à la saison régulière, probablement en raison des différences dans les données des séries. En effet, les séries accueillent un nombre exclusif d'équipes voulant dire que les patterns que nous avons appris dans les données d'entraînement ne s'appliquement pas entièrement à ces matchs. Aussi, en séries éliminatoires les équipes changent leurs stratégies de jeux ce qui peut mener à beaucoup de scénarois différents de buts qu'on a jamais vus auparavant. Un autre facteur pouvant mener à cette différence, est l'état mental des joueurs. En effet, on remarque un stress accru en séries éliminatoires ce qui peut grandement affecter la qualité des tirs ou même les performances des joueurs et gardiens. 

En conclusion, le modèle XGBoost avec SHAP reste le plus performant et robuste, suivi de près par logreg_comb et logreg_dist. Le MLP, bien qu'étant un modèle plus complexe, continue de décevoir en termes de généralisation, particulièrement dans des contextes comme les séries où les données peuvent être moins prévisibles.

**Lien du run de test:** https://wandb.ai/michel-wilfred-essono-university-of-montreal/IFT6758.2024-A03/runs/kkfh7fyo?

# Références

1. https://www.google.com/search?q=nhl+api+documentation&oq=nhl+api+doc&gs_lcrp=EgRlZGdlKgwIABBFGDsYgAQY-QcyDAgAEEUYOxiABBj5BzIGCAEQRRg5MggIAhAAGBYYHjIICAMQABgWGB4yCAgEEAAYFhge0gEIMjYxNmowajSoAgCwAgA&sourceid=chrome&ie=UTF-8
2. https://www.nhl.com/stats/
3. https://www.ibm.com/topics/logistic-regression
4. https://www.geeksforgeeks.org/understanding-logistic-regression/
5. https://xgboost.readthedocs.io/en/stable/
6. https://scikit-learn.org/1.5/modules/generated/sklearn.feature_selection.SelectKBest.html
7. https://www.simplilearn.com/tutorials/statistics-tutorial/what-is-annova-test
8. https://shap.readthedocs.io/en/latest/
9. https://www.ibm.com/topics/random-forest#:~:text=Random%20forest%20is%20a%20commonly,both%20classification%20and%20regression%20problems.
10. https://www.ibm.com/topics/knn#:~:text=The%20k%2Dnearest%20neighbors%20(KNN,used%20in%20machine%20learning%20today.
11. https://www.geeksforgeeks.org/multi-layer-perceptron-learning-in-tensorflow/
12. https://scikit-learn.org/1.5/auto_examples/model_selection/plot_roc_crossval.html
13. https://github.com/dtreisman/BigDataCup2021