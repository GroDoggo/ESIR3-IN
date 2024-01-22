## Introduction
le **recalage** est une technique qui consiste en la mise en correspondance d'images, dans le but de comparer ou combiner leurs informations respectives
### Principe
On donne un critère de similarité qui mesure la resemblance entre deux image.
On donne également un famille de transformation
## Critère de similarité
### Histogramme conjoint
Histogramme classique -> Pas d'information spatiale
Histogramme conjoint -> $Card((x, y) | I(x, y) = i * J(x, y)=j)$
Pour les pixels qui valent x dans l'image I
	Yen a A qui valent j1 dans J
	Yan a B qui valent j2 dans J
	...
Divisé par le nombre de pixel -> probabilité
**recalage** -> *argmin H(I, J)*
#### Problème
**Extrapolation** : On ne prend pas en compte les pixels qui tombent en dehors de l'image
**Interpolation** : Plus proche voisin ou moyenne pondérée (Attention a bien comparer avec T(J) si on applique la transformation sur I)
### Conservation de l'intensité
SSD(T) = $\sum_{x, y} (I(x, y) - J(T(x, y)))^2$
**Avec Histogramme joint** -> SSD(A, B) = $\sum_{ij}H_{A, B}(i, j)(i-j)^2$
#### Problème
Marche uniquement lorsque l'image recalé est exactement la même que celle désiré
Même patient et même modalité
On doit supposer qu'elle ont la meme intensité une fois recalé
### Dépendance linéaire ou affine
Lorsque J = $\alpha I + \beta$
L'histogramme conjoint est une droite de paramètres alpha et beta
**Critère adapté** -> coefficient de corrélation
p(I, I) = 1
p(I, -I) = -1
p(I, $\alpha I + \beta$) = signe de $\alpha$
#### Problème
Différents patients mais même modalités
### Dépendance statistique
On utilise la probabilité de l'histogramme joint
**Information mutuelle** -> $\sum_{x, y}p(x, y)\log\left( \frac{p(x, y)}{p(x) p(y)} \right)$
Si I est indépendant de J ->p(I, J) = p(I)p(J) -> IM(I, J) = 0 (c'est réciproque)
Plus la distance entre p(X, Y) et p(x)p(y) est grande, plus les images sont liés
On suppose que l'intensité des images recalé sont dépendantes
## Transformation
### Transformation linéaires
**Rappel** -> Passer en coordonnées homogènes
#### Transformation rigides
Compenser le mouvement d'un patient
**M sujet et modalité**
#### Similitudes et transformations affines
Corriger la resolution spatiale
**M sujet mais modalité différentes**
### Transformation non-linéaires
Source - Cible -> si contour bizarre alors non recalé (ou evolution du sujet)
Transformation linéaire ne permet pas les parties complexes (pas de transformation élastique)
Choix des points de contrôle
On applique un vecteur déplacement par pixel/voxel
Beaucoup de paramètres -> 3N
On rajoute (en plus du critère de similarité) un critère de regularization
La somme des trois gradient (X, Y, Z) est le plus petit possible
- Si je recale I sur J, je dois obtenir l'inverse de si je recale J sur I
- Limiter l'amplitude des déplacements
**différents patient et modalités**
## Optimisation
Etant donner un critère de similarité, comment trouver la meilleure transformation?
### Exemple SSD + Transformation 2D
On cherche $\vec{t} = (p,q)$ qui minimise $\sum (I(x, y) - J(x+p, y+q))^2$
**Descente de gradient**
- Partir d'une initialization (p0, q0)
- $p_{k+1} = p_{k} - \alpha  \frac{\nabla SSD}{\nabla p}(p, q)$
- On s'arrete quand la diff est inférieure à un seuil (minimum global/local)
$$
\frac{\nabla SSD}{\nabla p}(p, q) = 2 \sum (I(x+p, y+q)-J(x,y))^2 * \frac{\nabla}{\nabla p}(x+p, y+q)
$$
### Avec Rotation
Pareil mais un seul paramètre $\theta$
### Transformation rigide
Différence de pente entre la translation et rotation
Ne pas utiliser la méthode classique
#### Approche hiérarchique
Effectuer un recalage rigide -> affine -> non-linéaire
### Approche géométrique
- Extraction les primitives géométrique (points caractéristiques)
	- Segmentation
- Trouver la transformation optimale
	- On cherche la transformation qui fait correspondre le plus de points
	- Méthode des moindres carré
