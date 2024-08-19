# Quete_lvm
Challenge de la quête LVM
### Étape 1 : Ajout d'un nouveau disque

1. Éteindre la machine virtuelle Debian.
2. Ajouter un disque de 20 Go via l'interface de gestion de la machine virtuelle.
3. Redémarrer la machine virtuelle et vérifier que le disque est détecté avec la commande `lsblk`.

#### Commande :
```bash
lsblk
```
 

### Étape 2 : Initialiser le nouveau disque en tant que PV

1. Initialiser le nouveau disque `/dev/sdb` en tant que volume physique avec la commande :
   
```bash
pvcreate /dev/sdb
```

2. Vérifier que le PV a bien été créé avec la commande :

```bash
pvdisplay
```

 
### Étape 3 : Ajouter le PV au groupe de volumes `debian-vg`

1. **Ajouter le PV `/dev/sdb` au groupe de volumes `debian-vg` :**

- Exécutez la commande suivante pour ajouter le nouveau PV au VG existant :

```bash
vgextend debian-vg /dev/sdb
```

2. **Vérification de l'extension du VG :**
- Utilisez la commande suivante pour vérifier que le groupe de volumes a bien été étendu :

```bash
vgdisplay
```
 

Le VG debian-vg montre maintenant une taille totale de <39,52 GiB> avec <20,00 GiB> de PE libres.
Ce qui confirme l'extension réussie (donc VG doublé).

### Étape 4 : Créer un snapshot du volume logique `home` et le monter

1. **Créer un snapshot du volume logique `home` :**

- Créez un snapshot de 1 Go du volume logique `home` avec la commande suivante :

```bash
lvcreate --size 1G --snapshot --name home_snap /dev/debian-vg/home
```

2. **Vérification de la création du snapshot :**
 
- Utilisez la commande suivante pour vérifier que le snapshot a bien été créé :
   
```bash
lvs
```

3. **Monter le snapshot sur `/home-snap` :**

- Créez un répertoire pour monter le snapshot :
   
```bash
mkdir /home-snap
```
- Montez le snapshot dans ce répertoire :
   
```bash
mount /dev/debian-vg/home_snap /home-snap
```
- Vérifiez que le contenu du snapshot est identique à `/home` :
   
```bash
ls -l /home-snap
ls -l /home
```
 

