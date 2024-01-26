## Intro
3 grandes actions :
- Choix de l'action (Stratégie, Objectif)
- Choix du chemin (Steering)
- Pratique de mouvement (Animation, articulation)
## Model
![[Pasted image 20240125150711.png]]
Basé sur le schéma d'Euler
Steer force -> différence entre la force désiré et la force courante
Problème de contrôle a cause de l'inertie
### Seek and flee
Aller ou s'éloigner d'un point
![[Pasted image 20240125151207.png]]
![[Pasted image 20240125151212.png]]
**A l'arrivée** :
A l'intérieur d'un rayon autour de la cible -> % de deceleration
![[Pasted image 20240125151612.png]]
### Scénario de poursuite et évasion
On projette la position de la cible dans le futur
Extrapolation linéaire
Adaptation avec la position prédite
### Evitement d'obstacles
On évite des cercles
Un obstacle est a éviter si sa distance avec la trajectoire est inférieur a un seuil
Calcul d'une nouvelle vitesse tangente a l'obstacle![[Pasted image 20240125153911.png]]
### Wander
Balade aléatoire
![[Pasted image 20240125154604.png]]
### Suivi de chemin
![[Pasted image 20240125154942.png]]
## Champ de mouvement
![[Pasted image 20240125155237.png]]
## Evitement de collision sans alignement
![[Pasted image 20240125155402.png]]
![[Pasted image 20240125155411.png]]
## Navigation de groupe
Structure de voisinage -> récupérer ses voisins
Force de séparation
![[Pasted image 20240125162731.png]]
Force de cohésion
![[Pasted image 20240125162746.png]]
Force d'alignement
![[Pasted image 20240125162757.png]]
Chaque force est lié à un poids, la combinaison des trois donne la force finale
