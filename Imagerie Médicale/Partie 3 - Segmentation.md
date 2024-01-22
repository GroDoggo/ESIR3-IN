Segmentation -> Quantifier des volumes, Localiser un objet
## Approches modèle globales
### Seuillage
Exemple le plus simple
Plusieurs solution possible pour déterminer la valeur du seuil
	Généralement basé sur l'histogramme
### k-means
trouver les X points de "gravite"
1) Chaque pixel est associé à sa graine la plus proche
2) On recalcule les graines en fonctions de leurs pixels associé
### Seuillage adaptatif
On divise l'image en sous-région
On applique une seuillage différents sur chaque région
### Bilan
Simple, rapide, pas d'info de connexité
## Approche modèle région
### Region growing
On plante une graine
Tant que le voisin a une différence inférieure à un seuil, le voisin est de la meme classe.
### Split and merge
On créer une partition de l'image de façon récursive
On mélange les partitions qui se ressemble
### Markoviennes
Utilise la formule de Bayes
On cherche l'image qui maximise le proba P(u|f)
Algorithme de metropolis pour échantillonner les proba
### Graph-cut
Chercher une coupe de poids minimale
Problème P 
La coupe minimale passe par les arrête saturée
## Approche modèle contour
Importante variation d'intensité
### Gradient
Différence avec ses voisins
Seuillage par gradient
### Détecteur de Canny
Ne garder que les maxima locaux (dans la direction du gradient) et supérieur à un seuil.
**hystérésis** : segmentation avec deux seuils
### LaPlacien
La ou le LaPlacien de l'image passe par zéro.
### Watershed
### Contour actif
On cherche la forme qui minimise l'énergie
![[Pasted image 20231203104335.png]]
## Approches données
Machine Learning
**Input** -> image
**Output** -> image segmentée
Réseaux de neurones profond
