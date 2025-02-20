Nous avons rajouté 5 nouveaux JVM flags : <br>

1. (-Xmx1024m) qui dicte la taille maximale du monceau comme étant de 2048 MB; <br>
Raison : Permet de commencer avec une mémoire préallouée et ainsi réduit les "resizings" pendant que le logiciel démarre <br>

2. (-Xms512m) qui dicte la taille initiale du monceau comme étant de 1024 MB ; <br>
Raison : Permet de limiter la quantité de mémoire du monceau et évite ainsi des erreurs potentielles comme "OutOfMemoryError" <br>

3. (-XX:+UseZGC) qui utilise le "Garbage Collector" Z ; <br>
Raison : Permet d'utiliser le garbage collector Z qui est bon pour les logiciels utilisant des monceaux de grande taille et qui requièrent des temps de pause minimaux <br>

4. (-XX:MaxNewSize=256m) qui limite la taille des nouveaux objets dans le monceau ; <br>
Raison : Réduit la fréquence de garbage collection et par conséquent, la performance du logiciel <br>

5. (-XX:MaxTenuringThreshold=0) qui spécifie le nombre de fois un objet peut passer à travers la nouvelle génération avant d'être envoyé dans la vieille ; <br>
Raison : Permet d'éviter plusieurs petits cycles de GC et donc d'éviter que des nouveaux objets deviennent des vieux objets s'ils passent au travers du GC <br>

Les flags sont séparés sur deux nodes YAML afin de faire deux builds différents; cela évite des conflits, par example un conflit entre les deux flags Xmx. <br>
Le premier build tente d'être optimisé, alors que le deuxième teste ce qui se passe si on limite la mémoire à outrance et dump les logs pour voir ce qui se passe. <br>
Nous avons aussi ajouté des étapes à la fin de la github action qui permettent de voir tous les logs afin d'aider le débogage et de l'optimisation additionelle.
