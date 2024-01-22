Aline ROUMY
http://people.rennes.inria.fr/Aline.Roumy/COV.html
**Evaluation** : 3CC de cours + lire un article
Encodeur a partir d'un reseau de neurone
Voir *modalité d'évaluation* pour conseil

## Lossless
On peut compresser sans perte des sources discrètes iid (indépendants et identiquement distribuées)
**sources** -> Séries de variables aléatoires
**discrete** -> Valeur finie (sur N)
On utilise alors un code Entropique
 - Huffman
 - Arithmétique
Un code à longueur variable (longueur petite si grande fréquence)
**Performance optimale** -> (Shannon) sont l'entropie de la source H(S) \[bit/s]
$$ H(S) = \sum_{{s}}p(s) * \log_{{2}}\left( \frac{1}{p(s)} \right) = E\left[ \log_{2}\frac{1}{p(S)} \right]$$
$$ E[g(s)] = \sum g(x) * p(s)$$
On a deux résultat optimaux :
- asymptotiquement (lorsque le nb de sympbole tend vers l'infinie)
$$ P_{e} = probabilite_{erreur} \to 0$$
- La longueur moyenne d'un code entropique optimal est $H(S) \leq l < H(S)+1$
	- Les bornes dépendent de la distribution de S
On peut prendre n symboles à la fois -> borne supérieur $=H(S) + 1/N$
$$ l = \frac{1}{N} * \sum p(s) * l(s)$$
## Lossy
Source -> Encoder -> Decoder -> Sink
Entre S et S' il y a une distorsion D
$$d_{N}(s, s') \geq 0 (= \iff s = s')$$
On peut utiliser MSE
$$d_{N}(s, s') = \mid s - s' \mid_{2} = \frac{1}{N} * \sum (s_{k} - s_{k}')^{2}$$
On peut associer chaque code Q à un point (R, D)
On arrive à un nuage de nuage et on peut former une fonction de Rate (débit) minimum en fonction de la distorsion R(D)
-> Impossible à compute (impossible de faire tout les codes)
$$R(D) = inf_{Q:\sigma(Q)\leq D} r(Q)$$
$$R(D) = min_{p(S'|S):E[d(S', S)]\leq D} I(S;S')$$
Trouver une borne inférieure pour R(D) ou un algo informatique (Blahut-Arimoto)
Si D=0, $R(0) = R_{max} = H(S)$ (débit infini)
$D_{max} = E[d(S, \mu)] = V$
On peut borner inf la fonction D(R) et R(D) (avec la distance calculer par MSE)
*voir formule Shannon slide 24*
Cette borne inférieur dépend de la source (Gaussienne est la plus haute -> plus grande distortion)
## Quantification
s -> quantizer Q -> s'
fonction non-inversible
On peut compresser avec perte
méthode quasi-optimale -> Q scalaire uniforme + code entropique
Courbe R(D) -> region atteignable est au dessus
Quelque soit la distribution iid, la méthode quasi-optimale est a 1.53dB ou 1/4 bit/s de la courbe optimale théorique R(D)
