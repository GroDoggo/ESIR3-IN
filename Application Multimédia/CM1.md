## TAL
Accomplir des tâches en lien avec le langage
- Correction
- Recherche d'information
- Classification de texte
- Traduction
- et plein d'autre...
### Lemmatisation
Obtention de la forme canonique
- verbe -> a l'infinitif
- sinon -> forme au masculin singulier
### Bag of word
Construction d'un vecteur avec le vocabulaire des documents
Systems de pondération avec ce vecteur pour chaque document
mot indépendant les uns des autres -> pas de négation
### Représentation denses
**représentation statique** ->un token = un vecteur
**représentation contextuelle** -> calcul du vecteur en contexte
(ELMo, ULMFit, ...)
## Embeddings
### Word embedding
represents word in a Euclidian space with properties
words are represented by the context (un mot est reconnu par son voisinage)
- count co-occurence of words dans un contexte -> grosse matrice
- réduire dimensions (eviter sparsity)
- utiliser les vecteurs comme représentation
#### Approche directe
1. D'apres une phrase en input, creer la matrixe de co-occurence
2. Decomposer X avec les eigen-value decomp ou singular value decomp (SVD)
	- X = UVUt ou X = USVt
3. Utiliser les vecteurs propres Ui comme representation du mot i
#### Word2Vec
- Directly seek vector representation  of tokens that maximizes the joint probability of co-occuring words
- Deux tâches 
	- Prédire le mit central des mot de contexte (CBOW)
	- Prédire les mots de contexte a partir du mot central (Skip gram)
- Simple neural network
### Document embedding
Simple solution -> bag of word
#### CNN (convolution)
Similaire aux images mais en 1D
