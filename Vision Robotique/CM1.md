Maude Marchal (RAIMBOW)
robot = movement
## Introduction
### Les robots
First autonomous robot (1948) built by Elmer and Elsie
	Turtle moving toward source of light
First industrial robot (1956)
	**Unimate** by unimation
	Grab and put arm
First mobile robot (1960)
	With sensors
	HILARE (1970) with video camera
Best robots today
	Atlas
	Space robotics -> Perseverance
	Underwater robotics
	Medical robots

### Tracking
L'estimation d'un état
### SLAM
Créer la carte de l'environnement et utiliser cette dernier pour determiner sa position
### Motion capture
Localiser des objets dans l'environnement )à partir d'un ensemble de caméra

## Rappels
### Perspective projection
Repere de la camera Rc et C le centre optique
L'axe Z est l'axe optique
	Touche l'écran en u0 v0
	La distance entre C et (u0, v0) est la focale f
Pour connaitre X ou x (ou y/Y), on applique Thales
	$x/X = f/Z$
La droite qui passe par le point et sa projection
	fX - Zx = 0
	fY - Zy = 0
	Tout les points sur cette droite se projete au meme endroit sur l'ecran
### Sampling
Transformer de mêtre en pixel
	u = (x + x0)/lx
	v = (y + y0)/ly
	lx et ly sont la taille des pixels et (x0, v0) la translation de (u0, v0)
### Camera model
Conclusion
	$u = u0 + px*X/Z$
	$v = v0 + py* Y/Z$
A l'envers
	$x = (u - u0)/px$
	$y = (v - v0)/py$
### Coordonnées homogène
On rajoute w = 1
	(X, Y) -> (X, Y, 1)
A l'envers on divise par w
	(X, Y, W) -> (X/W, Y/W)
Point a l'infini -> w = 0
### Perspective model
$(u, v, 1) = K \pi (X, Y, Z, 1)$
### Calibration
Utilisation d'une mire dont on connait parfaitement ses paramètres
On a besoin de connaître la transformation entre le repaire de la camera et celle de la mire
Sachant que $R^t = R^{-1}$ 
### Matrice homogène
$$\begin{bmatrix}
R & t \\
0 & 1
\end{bmatrix}^{-1} = \begin{bmatrix}
R^{-1} & R^{-1}t \\
0 & 1
\end{bmatrix}$$

### Géométrie épipolaire
Quand on a un point réel projeté sur une image, ou se situe-il sur l'autre image
Projeter toute la droite *(x1 X)* sur la deuxième image -> Droite épipolaire, on sait que X se situe sur cette droite.
Les épipoles sont la projection de la camera 1 sur l'image de la camera 2 et vice-versa.
Toute les droites épipolaire passe par les épipoles.
### Disparité
Soit X un point réel projeté sur l'image 1 en *x1* et sur l'image 2 en *x2*
La disparité est la distance entre *x1* et *x2*
### Matrice essentielle
$$\begin{bmatrix}
^1t_2
\end{bmatrix}_x = \begin{pmatrix}
0 & -t_z &  t_y\\
t_z & 0 & -t_x \\
-t_y &  t_x& 0
\end{pmatrix}$$
$$^1E_2 = \begin{bmatrix}
^1t_2
\end{bmatrix}_x * ^1R_2$$
$$^1F_2 = K_1^{-T}* \begin{bmatrix}
^1t_2
\end{bmatrix}_x ^1R_2K_2^{-1}$$
### Homographie
Uniquement pour les rotations pure
$$^2H_1 = \frac{Z1}{Z2} R_1^2$$
$$x2 = H^2_1 *x1$$
