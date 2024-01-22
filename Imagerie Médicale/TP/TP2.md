#imed 
#### Exercice 1.4
- Image 1 -> Meme image avec légère transformation
	- SSD=30146448 (élevé)
	- correlation=0.97516 (élevé)
	- info mutuelle=2.1572 (élevé)
Toute les technique marche plutôt correctement sauf la SSD qui est trop forte
- Image 2 -> Meme image assombrie
	- SSD=473379387 (élevé)
	- correlation=0.99621 (élevé)
	- info mutuelle=3.2154 (élevé)
Meme conclusion que l'image 1
- Image 3 -> Image différentes sans recalage
	- SSD=870751839 (élevé)
	- correlation=0.14339 (faible)
	- info mutuelle=0.96481 (faible)
Les images n'étant pas recalé, il est donc normal que la correlation et l'info mutuelle soient faibles. Cependant, la SSD reste compliqué à analyser
- Image 4 -> Image3 avec recalage
	- SSD=362261357
	- correlation=0.56403
	- info mutuelle=1.4775
Comme l'image 3 avec recalage, donc la corrélation a nettement augmenté comme l'info mutuelle. La SSD reste élevé.