Francois Chaumette
Equipe Rainbow
## Introduction
Tache -> positionner robot par rapport a un objet a l'aide d'une camera
c* -> la ou je voudrais que la camera se positionne
c -> la ou est actuellement la camera
Pose désirée -> $^{c*}T_o$
Déplacement -> ![[Pasted image 20231129095440.png]]
e -> effecteur (grapin du robot)
e* -> la ou je veux que l'effecteur se situe
![[Pasted image 20231129095637.png]]
$^{e*}T_{c*}=^{e}T_c$
![[Pasted image 20231129095749.png]]
![[Pasted image 20231129095812.png]]
### Calibration
![[Pasted image 20231129100037.png]]
A et B des matrice homogene
On arrive au systme
![[Pasted image 20231129100529.png]]
Changement de représentation
![[Pasted image 20231129101027.png]]
![[Pasted image 20231129101151.png]]
Ne marche que lorsque tout est parfaitement calibré
### Visual servoing
Vision bases loop control of a dynamic system
- extract visual measurements near video rate (matching then tracking)
- design adequate visual features from the available measurements:
- design a control scheme to regulate the error to 0
- taking into account the system and environment constraints for an adequate system behavior (stability, robustness, …)
## Loi de contrôle
![[Pasted image 20231130095107.png]]
![[Pasted image 20231130095359.png]]
possibilité d'améliorer (uniquement dans le cas ou s est proche de s*) Ls est calculé avec s*
![[Pasted image 20231130100144.png]]
exemple : Ls classique -> le point vont vers leur objectif en ligne droite
![[Pasted image 20231130101309.png]] necessite de faire reculer l'image a l'infini
Ls avec s*
![[Pasted image 20231130101427.png]] on autorise une augmentation d'erreur
## Modeling issues
