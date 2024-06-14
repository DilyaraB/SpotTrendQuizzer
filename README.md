# SpotTrend Quizzer 

lien de l'appli:  https://spottrendquizzer.onrender.com

Pour démarrer le serveur localement: 
- cd serveur
- go run .

Pour démarrer le client:
- cd spotrend-quizer
- npm start

## Description de l'application

SpotTrend Quizzer est une application web interactive qui offre un quiz divertissant sur les tendances Spotify. Le quiz mélange des questions autour des chansons les plus écoutées, des artistes les plus streamés, des genres musicaux populaires et des tendances régionales. Les utilisateurs seront invités à répondre à une série variée de questions tirées aléatoirement de ces différents thèmes.

## API Web choisie

L'application utilise l'API Spotify pour récupérer des données musicales. L'API Spotify fournit des informations sur les artistes, les pistes et les playlists. Les données sont utilisées pour générer des questions de quiz et mettre à jour les classements des utilisateurs.

- Authentification : L'application obtient un token d'accès via l'API Spotify pour accéder aux données.
- Récupération des playlists : Les playlists populaires sont récupérées pour générer des questions de quiz avec l'endpoint /v1/playlists/%s/tracks en remplaçant %s par l'id de la playlist
- Données des artistes : Les informations sur les artistes, y compris la popularité et les genres, sont utilisées pour créer des questions pertinentes avec l'endpoint /v1/artists/%s en rempaçant %s par l'id de l'artiste.

## Fonctionnalités de l'application

Les principales fonctionnalités de l'application incluent :

- Inscription et connexion des utilisateurs
- Génération de questions de quiz basées sur des données musicales
- Suivi et mise à jour des scores des utilisateurs
- Classement des utilisateurs en fonction de leurs scores
- Consultation du profil de l'utilisateur

### Quiz

L'application offre une variété de quiz sur les tendances Spotify, où les utilisateurs doivent deviner ou reconnaître les éléments musicaux les plus populaires. Voici quelques types de questions possibles de l'application :

- **Artistes les plus streamés** :Parmi 4 artistes, l’utilisateur devra choisir celui qu’il pense être le plus populaire.
- **Genres musicaux le plus représenté parmi 4 artistes** : Parmi 4 genres musicaux, l’utilisateur devra choisir celui qu’il pense regrouper le plus d'artistes.
- **Tendances régionales** :  Ce type de question comprend deux sous-types: L’utilisateur devra choisir parmi 4 pays celui où une chanson donnée est la plus populaire.
Ou l’utilisateur devra choisir parmi 4 chansons celle qui est la plus populaire dans un pays donné.


### Profil

Les utilisateurs peuvent consulter leur profil personnalisé, qui comprend les informations suivantes :

- Pseudo de l'utilisateur
- Score total
- Nombre de parties jouées
- Historique des scores par partie (les 5 dernières parties)
- Classement par rapport aux autres utilisateurs

## Cas d'utilisation classiques

1. L'utilisateur ouvre l'application SpotTrend Quizzer.
2. L'utilisateur se connecte en utilisant son identifiant et son mot de passe.
3. Une fois connecté, l'utilisateur accède à l'écran d'accueil de l'application.
4. Sur l'écran d'accueil, l'utilisateur appuie sur le bouton "Démarrer le quiz" pour commencer.
5. L'application affiche la première question du quiz.
6. L'utilisateur répond à la question en sélectionnant l'une des options proposées.
7. Après avoir répondu, l'utilisateur appuie sur le bouton "->" pour passer à la question suivante.
8. Les étapes 5 à 7 se répètent jusqu'à ce que les 7 questions du quiz soient terminées.
9. Une fois toutes les questions répondues, l'utilisateur appuie sur “Finish” et voit une page avec son score et son classement apparaître.
10. Pour consulter son profil, l'utilisateur appuie sur l'icône du profil
11. Sur la page du profil, l'application affiche le pseudo de l'utilisateur, son score total, le nombre de parties jouées, l'historique de son score des 5 dernières parties et son classement parmi les utilisateurs.

## Données stockées dans la base de données

### User

| Champ        | Description                                           |
|--------------|-------------------------------------------------------|
| UserID       | Identifiant unique de l’utilisateur                   |
| Pseudo       | Pseudonyme de l'utilisateur                           |
| Password     | Mot de passe de l’utilisateur                         |
| ScoreTotal   | Score total accumulé par l’utilisateur                |
| NbDeParties  | Nombre total de parties jouées par l’utilisateur      |
| ScoreHistory | Historique des scores récents                         |

### Artistes

| Champ        | Description                                           |
|--------------|-------------------------------------------------------|
| ArtistID     | Identifiant de l'artiste                              |
| ArtistName   | Nom de l'artiste                                      |
| Popularity   | Popularité de l'artiste                               |
| Genre        | Liste des genres musicaux de l'artiste                |


### Tracks

| Champ        | Description                                           |
|--------------|-------------------------------------------------------|
| TrackID      | Identifiant de la piste                               |
| TrackName    | Nom de la piste                                       |
| Popularity   | Popularité de la piste dans le pays                   |
| Artists      | Liste des artistes associés à la piste                |
| Country      | Pays dans lequel on a récupérer la playlist           |

### Classement

| Champ        | Description                                             |
|--------------|---------------------------------------------------------|
| UserID       | Identifiant de l'utilisateur                            |
| UserName     | Pseudonyme de l'utilisateur                             |
| scoreTotal   | Score total de l'utilisateur                            |


## Mise à jour des données et appel de l'API externe

Les données sont mises à jour de la manière suivante :

- Fréquence des mises à jour : Les données de popularité des artistes et des pistes sont mises à jour périodiquement (tous les 24h) en utilisant un ticker.
- Appel à l'API Spotify : Lors de chaque mise à jour, des appels sont faits à l'API Spotify pour récupérer les dernières données sur les artistes et les playlists.
- Insertion/Modification dans MongoDB : Les nouvelles données sont insérées ou mises à jour dans la base de données MongoDB pour refléter les informations les plus récentes.

## Description du serveur et des requêtes

L'application suit une approche Service. Voici la composition et les fonctionnalités des composants principaux :

#### Handlers HTTP :
- signUpHandler : Gère les requêtes d'inscription des utilisateurs.
- signInHandler : Gère les requêtes de connexion des utilisateurs.
- userInfoHandler : Récupère les informations des utilisateurs.
- generateQuizQuestionHandler : Génère et renvoie une question de quiz.
- finishQuizHandler : Gère la fin d'un quiz et met à jour les scores.
- getQuizResultHandler : Récupère les résultats du quiz pour un utilisateur.

#### Base de données MongoDB

Stocke les informations sur les utilisateurs, les artistes, les pistes et les classements.

## Requêtes et réponses entre le client et le serveur

- **/signup:**
    - **POST** : Inscription d'un nouvel utilisateur. Prend en charge la création d'un compte utilisateur avec pseudo et mot de passe.

    ```json
    {
        "pseudo": "user123",
        "mdp": "password123"
    }
    ```

    ```json
    {
        "message": "Utilisateur créé avec succès.",
    }
    ```
- **/signin:**

    - **POST** : Connexion d'un utilisateur spécifique.

    ```json
    {
        "pseudo": "user123",
        "mdp": "password123"
    }
    ```
    ```json
    {
        "message": "Connexion réussie",
    }
    ```

- **/userinfo :**


    - **GET** :Récupère les informations d'un utilisateur

    ```json
    {
        Headers : Authorization: Bearer <token>
    }
    ```
    ```json
    {
        "userId": 1,
        "scoreTotal": 1500,
        "lastScores": [300, 200, 400, 100, 200],
        "userRanking" [{pseudo: "bob3", scoreTotal: 3, rank: 2}]
    }
    ```

- **/generate-question :**

    - **GET** : génère une question de quiz.

    ```json
    {
    }
    ```
    ```json
    {
        "question": "Qui est l'artiste le plus populaire parmi ces artistes?",
        "choices": ["chanteur1","chanteur3","chanteur2","chanteur4"],
        "answer": "chanteur3",
    }
    ```

- **/finish-quizz :**

    - **POST** : Requête pour terminer un quiz.
    ```json
    {
        "userId": 1,
        "score": 6,
    }
    ```
    ```json
    {
    }
    ```

- **/get-result :**

    - **GET : Requête pour récupérer les résultats du quiz
    ```json
    {
        Headers : Authorization: Bearer <token>
    }
    ```
    ```json
    {
        "scoreTotal": 1500,
        "scoreHistory": [6,3,8,2,10],
        "userRanking":  [{pseudo: "bob2", scoreTotal: 10, rank: 1}, {pseudo: "bob3", scoreTotal: 5, rank: 2}],
    }
    ```


## Schema global du système

                               Utilisateur
                                    |
                                    |
                                    |
                                    V
                           +-------------------+
                           |    Application    |
                           |     SpotTrend     |
                           |      Quizzer      |
                           +-------------------+
                                    |
                                    |
                                    |
                                    V
                           +-------------------+
                           |     Serveur       |
                           |       API         |
                           |       (Go)        |
                           +-------------------+
                             /              \
                            /                \
                           /                  \
                          /                    \
                         V                      V
           +--------------------------+     +----------------------------+
           |     Base de données      |     |      API Web Spotify       |
           |    (Stockage des users,  |     |  (Récupération des         |
           |   classement, réponses)  |     |     données musicales)     |
           +--------------------------+     +----------------------------+
