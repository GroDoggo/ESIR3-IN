All planning problems can be represented by a graph
-> Solving problem is finding a sequence of node from A to B in graph
Généralement on recherche le plus court chemin -> chemin de moindre coût
*exemple : un graphe d'aeroport peut avoir comme cout le distance ou le temps*
**Seulement possible si tout les edges sont de valeurs non-négative** -> sinon un cycle peut être de cout négatif
![[Pasted image 20231211081650.png]]
## Dijkstra's algorithm
- **Q** la liste de priorité de pair <cout, node>
-> la queue est trié selon un cout croissant
- **cost(a, b)** retourne le cout du edge reliant a vers b
- **cost(a)** table qui donne le cout optimal entre la source et a (valeur par default -> infinie)
- **pre(a)** table qui donne le prédécesseur de a le long du chemin optimal (valeur par default -> infinie)

![[Pasted image 20231211082310.png]]
Le chemin optimal est indépendant entre le passé et le futur (concaténation de chemin optimaux)
On peut stop des que le sommet de la file de priorité est de de cout supérieur a cost(cible)
## A* algorithm
Calcule le plus court chemin entre une source et une destination bien précise
Utilise une heuristique pour estimer le cout de la source vers l'objectif
La petite étoile signifie que l'algo utilise une heuristique
![[Pasted image 20231211084415.png]]
## IDA* algorithm
Variante de A*
Boucle avec plusieurs limite de profondeur
![[Pasted image 20231211091614.png]]![[Pasted image 20231211091631.png]]
Plus lent que A*
Possibilité d'amléioration :
- Eviter de reboucler sur un nœud déjà exploré
- Utiliser un cache pour sauvegarder le meilleur chemin dans certaines configuration
## Heuristique
### Grille
![[Pasted image 20240123100654.png]]
![[Pasted image 20240123100707.png]]
### Espace continu
![[Pasted image 20240123100723.png]]
## Comparaison des algorithmes
![[Pasted image 20240123100834.png]]
