# Squelette Client

#### Technologies clients

React est utilisé pour gérer l'état des différents quiz, afficher les questions, les options de réponse, et les résultats (si le choix est vrai ou faux) en temps réel sans recharger la page. 
Le flux d'état est géré localement dans les composants, et le passage d'informations se fait via les props et les hooks comme useState et useEffect.

React Router est employé pour la navigation entre les pages, permettant ainsi aux utilisateurs de se déplacer aisément entre la page de connexion (SignInPage), d'inscription (SignUpPage), la page d'accueil (HomePage), le quiz (QuizPage), la page des résultats (ResultPage) et la page de profil (ProfilePage).

#### Plan des pages

- App : Sert de point d'entrée où les utilisateurs peuvent choisir entre s'inscrire et se connecter.
- SignInPage/SignUpPage : Pages pour l'authentification des utilisateurs, qui gèrent les soumissions de formulaires et les validations.
- HomePage : Sert de point d'entrée où les utilisateurs peuvent commencer un quiz et consulter le classement du TOP5 des utilisateurs.
- QuizPage : présente les questions et gère la logique du quiz.
- ResultPage : affiche les résultats de l'utilisateur à la fin du quiz.
- ProfilePage : montre les informations de l'utilisateur, son historique de jeux et son classement.