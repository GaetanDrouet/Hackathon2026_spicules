# Classification d'images de silicite en fonction de la présence de spicule
## Objectif du projet
Ce projet vise à permettre de repérer l'absence ou la présence de spicules dans une image de silicte. 
Pour cela, il se base sur 27 photographies de silicite avec des spicules et de 83 sans. Celles-ci peuvent être récupérées sur ce lien : https://www.grosfichiers.com/rRdH4srcNvi

## Méthodes employées
Deux techniques ont été testées sur ce jeu de données.
### YOLO cls
Une première technique utilise un modèle de [YOLO cls](https://docs.ultralytics.com/tasks/classify/) pour classifier automatiquement les images en deux classes : sans spicule et avec spicule. Pour cela, une première phase de répartition de données en Train, Test et Val est effectuée ainsi qu'une normalisation des données avec d'avoir autant d'image de chaque classe. Les images ultérieures peuvent ensuite être classées autmatiquement au moyen de ce modèle.
### Transport optimal
Après un prétraiatement, 3 images variées des deux types sont extraites afin de servir d'exemples. Les images à tester sont ensuite comparées à ces images et un calcul de distance minimale du coût de transport établit dans quelle classes celles-ci sont à placer. Nous conjecturons que l'implémentation n'est pas bonne (bien trop naïve) mais l'idée sous-jacente vaut sans doute le coup d'être étudiée.

## Résultats
### YOLO cls
En faisant la moyenne de 25 modèles développés sur des jeux de données différents extraits du jeu de données initial, 56,6% des images sans spicules sans classées correctement et 71,2% des images avec. Cela fait une moyenne de 64,4% de précision.
### Transport optimal
62,65% des images sans spicules sont classées correctement et 37,04% des images avec spicules. Cela fait une moyenne de 56,36% de précision.

## Anlyse des résultats
En analysant les images qui sont classés incorrectement, on repère certains points communs. Les images avec spicules qui sont classés sans sont souvent des images où les spicules ressortent peu du reste de l'image au niveau du contraste et des couleurs. À l'inverse, les images sans spicules qui sont classées incorrectement sont souvent des images avec des variations de couleur importantes en leur sein ou des marques (telles que des fissures) qui pourraient, même pour un humain non-entraîné, être confondues avec des spicules. 
Un augmentation du nombre de données pourrait sans doute avec un effet important sur les résultats du modèle YOLO cls. Les modèles CNN (Convolutional Neural Networks) ont généralement besoin d'une certaine quantité de données pour en comprendre des modèles fiables et généralisables. Ainsi, après avoir vu suffisamment d'images avec fissures n'étant pas classés en tant qu'image avec spicule, il pourra cesser de faire l'amalgame. 
