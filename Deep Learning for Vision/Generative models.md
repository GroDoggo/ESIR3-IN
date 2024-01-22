generative model -> a l'envers, on donne une classe et on attent une image
likelihhod (vraisemblance)
- function qui définie les parametre du model
- on veut maximiser cette vraisemblance
## Variational Auto-encoder
Reduction des images en une idée simple
- Passer de dimension NxN a YxY
Le model pour reduire la dimension des images est un encoder
- Prend une image en entrée
- Resort un vecteur Z de dimension très réduite
Le décodeur fait l'inverse
- Prend un vecteur Z petit en entrée
- Resort une image
L'architecture auto-encodeur :
- On pose à la suite l'encodeur et decodeur
- Objectif -> obtenir la meme image d'entrée et de sortie
![[Pasted image 20231127132856.png]]
### Applications
#### Debruitage
La meme image bruite devra redonner l'image originale
#### Compression
Ajouter des contraintes pour forcer l'autoencoder à compresser l'image
### Definitions
Le model prend une entrée une image et ressort une distribution de probabilité
prior -> p(z)
likelihood -> p(x|z)
posterior -> p(z|x)
- On prend un z aléatoire dans p(z)
- on genere un x depuis le likelihood p(x|z)
### Trouver les paprametres
Objectif, maximiser likelihood
probleme : trop cher to calculer tout les p(x) avec tout les z possible donc on approxime avec p(z|x)
![[Pasted image 20231127133532.png]]
il faut rajouter du bruitage
![[Pasted image 20231127134424.png]]
## Generative Adversarial Networks
Un faussaire essaye de contrefaire des tableau
Un expert veut trouver les faux tableau
Les deux sont sans expérience
Au fil des années, soit l'expert très trop bon (peu intéressant)
ou le faussaire devient trop bon (tout ces tableau passe)
### Application
Un générateur G crée de la data
un discriminateur essaye de determiner si la data est vraie ou fausse
les deux apprennent
la loss -> ...
![[Pasted image 20231127135748.png]]
très long a entrainer et parfois ne convergera jamais
**collaspe** : le generateur genere toujours la meme image
le discrimiteur devient trop bon trop rapidement
**pas d'équilibre de nash** -> pas d'équilibre (un est tj trop bon par rapport à l'autre)
**pas de métrique** -> meme si l'image généré est bonne, elle reste mauvaise à l'oeuil humain
### amélioration
ajouter du bruit
entrainement inertiel -> les poids ne peuvent pas trop bouger
minibatch trianing -> retroprapager uniquement toute les X images
donner une generation par classe
## Normalizing Flows
Il est facile de manipuler des Distribution de proba quand elle sont connue
Problème -> les distribution dans la vraie vie sont compliqué
On va combiner plusieurs distribution simple pour reformer la distribution compliqué
![[Pasted image 20231212133143.png]]
![[Pasted image 20231212133235.png]]
$$ x = z_{k} = f_{k} o \dots o f_{1}(z_{0}) $$
Le choix est f est très dépendante du problème
Chaque f doit être inversible
La collection des fonctions doit être assez précise pour représenter la distribution des données
La jacobienne entre deux fonction adjacente doit être calculable
## Diffusion Models
Mouvement de particule dans une région avec grande concentration vers faible concentration
Rappel : Chaine de Markov, séquence d'évèenement lié par des probabilités
![[Pasted image 20231212135422.png]]
Image un réseau de neurone qui apprend comment passer d'une image concentrée (real image) à une image diffusé (gaussian complète)
Le process peut être symbolisé par une chaine de MArkov
Le network peut-il inverser le gaussien?
![[Pasted image 20231212135553.png]]
![[Pasted image 20231212135626.png]]
### CLIP : Connection text to image
On veut que l'encodeur du texte et de l'image envoie au meme endroit
![[Pasted image 20231212140733.png]]
Fusing CLIP and diffusion models to generate images
![[Pasted image 20231212140902.png]]
