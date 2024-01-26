Application industrielle
## Use cases
### TV linéaire
Diffusion continue
Pas de décalage temporelle
**contrainte technique de l'encodeur**
- Temps réel
- Fiable
-  Contribution
	- Haute qualité
	- Haut débit
	- Peu de latence
- Distribution
	- Haute qualité
	- Petit débit
### VOD
Envoi de paquet
**contraintes**
- Haute qualité
- Possibilité d'être plus lent
- Plusieurs versions
### Support physique
**contrainte**
- Très haute qualité
- Très haut débit
- Lent
## Transport
### Terrestre
Limite physique sur les fréquences arbitrée par l'Etat
### Cable
Robuste
### Satellite
Résout le problème de distance
### IPTV
Television par internet
Gérer par le distributeur internet
### OTT
Diffusion sur l'internet en général
## Encodeur live
La qualité d'une vidéo provient de beaucoup de facteur
![[Pasted image 20240122160335.png]]
![[Pasted image 20240122160343.png]]
What's the impact of the current decision on the next block?
## Contrôle de débit
Varie en fonction du contenu
![[Pasted image 20240122160831.png]]
![[Pasted image 20240122161117.png]]
DPB : Decoded Picture Buffer
Retient en mémoire les images déjà décodée mais pas encore affichée
![[Pasted image 20240122161458.png]]
A l'inverse, le VBV
![[Pasted image 20240122161754.png]]
On adapte le QP dans le VBV
![[Pasted image 20240122161708.png]]
## Statmux
Choisir le débit en fonction de la qualité
![[Pasted image 20240122162636.png]]
![[Pasted image 20240122163041.png]]
![[Pasted image 20240122163112.png]]
## OTT Streaming
Mise en place d'encodage multi-profil
Un profil par qualité
Une qualité par débit
Selection de profil : HLS (Apple), Smooth Streaming (Microsoft)
Adaptive Bit Rate (ADR) Streaming
**Chunking** : Découpage du stream en section de 2 à 10s
-> Permet de switcher entre plusieurs profils pendant le streaming
### Content adaptive encoding
Deriving an optimal set of profiles for each content
**convex-hull strategy** (Netflix)
![[Pasted image 20240125095634.png]]
Pour l'utilisateur (qui a un certain bitrate) on choisit le point le plus haut (moins de distortion)
## Group of Picture (GOP)
![[Pasted image 20240125100243.png]]
![[Pasted image 20240125100810.png]]
Passage de l'intra dans la video -> effet de battement (intra pumping)
Closed GOP -> Les GOP sont 100% indépendant
Open GOP -> Les B frames peuvent utiliser l'I frame suivante -> lissage de la video (no more bumping)
Mise en place d'un buffer (Lookahead) qui permet de choisir si on utilise un closed ou open GOP
-> detection du changement de scene
## Latence
Temps entre prise d'image et affichage
### Encodeur latency
input buffer
Lookahead
GOP management
Pipelining
Rate control
Real-time smoothing buffer
**Gradual decoder refresh** Each frame have intra blocks
-> progressive refresh
-> contrainte sur les vecteur de mouvement
-> très petite latence
## Preprocessing
Taille de l'image
Deinterlacing
Color conversion
Bitdepth conversion
et d'autres...
### Compensation du mouvement temporel
Nettoie et lisse l'image
On enlève le 'bruit', l'encodage devient plus efficace
### Skin-tone detection
Creation d'un masque pour détecter les visages (les humains)
