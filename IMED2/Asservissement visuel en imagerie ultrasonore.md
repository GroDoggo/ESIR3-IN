Alexandre KRUPA -> INRIA Rainbow
Asservissement -> déplacer un système robotique de manière automatique
## Différents type de systèmes en robotique médicale
Objectif  : Assistances du clinicien
- Système télé-opérés -> Duplication du geste médical (Da Vinci)
- Système de co-manipulation -> L'outils est manipulé par le chirurgien mais porté par le robot (éviter les tremblements)
- Système semi-autonome ou autonome -> intervention quasi ou entièrement automatique
Dans ce cours -> système semi-automatique ou autonome avec guidage a partir d'image
## Robots médicaux guidés par l'image
### Pre-opératoire
Trajectoire du robot précalculé à partir d'une planification
Les images ont été prise avant l'opération
**problème** : toute les images sont le référentiel du capteur -> pendant opération, mettre en lien le repère du capteur et du robot -> recalage
pendant l'opération, pas de capteur dans le robot, donc pas de garantie
**pro** : modalité d'image non temp-réel (lente) possible
**cons** : précision sensible aux erreurs d'étalonnage et recalage et LE PATIENT DOIT RESTER FIXE
### Per-opératoire
Trajectoire du robot calculé pendant l'opération
Contrôle du robot en boucle fermé par retour visuel (se corrige en fonction du retour image)
**pro** : haute-précision (celle de l'image) et compensation du mouvement psysiologique (mouvement des organes)
**cons** : cadence d'image rapide (25fps min), traitement d'image en temps réel et robuste
## Les modalités d'imagerie médicale
- Imagerie optique (camera) invasive
- IRM (Résonance magnétique) non temps réel
- Scanner X (rayons X) ionisante et non temps réel
- Echographie (ultrasons) mauvaise qualité
Le meilleur choix pour un guidage robotique non invasif -> **echographie**
## Formation de l'image
Principe -> emmètre une onde acoustique dans le patient (ultrasons) et réception de l'echo (rebond)
Emetteur -> Elément céramique piézo-électrique (PZT) qu'on excite par impulsions électrique pour créer une onde
Récepteur -> le meme PZT qui convertit l'onde en signal electrique
Après recepteur, echantillonage et quantification (TS) pour générer l'image
vitesse de propagation $c=Z/p$
Z -> impédance accoustique
p -> masse volumique
Chaque tissus du corps possède une impédance acoustique différentes (+ impédance -> + vitesse)
Intensité de l'onde lors de la propagation $I(d) =I_0e^{\mu d}$ 
I0 -> intensité initiale
$\mu$ -> coefficient d'absorption du milieu
Le coefficient d'absorption est en fonction de la fréquence de l'onde et constante propre au milieu
- fréquence faible -> structure profonde mais mauvaise qualité
- fréquence élevée -> structure peu profonde mais bonne qualité
![[Pasted image 20231127104209.png]]
Intensité de l'echo refléchi : $I_r = R*I_i$ 
avec R coefficient de réfléxion
si coefficient >40% -> impossible d'explorer les structure plus profonde
**attention dans le cas ou l'onde n'est pas perpendiculaire**
![[Pasted image 20231127105058.png]]
$\frac{sin\theta _t}{\sin\theta_{i}} = \frac{c_{2}}{c_{1}}$
### Mode d'aquisition A (Amplitude)
Amplitude des échos renvoyés sur une simple ligne de tir
Ne fournit as d'image 2D mais un signal 1D en fonction de la profondeur
### Mode d'aquisition B (Brillance)
Fournit une image 2D
Mode A avec un balayage sur plusieurs ligne de tir
pixel de l'image -> amplitude de l'écho
### Mode Doppler
Permet de mesure la vitesse du sang dans les veines
mesurer la différences de fréquence
si onde écho > onde émise -> interface rencontrée se rapproche
sinon -> interface rencontrée s'éloigne
*exemple du camion de pompier*
Possibilité de superposé mode B et Doppler
## Type de sondes
### Sonde 2D
les + répandues
plusieurs formes en fonction de la cible
convexe -> zone d'observation large et profonde
linéaire -> grande résolution mais faible profondeur
### Sonde bi-plans
2 barrettes -> 2 images 2D orthogonales
### Sonde 3D à balayage motorisé
Sonde 2D avec moteur
Volume reconstruit par interpolation
Large champs visuel mais gros temps d'aquisition
## Asservissement visuel
Utilise nu capteur extéroceptif (capteur qui peut effectuer des mesures sur l'environnement d'un robot)
- Camera (visible, rayon X)
- Echographie
- et bien d'autres
Objectif -> asservir la position d'un objet poluarticulé de manière visuelle
Deux type :
- Capteur embarqué (capteur sur le robot)
- Capteur déporte (Pas sur le robot)
![[Pasted image 20231128095052.png]]
Commande en boucle fermé par retour visuel
![[Pasted image 20231128095153.png]]
s -> informations 2D/3D (coordonnées de points, paramètre des droites, etc.)
s* -> information désirée
objectif -> minimiser e = s-s*
ds = L \* v
avec ds la dérivée de s
v la vitesse du robot
L la matrice d'interaction
**Loi de commande classique** (décroissante exponentielle de l'erreur visuelle)
![[Pasted image 20231128095823.png]]
1. Description de la tache robotique
	- Tache de positionnement : atteindre une consigne fixée
	- Tache de suivi : atteindre une consigne variable
	- Tache de compensensation de mouvement : maintenir l'info visuelle initiale
2. Choix des infos visuelles
	- Pouvant être extraite de manière robuste
	- Eviter le couplage (info qui se relient entre elles)
3. Modélisation de la matrice d'interaction
4. Synthèse d'une loi de commande
### Problèmes
- Faible qualité d'images
- Déformation due au mouvement physiologique
- Est uniquement sur un plan de coupe (pas de Z)
- 3 DDL hors plan (malgré 3DDL dans plan)
 ![[Pasted image 20231128100528.png]]
Il faut avoir un connaissance du modèle 3D de l'objet étudié
## Méthode générique
Contrôle des 6DDL d'une sonde embarquée
### approche directe
- Pas de segmentation ou traitement
- Intensité des pixels de l'image directement considérée
s = I = (I11, I12, ..., Inm)
**matrice d'interaction**
ds = dI = L \* v
On fait l'hypothese qu'il n'y a pas de variation d'intensité peu importe la variation de l'angle
**conservation d'intensité** -> I(**X + dX**, t + dt)-I(**X**, t)=0
**dev de Taylor** -> dI/dt + dI/dx + dI/dy + dI/dz = 0
dI = -deltaI \* dX
avec deltaI = (dI/dx, dI\dy, dI/dz) 
dx = Lx \* v
avec Lx = $\begin{pmatrix}-1 & 0 & 0 & 0 & -z & y \\0 & -1 & 0 & z & 0 & -x \\0 & 0 & -1 & -y & x & 0\end{pmatrix}$
**rappel** -> z = 0
L1 = -deltaI \* Lx
Pour obtenir dI/dx ect, on applique les filtres dérivatifs sur un volume de 3 coupes d'image (antérieure, actuelle et suivante)
**estimation de z**
![[Pasted image 20231128104526.png]]
## Tache de positionnement
![[Pasted image 20231128105801.png]]
## Tache de suivi d'une coupe anatomique
- Délimitation d’une région d’intérêt (motif) à suivre dans l’image initiale
- Loi de commande avec :
	- Infos visuelles désirées = intensité des pixels de la région d’intérêt initiale
	- Infos visuelles = intensité des pixels de la région dans image courante
	- Matrice d’interaction constante obtenue à la position désirée
- Gradient 3D estimée uniquement pour image initiale=désirée
	- avec filtres dérivatifs appliqués sur 3 coupes parallèles
- Contrôle de 5 DDL par vision
- _Contrôle de 1 DDL par commande en effort pour maintenir contact sonde/patient_


