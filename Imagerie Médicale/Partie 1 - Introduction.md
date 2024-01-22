## Contexte
- Explosion de l'importance des images médicales en médecine
- Grand volume de données -> besoin outils d'aquisition et traitement
	- Acquisition
	- Amélioration
	- Analyse
	- Visualisation
### Spécificité de l'image médicale
- **Image volumique** : informations en 3D
	- Il faut adapter les méthodes à ce type de données
- **Recalage** : comparer plusieurs images d'un même *objet*
	- Même cerveau issu de différents scanner
	- Cerveaux de plusieurs patients
	- Même cerveau à différents moment
- **Fusion** : rassembler en une image les informations
## Exemples
### Radiographie
- 1901 -> découverte des rayons X
- Visualisation des os, dents et non des muscles
- Impression sur un film argentique
- Examen rapide et précis
- Radiation -> multiplication d'examen néfaste
- Application pour les structure osseuses et articulaires
Pas possible de faire des images de coupe
- On peut voir le dessus
- On peut voir le dessous
- Impossible de voir au milieu
### Scanner
- Utilisation des rayons X, plusieurs photos prise autour du patient
- Reconstruction en seconde partie pour obtenir des images de coupe
### Imagerie nucléaire
- On utilise un émetteur de positon
- Le positon rencontre un electron et émet deux photons (1 de chaque coté)
- On détecte les photons pour determiner le lieu de la réaction (droite)
- Reconstruction dans un second temps
- Mauvaise résolution spatiale
- Rayon ionisant
- Application cardiologie et organique
### Ultrasonographie (échographie)
- Utilisation des ultrasons
- Rebondissement des ultrasons
- Très portatif, bonne résolution, temps réel
- Application partout
### IRM - Imagerie à résonance magnétique
- Utilisation du magnétisme nucléaire
- **Spin** : Un petit aimant qui tourne sur lui-même
- Dans l'IRM (un gros aiment) : tout les atomes d'hydrogene s'alignent (dont 10 environ sur un axe précis)
- On excite ces 10 atomes avec un rayon RF à une fréquence précise
- Le noyau rentre alors env résonance
- **Relaxation** : Retour à l'équilibre de l'aimantation
- L'atome se relaxe et on peut le mesurer
- Selon le tissus, la relaxation n'est pas la même
- En fonction de la positon du corps, la puissance du magnétisme change afin de déterminer la coupe de la relaxation recue
### MEG EEG
- Mesure directe de l'activité électrique cérébrale en utilisant des électrodes
- Localisation en surface des zone d'activités
- En utilisant des lois de physique de propagation des signaux électriques on peut en reconstruire une image
