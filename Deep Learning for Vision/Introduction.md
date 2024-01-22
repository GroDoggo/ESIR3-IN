## Prérequis
- Supervised learning
- Different model
- Underfitting, Overfitting
- Train Val Test set
- Optimization : loss functions, regularization gradient descent
- Evaluation : empirical/real error, cross validation
- CNN
	- conv pool fully-connected layers
	- parameters hyper-parameters

## Image classification
Donner un label à une image
Pour chaque couche, on donne un poids qu'il faut estimer (minimiser l'erreur)
**activation function** : $g(y) = max(0,y)$
**stacking layers** : couche ($w_1$) -> activation function -> couche ($w_2$) -> ...
Chaque couche est une simple combinaison linéaire de poids $w_1$
Sur le dernier layer, on applique la fonction **SoftMax** pour obtenir une probabilité d'une classe. (avec température T parfois)
	*Grand T -> uniform distribution
	Small T -> sharper distribution*
**classification loss function** : $h(y, j) = - \sum y_k*log(j_k)$ avec $j = f(x)$
Pour résumer : image -> encoder (layers) -> classifier (SoftMax) -> result

## Regularisation
Beaucoup trop de paramètres dans un réseaux de neurones -> overfitting facile
1) Limiter le nombre de neurones
2) Dropout -> désactiver des neurones aléatoires
4) Normaliser les layers avant chaque activation
5) Weight decay -> rajouter un offset aux poids de couches
6) Augmenter la data via des transformations (mirror/crop/rotation)
	- Mix-up : mélanger (linéairement) deux images de classes différentes. Le classifieur doit retrouver les bonnes probabilités.
7) Distillation
	- On prend un model pré entrainé (teacher) qu'on fait passer un dataset. On train notre model (student) avec ce meme dataset.
	- On prend $y=teacher(x)$ et $j=student(x)$.
	- $DisstilationLoss = H(y, j)$
	- On a toujours le $StudentLoss$ en suivant la parcours classique
	- On chercher a minimiser les deux $DisstilationLoss$ et $StudentLoss$

## Application
### Object detection et localisation
**input** : image
**output** : class info (vecteur de taille X) + bounding box (vecteur de taille Y)
On peut rajouter une data du style *IsThereAnObect* et la fonction Loss change de cette data.
