# Q_Learning_simple

Implémentation d'un environnement personnalisé et application du Deep Q-Learning pour déterminer une policy pour résoudre le jeu.

## Environnement 

L'environnement sera basé sur la librairie gym créer par openIA , que l'on peut retrouver ici : https://www.gymlibrary.dev/ et installer avec la commande **pip install gym** ,
Il est composé d'un terrain carré de taille 6x6 initialisé par des cases vides numérotées par des 0 de couleur blanche, un agent représentant le joueur numéroté par un 1 de couleur bleue avec une position de départ aléatoire, et la position de victoire représentée par un 2 de couleur verte à la position (3,5).

Représentation d'un état 

<img width="393" alt="Capture d’écran 2024-05-16 à 11 13 48" src="https://github.com/JeromeUwU/Q_Learning_simple/assets/127997538/f22c813b-ec2e-41e1-8220-b0ad6931fe30">


L'agent peut éffectuer 4 actions :

- UP == 0
- DOWN == 1
- LEFT == 2
- RIGHT == 3

L'objectif est de partir d'une position de départ aléatoire en **Bleu** et de rejoindre la position de victoire en **Vert** en un certain nombre de coup X.

Le système de récompense est défini comme suit:
- Si l'agent reste sur la même position il gagne -0,5 point
- Si l'agent n'atteint pas la position de victoire en moins de X coups il gagne -2 points
- Si l'agent atteint la position de victoire en moins de X coups il gagne 1 point
- De plus pour encourager l'agent à explorer, il gagne 0.01 point pour un déplacement

Le jeux s'arrete si l'agent atteint la position de victoire en moins de X coups ou si l'agent n'atteint pas la position de victoire en moins de X coups.

L'environnement est défini dans la classe *BasicEnv()* doté de plusieurs méthodes:
- *__init__* qui initialise l'état du jeux (position du joeur, terrain, action,...)
- *__step__* qui éffectue une action parmi les 4 définie
- *__reset__* qui va réinitialisé le jeux apres victoire ou défaite
- *__render__* pour visualisé le jeux


L'environnement est basé sur le travail de Paul Swenson accessible ici : https://github.com/PaulSwenson2/ReinforcementLearningProjects/blob/main/BasicEnvironment/BasicEnvironment.py

## DQL

Deep Q-Learning (DQL) avec  epsilon-greedy est un algorithme de reinforcement learning populaire combinant Q-learning et l'epsilon-greedy policy.
Cette algorithme utilise un agent pour apprendre l'action optimal à choisir dans un environnement basé sur un processus de décision Markovien.

1- Initialisation:
  - Initialiser le Q-Network et Target-Network avec des poids et biais aléatoire
  - Initialiser la Memory Replay
  - Définir les Hyperparamètres
    
2- Intéraction agent-environnement:
  - L'agent recoit une observation *o* de l'environnement à chaque step
  - Avec une probabilité ε sélectionner une action aléatoire *a* sinon choisir l'action avec la plus grande Q-value.

3- Executer l'action:
  - Esexuter l'action *a* et observer la récompence *r* et le nouvel états *o_2*

4- Sauvgarder l'expérience:
  - Sauvgarder (*o*,*a*,*r*,*o_2*) dans la replay memory
    
5- Mini-Batch:
  - Mélanger un mini-batch d'éxpériences (*o*,*a*,*r*,*o_2*) dans la replay memory

6- Calcule de la target Q-Value:
  - Pour tout éxpérience (*o*,*a*,*r*,*o_2*) dans le mini-batch calculer la target Q-Value
    
7- Mise à jour du réseau:
  - Calcule de la loss entre predicted Q-values et target Q-values
  - Optimisation du réseau par descente de gradient

8- Mise à jour du Target-Network:

9- Repeter les opérations 2-8 pour un certains nombres d'épisodes

Pour plus d'information sur le méchanisme théorique de la Q-learning : https://en.wikipedia.org/wiki/Q-learning
Pour plus d'information sur le méchanisme théorique de l'epsilon-greedy : Sutton, R. S. & Barto, A. G. 1998 Reinforcement learning: an introduction. Cambridge, MA: MIT Press.











