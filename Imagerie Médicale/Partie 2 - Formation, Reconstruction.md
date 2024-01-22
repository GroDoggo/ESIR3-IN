## Préambule mathématique
### Transformée de Radon
Projection en fonction d'un angle
$R(f(x, y)) = P(p, \theta) = \int_{-inf}^{+inf}f(p*cos\theta - q*sin\theta, p*sin\theta + q*cos\theta)dq)$
![[Pasted image 20231203101832.png]]
![[Pasted image 20231203102218.png]]
![[Pasted image 20231203102224.png]]
Représentation de la transformée -> Sinogramme
*astuce : la dernière colonne est forcement l'inverse la première*
Un scanner donne au final des sinogramme d'une transformée de Radon
### Théorème de Radon
Il est possible de faire l'inverse d'une transformée de Radon mais il faut une infinité de projection.
#### Théorème de la coupe centrale
La transformé de Fourier 1D de la projection parallèle d'un object dans une direction theta+pi/2 est égale à la coupe de transformée de Fourier 2D de cet objet la long de la droite passant par l'origine des fréquence et incliné d'un angle thêta.
![[Pasted image 20231203102618.png]]
**problème** -> il faut une infinite de projection
**amélioration possible** : rétroprojection par interpolation (couteux en calcul)
## Autres Reconstruction
**IRM** Directement donnée par la transformée de Fourier inverse
**Echo** Image donnée par la distance

