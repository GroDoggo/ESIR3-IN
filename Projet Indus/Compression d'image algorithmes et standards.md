*Auteur : Eric Incerti*
## Format brut
- PNM (Portable aNy Map) -> Classe regroupant des formats
	- PBM -> noir et blanc
	- PGM -> niv gris
	- PPM -> couleur RGB
- BMP -> format de base Windows 
## Format compression sans perte
- TGA -> similaire a BMP, utilise le codage RLE
> [!NOTE]
> Le texte à encoder est parcouru pour trouver des suites de caractères identiques, noter alors le caractère et le nombre de répétition dans la séquence.
> **Exemple** : DDDDDCCCCOOODDE peut être décrit par 5 fois le caractère D suivi de 4 fois le caractère C, etc. Le message peut donc être compressé D5C4C3D2E1 (10 caractères au lieu de 15, taux de compression : 33%).
> https://www.dcode.fr/compression-rle

- GIF -> LZW (dico)
- PNG -> LZ77 (deflation/inflation)
- TIFF -> LZW + predictif
- JPEG (version sans perte) -> DPCM
- JBIG (norme) -> QM-Coder
## Format compression avec perte
JPEG -> DCT
## Image en couleur
### Synthèse additive
RGB classique
Image finale = Rouge + Vert + Bleu
### Synthèse soustractive
CMY (Cyan Magenta Yellow)
Image finale = Blanc - Cyan - Magenta - Yellow
### Teinte/Saturation
HSV
Teinte + Saturation  + Valeur (Voir roue des couleurs)
### Luminance
YUV (YIQ + YCrCb)
Formule connue de RGB->YUV (et pareil pour les autres)
## Codage avec extension de source
> [!NOTE]
> Rappel : HUFFMAN

**Extension de source** : Augmenter la taille de l'alaphabet en groupant les lettres. Par exemple S = {"AAA", "AAT", "AAC", ect}
Cela peut améliorer à la fois le CLF (Codage a longueur fixe) et le codage de Huffman encore plus.
A essayer lorsque S semble chaotique
> [! WARNING]
> Par default, Huffman nécessite que le décodeur connaissent le dictionnaire (1 -> a, 01 -> b, etc.). ce qui le rend inutilisable en pratique dans de nombreux cas.
> Il existe cependant une variante dynamique de Huffman qui construit le code à la volée mais très peu utilisé.

## Codage arithmétique entier
Alternative du codage arithmétique (celui qui est infame) pour la pratique7
