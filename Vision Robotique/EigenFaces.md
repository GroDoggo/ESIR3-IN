On calcule le visage moyen
On va faire nos traitement sur l'image I moins l'image moyennes
On calcule la Covariance
$$ C = 1/M \sum \nabla_{i} \nabla_{i}^T $$
Problème de mémoire, matrice de covariance trop grande
$$A^TAv_{i} = \mu v_{i}$$
$$ A A^tAv_{i} = \mu Av_{i}$$
where $Av_i$ are the eigenvector of $AA^T$ (C)

classification : vecteur W avec $W_{k} = u_{k}(x-\nabla)$
Autre solution :simple SVD (Matrice U)

