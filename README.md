## 💪 Challenge

Le challenge consiste, en partant d'une machine Debian telle que celle installée au début de la quête, à suivre une succession d'étapes visant à effectuer des opérations classiques sur LVM.  
À chaque étape, des commandes doivent être saisies pour afficher l'état du système avant les opérations et après les opérations afin de constater les modifications effectuées.  
L'ensemble des commandes et leurs affichages sont à recopier dans la solution de cette quête.

- Ajoute un nouveau disque à la machine et ajoute-le au groupe de volume `debian-vg` pour au moins doubler l'espace du groupe de volume.
- Créer un snapshot du LV `home`.
- Monte le snapshot créé sur `/home-snap`.
- Constate que `/home-snap` est bien une copie de `/home`.
- On peut alors travailler sur `/home-snap` et y faire des modifications. En supposant qu'on n'a plus besoin de la copie, démonte `/home-snap`.
- Détruit le snapshot.

## 🧐 Critères d'acceptation

Les commandes et leurs affichages permettent bien de constater :

- L'ajout d'un PV à `debian-vg` et au moins le doublement des `Total PE`.
- La création d'un snapshot du LV `home`.
- Il y a bien création d'un dossier `home-snap` et montage du snapshot dans ce dossier.
- L'affichage du contenu de `home-snap` affiche un contenu identique à `/home`.
- L'affichage des systèmes de fichiers actuellement montés n'affiche plus `/home-snap`.
- L'affichage des LV n'affiche plus le snapshot et le LV `home` n'est plus la source d'aucun snapshot.
