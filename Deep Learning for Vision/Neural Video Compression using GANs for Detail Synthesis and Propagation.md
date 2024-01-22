## Abstract
Neural video compression GAN
GAN loss is crucial
- Synthesize details
- Propage this detail
User studies
## Introduction
Anciennement, les neural network arrive a égaler voir dépasser les performances des standard comme HEVC sur les distortion (PSNR, SSIM)
Par contre, sur des débits bas les reconstruction vidéo sont floue (neural) ou block (non-neural)
Idée : Ajouter une contrainte de "réalité", s'assurer que la reconstruction reste réaliste (tout en restant proche de l'input) -> 3-facteur (debit-distortion-réalisme)
-> mise en place d'un GAN
Seulement mis en place pour des images -> peu exploré dans le cas des vidéos (trop difficile, train dur)
Pour appliquer 3 facteurs, on a besoin de synthétiser les détails et de les propager quand du nouveau contenu apparait
-> mise en place d'un reseau generatif
**problème** -> on ne peut pas mesurer le réalisme avec le PNSR et SSIM
**solution** -> user studies pour trouver le meilleur compromis
### Contributions
1. Premier GAN de compression video qui dépasse les standard H264, H265 (loss très importante)
2. Condition pour une loss efficace :
	1. Laisser autant de bits possible pour synthetize les détails
	2. Pouvoir propager les détails
## Conclusion
Grace aux users studies, deux composantes sont cruciales :
1. Conditionner le résidu sur la reconstruction précédente
2. Utiliser un flow adéquat
Decoupler scale space warping afin d'utiliser une reconstruction de haute qualité
Utiliser un débit de contrôle adaptatif pour assurer un bitrate constant avec beaucoup d'hyperparametre
### Limitation
Il existe quasi peu de métrique et il est nécessaire de se rattacher à des user studies
C'est cher et pas très consistant
Nécessaire de trouver cette métrique
## Related Work
### Neural video compression
1. *Wu et al.* - Compression des B-frames par interpolation
2. *Djelouah et al.* - interpolation et flow optique prédiction
P-frame only
3. *Lu et al.* - Utilise frames précédente dans un flow optique
A FINIR

## Method
![[Pasted image 20240110110322.png]]
![[Pasted image 20240110110345.png]]
### Overview
 $x = \{x_1, x_2, ...\}$ une séquence de frames
 $x_{1} = x_{I}$ est la la frame initiale (I frame)
Pas de B frames
$\hat{x} = \{\hat{x_{1}}, \hat{x_{2}}, \dots\}$ la séquence reconstruite
**Stratégie**
1. Synthétiser les détails sur $x_1$
2. Propager les détails partout ou cela est possible
3. Quand du nouveau contenu apparait, synthétiser les détails
#### I branch (x1)
$x_1$ passe dans un encodeur CNN qui le quantifie en un espace latent $y_1$
On compresse alors $y_1$ en utilisant un hyperprior $p(y_1)$ (pas utilisé par la suite)
En utilisant $y_1$ (et non $p(y_1)$), on peut obtenir une reconstruction $\hat{x_{1}}$ avec le générateur $G_I$
Pour entrainer le générateur, on utilise un discriminator
#### P branch (reste)
Calcul du flow entre deux frames avec Uflow -> $F_t$
Quantifie et compresse le flow dans un espace latent $y_{t, f}$
On obtient un reconstruction du flow $\hat{F_{t}}$ et un maque $\sigma_{t}$ avec le générateur $G_{flow}$
Ensemble il passe dans le decoupled scale-space warping pour obtenir une reconstruction $\hat{x_{t}}^{w}$
**Attention** cette reconstruction est très probablement flou en cas de nouveaux détails

Ensuite on calcule le résidu et on le quantifie dans $y_{t, r}$
On ajoute en plus $\hat{x_{t}}^{w}$ quantifié avec le même encodeur que dans la I branch pour mieux synthétiser les détails de haute fréquence
$G_{res}$ permet de reconstruire $\hat{y_{t, r}}$
L'addition de $\hat{x_{t}}^{w}$ et $\hat{y_{t, r}}$ donne la reconstruction $\hat{x_{t}}$
Pour entrainer, on utilise un discriminateur
### Decoupled Scale-Space Warping
We want to preserve details during wrapping reconstructed frames
En combinant ces deux concepts, le "Scale-Space Warping" pour la compression vidéo consiste à déformer l'image à différentes échelles pour qu'elle conserve les informations visuelles importantes tout en réduisant la redondance des données. Cela permet de mieux représenter la vidéo avec moins d'informations, facilitant ainsi la compression sans une perte significative de qualité visuelle.
Use of scale-space warping (SSW)
**problème** Le noyaux d'interpolation doit être de très bonne qualité, pour éviter le flou
**proposition** : découpler en 2 étape
- Plain wraping
- spatial adative blurring
En entrée : flow optique,  masque et la précédente image reconstruite (x)
- On applique un filtre Gaussien L fois sur x
	- On optient un vecteur d'image $[x, x*G(s_{1}), \dots, x*G_{L-1}]$
	- s1, ... sont des hyperparamètres
- Wrap and blur ()
## Experiments
training -> 992k video 256x256 (12 frames each)
evaluation -> MCL-JCV
gain on youtube
two alternative forced choice
on right : original video
on left : compressed video using method A or B
user can change between A and B at any time
choose closest to original
5 questions d'or -> HEVC
métriques très mauvaise
	