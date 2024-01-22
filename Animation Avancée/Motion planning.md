## Introduction
Are two points connected with a path?
Ressource : Zone interdite + Zone libre + Départ + Arrivée
Toute les positions du chemin sont dans la zone libre
Shema en 2D **mais** faire l'extension en n-D
### Objectifs
2 type de planifications
- **Chemins géométriques** -> Déterminer par ou il faut passer
- Trajectoire -> Géométrique + notion du temps (obstacle en mouvement)
Seul les chemins géométrique seront vus
Objectifs :
- Atteindre une cible sans collision avec un obstacle
### Applications
Robotique (Bras robotique)
Véhicule autonome (voiture + spatial)
Animation par ordinateur (jeux et films)
Chirurgie
Biologie moléculaire
### Exemple (difficultés)
Prendre les lunettes -> Quand les bras se connectes on a **une chaine fermée** (on peut connecter un épeule à elle-même en passant par les lunettes et l'autre bras)
Robotique -> **gestion de l'équilibre** / **etude dynamique** (en simulation, peut importe la posture, le robot est en équilibre mais en réalité non)
Alpha puzzle
### Problèmes
Déménageur de piano
- Je veux faire bouger le piano a A vers B sachant que je dois le faire tourner dans des couloirs
## Définitions
On a en entrée :
- un système mécanique : Géométrie et Mobilité
- un environnement
- Une configuration initiale et finale (état de la chaine)
On veut calculer un chemin sans collision pour lier la configuration initiale et finale
### Configuration
Vecteur généralise
Dimension -> nombre de degrés de liberté
#### Espace de configuration
Contient toute les configurations possibles
(Si le nombre de dimension est bas) On peut le représenter (2D -> graphe) (Courbe -> suite de points -> animation)
### Chemin et trajectoire
Chemin -> Séquence de configuration
Trajectoire -> Séquence de configuration avec notion temporelle
### L'espace libre (C-free)
Ensemble des configuration **qui ne sont pas en collision** avec les obstacles
C-obstacles -> Ensemble des configuration **avec collision** avec les obstacles
Possible de la visualiser en dilatant les obstacles (CAS DU CERCLE, avec un objet complexe la dilatation est différente)
C-space = C-free + C-obstacle
Un C-space est un espace de configuration
dim(C-space) = nb degrés liberté du mobile
Les composantes connexes du C-free dans C-space montre les chemins possible (si depart et arrivée ne sont pas dans la meme composante connexe -> pas de chemin)
## Approche déterministe
Prendre l'espace et le représenter par une grille
Chaque case de la grille est C-free ou C-obstacle
**Problème** : un petit objet peut être mal représenté, un passage peut être obstrué si il est trop petit (exemple de la porte)
**Pros** -> facile, rapide
**Cons** -> Mauvaise précision, gros temps de recherche dans des espaces à beaucoup de dimensions (graphe gigantesque)
Peut être améliorer -> Quadtree, Octree, représentation hiérarchique
### Représentation exacte
Principe : Décomposer C-free en cellule de géométrie simple
#### Exemple : Cellules verticale
de haut en bas de meme aire
represente exactement C-free (pas de probleme de porte)
Application -> passage par centre de cellule
attention -> ne représente pas le chemin optimal de l'environnement
#### Exemple : Triangulation Delaunay
Toute les somment sont relié en triangle
le cercle circonscrit des triangle ne contient que leur propre sommets
dans ce cas, un sommet est tj relié à son plus proche voisin
**avec contrainte** : les obstacles forment des segments de contraintes -> le coté d'un trianagle ne peut pas passer par une contrainte
peut être utiliser pour trouver les goulée d'étranglement
	- si une goulée est plus petite que la taille du mobile -> ne passe pas on peut simplifier le graphe
#### Exemple : diagramme de Voronoi
Dual de la triangulation de Delauney
Chaque points du diagramme est équidistant des 2 sommets les plus proches
Permet de trouver facilement le sommet de plus proche de chaque position
**avec contrainte** : Si on suit une ligne, on est toujours le plus loin possible des obstacles (robotique)
Pour chaque sommet d'obstacle, on fait un cone de profondeur. Les crevasse indique les droites de Voronoi
### Potential field
Uniquement sur C-free
pousser le mobile le plus loin possibles des obstacles (obstacles = répulseur)
tirer le mobile vers l'objectif (objectif = attracteur)
**pros** 
- attracteur et répulseurs peuvent être modifier au cours du temps
- planification et controle en une seule fonction 
- possibilité d'amélioration (local)
**cons**
- contraint au minimums locaux
### Planificateur a haute dimension
La complétude idéale consiste a donner une solution en un temps fini si elle existe ou indiquer qu'il n'y a pas de solution
Attention -> toujours selon la représentation du graphe
Complexity polynomiale en espace (PSPACE complet)
**solutions** 
- réduire le nombre de dimension
- ajouter des contraintes, réduire le volume de recherche
- sacrifier optimalité (je ne calcule pas le chemin le plus court)
- sacrifier la complétude (si je trouve un chemin c'est qu'il existe, si j'en trouve pas je ne peux plus dire qu'il en existe pas)
**idée**
- échantillonner aléatoirement l'espace
- construire la structure à partir de cet échantillonnage
plus efficace pour remplir l'espace mais sacrifie optimalité et complétude (compromis qualité et performance)
#### PRM : Probabilistic RoadMap
dans la diapo : Représentation 2D d'un espace ND
- un segment est un chemin d'interpolation pour la configuration
- les points sont des configurations
Principe -> Exploration aléatoire de C-free pour capturer sa topologie
Complete en temps infinie
##### Exploration phase
1. Compute random configurations
	- Detection de collisions -> si aucune on garde la configuration
2. Link configuration with knn neighbors (vp-trees)
	- Utilisation de la méthode locale pour déterminer l'interpolation
	- Si collision -> on stocke pas
	- Si pas de collision -> on garde
3. Recommencer a 1
![[Pasted image 20231206100242.png]]
##### Query phase
1. Connect init and final configuration points with road map
2. If it can be connected, a solution exist.
	- IF NOT, UNE SOLUTION EXISTE PEUT ETRE QUAND MEME
3. Search solution
4. Optimize
![[Pasted image 20231206100420.png]]
![[Pasted image 20231206101030.png]]
**problème du PRM** -> Enorme consommation de mémoire, temps de construction grand, recherche lente
![[Pasted image 20231206102426.png]]
alternative pour optimiser : **Visibility PRM** et Gaussian PRM
![[Pasted image 20231206102452.png]]
#### Visibility PRM
Domaine de visibilité : Ensemble atteignable a partir d'un point de configuration
*Visibility domain of a configuration q ![[Pasted image 20231206102703.png]]*
On tire des configuration qui ne sont pas dans le meme domaine de visibilité
objectif -> augmenter le domaine de visibilité
![[Pasted image 20231206102807.png]]
Ces configuration sont appelle gardiens
![[Pasted image 20231206102841.png]]
On tire maintenant des configurations qui connectent au minimum deux gardiens
On les appelle des connecteurs
![[Pasted image 20231206103147.png]]
#### RRT : Rapidly exploring Random Trees
PRM -> multiples queries, same roadmap for all queries
RRT -> structure only use for one query
##### Iterative algorithm
1. Compute qrand
2. Connect to qnear
3. Insert qnew
4. go back to 1
![[Pasted image 20231206103747.png]] ![[Pasted image 20231206103801.png]] ![[Pasted image 20231206103820.png]] ![[Pasted image 20231206103854.png]] ![[Pasted image 20231206103910.png]] ![[Pasted image 20231206103917.png]] 
Par construction, l'arbre ne reviendra quasi jamais sur ces pas
