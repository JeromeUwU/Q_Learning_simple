# Q_Learning_simple

Implémentation d'un environnement customisé et application de la Deep-Q-Learning pour détèrminer une policy pour résoudre le jeux

## Environnement 
L'environnement sera hérité de la librairie gym créer par openIA , que l'on peut retrouver ici : https://www.gymlibrary.dev/ et installer avec la commande **pip install gym** ,
Il est composé d'un terrain carré de taille 6x6 initialisé par des cases vide numéroté par des 0 de code couleur blanc , un Agent représentant le joueur numéroté par un 1 de code couleur Bleu avec une position de départ aléatoire, et la position de victoire représenté par un 2 de code couleur vert à la position (35,35).

Représentation d'un état 

<img width="393" alt="Capture d’écran 2024-05-16 à 11 13 48" src="https://github.com/JeromeUwU/Q_Learning_simple/assets/127997538/f22c813b-ec2e-41e1-8220-b0ad6931fe30">


L'agent peut éffectuer 4 actions :

- UP == 0
- DOWN == 1
- LEFT == 2
- RIGHT == 3

L'objectif est de partir d'une position de départ aléatoire en **Bleu** et de rejoindre la position de victoire en **Vert** en un certain nombre de coup X.

Le système de récompense est définie comme suit:
- Si l'agent reste sur la même position il gagne -0,5 point
- Si l'agent n'atteint pas la position de victoire en moins de X coup il gagne -2 points
- Si l'agent atteint la position de victoire en moins de X coup il gagne 1 point
- De plus pour encouragé l'agent à explorer il gagne 0.01 point pour un déplacement

Le jeux s'arrete si l'agent atteint la position de victoire en moins de X coup ou si l'agent n'atteint pas la position de victoire en moins de X coup

L'environnement est défini dans la classe *BasicEnv()* doté de plusieurs méthode:
- *__init__* qui initialise l'état du jeux (position du joeur, terrain, action,...)
- *__step__* qui éffectue une action parmi les 4 définie
- *__reset__* qui va réinitialisé le jeux apres victoire ou défaite
- *__render__* pour visualisé le jeux

L'environnement est basé sur le travail de Paul Swenson accesible ici : https://github.com/PaulSwenson2/ReinforcementLearningProjects/blob/main/BasicEnvironment/BasicEnvironment.py

## DQL

Deep Q-Learning (DQL) avec  epsilon-greedy est un algorithme de reinforcement learning populaire combinant Q-learning et l'epsilon-greedy policy.
Cette algorithme utilise un agent pour apprendre l'action optimal à choisir dans un environnement basé sur un processus de décision Markovien.

1- Initialisation:
  - Initialiser le réseaux avec des poids et biais aléatoire
  - Initialiser la Memory Replay
  - Définir les Hyperparamètres
    
2- Intéraction agent-environnement:
  - L'agent recoit une observation de l'environnement à chaque step
  - Avec une probabilité &psi; | &#968; | Greek small letter psi | ψ | 










