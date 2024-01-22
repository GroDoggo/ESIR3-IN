Tracking -> suivre des objets mobiles
Localization -> capturer la position de la camera mobile
## Tracking
- 3D ou 2D
- Estimation d'un état à partir d'informations de l'images
**Exemple** : Transformation de l'objet sur l'image
**Mesures** : Intensité des pixels, features (gradient, key points), detection process (face, car)
**Etat** : Coordonnées, Bounding Box, 3D pose, SLAM
### Detection vs tracking
**Detection** : Sur une image indépendamment des précédentes
**tracking** : On estime en fonction du temps, le model est évolutif
### KLT
Using brightness consistency hypothesis $I_0(x) = I(x+h)$
On prend la valeur des points autour de x
Sur la nouvelle image, retrouver les même valeur de points quelques part dans l'image
### Color based tracking
Comme KLT mais cette fois si on utilise les histogrammes
On calcule la distance entre 2 histogrammes de couleurs sur un bloc
*distance de Bhattacharyya*
### Wrap function
$w(x, h)$ est une fonction de transformation du point x suivant h
*Exemple* : $w(x, h) = w+h$ -> translation
$Rx +t$ avec $R = rotationMatrix$ -> rotation
$\begin{pmatrix}a & b \\c & d\end{pmatrix}x + t$ -> affine
### Homographie estimation
$x_2 = H_1^2 * x_1$
équivalente a $x_2 * H_1^2x_{1} = 0$
### 3D Model-based tracking
Pose estimation
Small object/camera displacement between two frames
Minimiser l'erreur entre le model de l'objet et les contours de l'image
On connait la position des points dans le repère Objet
On recherche la transformée vers la camera
$$
x = \frac{(r_1 0)^wX + t_x)}{(r_3 0)^wX + t_z)} $$ $$
y = \frac{(r_2 0)^wX + t_y)}{(r_3 0)^wX + t_z)}
$$
Problème connu sous le nom PnP
Robustesse aux outliners -> Ransac ne suffit pas
1) On considère qu'on a confiance dans tout les points
2) On estime notre erreur
3) On détermine les résidus (erreur de chaque point de l'estimation)
4) Les points les plus proches gagne une très bonne confiance (et inversement)
5) On recommence en pondérant les point avec leur confiance
