# Squelette Serveur

Adoptant une architecture orientée service plutot. Cette approche est idéale pour un système qui doit fournir des fonctionnalités dynamiques et interactives telles que l'inscription des utilisateurs, la gestion des sessions de quiz, et la mise à jour des scores en temps réel. Le serveur est conçu pour répondre aux requêtes HTTP, gérer des sessions utilisateur sécurisées via des tokens JWT, et interagir avec une base de données MongoDB pour stocker et récupérer les données nécessaires

#### Composant : signUpHandler POST
Gère l'inscription des nouveaux utilisateurs.
Fonctionnalités :
- Reçoit les données d'inscription de l'utilisateur (pseudo, mot de passe).
- Vérifie l'unicité du pseudonyme.
- Génère un identifiant utilisateur unique.
- Insère les informations de l'utilisateur dans la base de données.
- Retourne un message de succès ou d'erreur.

#### Composant : signInHandler POST
Gère la connexion des utilisateurs existants.
Fonctionnalités :
- Reçoit les données de connexion de l'utilisateur (pseudo, mot de passe).
- Vérifie les informations d'identification.
- Génère un token JWT pour l'utilisateur.
- Retourne le token et les informations sur les meilleurs joueurs.

#### Composant : userInfoHandler GET
Récupère les informations de l'utilisateur connecté.
Fonctionnalités :
- Vérifie l'authentification de l'utilisateur via le token JWT.
- Récupère les informations de l'utilisateur à partir de la base de données.
- Retourne les informations de l'utilisateur et son classement.

#### Composant : topPlayersHandler GET
Récupère la liste des meilleurs joueurs.
Fonctionnalités :
- Récupère les informations sur les joueurs ayant les meilleurs scores depuis la base de données.
- Retourne les informations sur les meilleurs joueurs.

#### Composant : topPlayersHandler GET
Génère une question de quiz
Fonctionnalités :
- Génère une question de quiz basée sur les données récupérées depuis la base de données.
- Retourne une question de quiz sous forme de JSON.

#### Composant : finishQuizHandler POST
Gère la fin d'un quiz et mettre à jour les informations de l'utilisateur.
Fonctionnalités :
- Authentifie l'utilisateur via le token JWT.
- Met à jour le score total et l'historique des scores de l'utilisateur.
- Met à jour le classement des utilisateurs.
- Retourne un message de succès ou d'erreur.


#### Composant : getQuizResultHandler GET
Récupère les résultats du quiz pour l'utilisateur connecté.

Fonctionnalités :
- Authentifie l'utilisateur via le token JWT.
- Récupère les informations du score total et de l'historique des scores de l'utilisateur.
- Récupère le classement de l'utilisateur.
- Retourne les résultats du quiz et le classement.