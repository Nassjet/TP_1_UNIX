# TP_1_UNIX

## Post Installation

### 1. Configuration ssh:


- On s'assure d'être connecté en tant qu'admin, ici on a qu'un seul utlisateur (root) et il est admin. 
- On execute `apt update` pour lister tout les paquets qu'on peut installer depuis le web. 
- On execute `apt search openssh-server` pour chercher le paquet qui pourra ouvrir un serveur ssh. 
- On execute `apt install openssh-server` pour installer le paquet. 

Ensuite

- On va décommenter dans le fichier sources.list grâce à la commande `nano /etc/ssh/sshd_config` les paramètres #PermitRootLogin prohibit-password par PermitRootLogin yes
- On lance le serveur avec `systemctl restart ssh` et on vérifie que ça fonctionne avec `systemctl status ssh`


### 2. Connection:

Maintenant, on peut CACHER la fenêtre de la VM et continuer sur un terminal de la machine hôte, c'est-à-dire qu'on va se connecter au serveur ssh avec la commande `ssh root@adresse_de_la_machine_hote`. 

### 3. Nombre de paquets 

On execute la commande `dpkg -l | wc -l` qui d'une part va lister les paquets installés, et qui ensuite va, grâce au pipe  |, envoyer la liste à wc -l (wc = word count) et va compter le nombre de paquets qu'il y a dans la liste, dans notre cas on est sur Vbox LicenceProPreInstalled, et on a donc 330 paquets au lieu de 320 (ce qui n'est pas grave). 

### 4. Répartition du stockage 

On va cette fois éxécuter la commande `df - h`qui va simplement afficher la répartion du stockage dans les différentes partitions: 

root@serveur-correction:~# df -h
|Sys. de fichiers |Taille |Utilisé |Dispo |Uti% |Monté sur
|-----------------|-------|--------|------|-----|--------
|udev             |  4,9G |      0 | 4,9G |  0% |/dev
|tmpfs            |  995M |   564K | 994M |  1% |/run
|/dev/sda1        |  9,1G |   1,6G | 7,1G | 19% |/
|tmpfs            |  4,9G |      0 | 4,9G |  0% |/dev/shm
|tmpfs            |  5,0M |      0 | 5,0M |  0% |/run/lock
|/dev/sda2        |  3,6G |    40K | 3,4G |  1% |/tmp
|/dev/sda3        |  921M |    31M | 827M |  4% |/var/log
|tmpfs            |  995M |      0 | 995M |  0% |/run/user/0

Et on voit que la racine est sur la première partition /dev/sba1, et il y a 1,6 GO d'utilisé, normalement c'est 1 mais bon c'est pas grave. 

### 5. Quelques commandes avec leurs rendus et explications: 

 - `echo $LANG`: affiche la langue du terminal. 
 - `hostname`: affiche le nom du hots, ici "serveur-connection" 
 - `man hostname`: ouvre le manuel du hostname et ainsi on trouve la commande permettant d'afficher notre nom de domaine qui est domainname, cette commande une fois executée donne "(none)"

 - `cat /etc/apt/sources.list | grep -v -E ’^#|^$’` :affiche le contenu du fichier sources.list non commentée, il s'agit des dépôts actifs que le système utilise pour installer les paquets. Le "grep" et ce qui suit dans la commande permettent de rechercher et de filter par caractères. 

 - `cat /etc/shadow | grep -vE ’:\*:|:!\*:’ `: affiche les informations hashés des comptes actifs, ici on n'a que root. Il n'affiche pas les comptes désactivés. 
 - `cat /etc/passwd | grep -vE ’nologin|sync’ `: affiche toutes les lignes des utilisateurs qui peuvent se connecter normalement en excluant les lignes contenant "nologin" et "sync"

 - `fdisk -l`, la commande affiche les caractéristiques du disque + celles des partitions. Et `fdisk-x`, même chose mais avec plus de détails. 


### 6. Pour aller plus loin: 

`preseed`: fichier de préconfiguration linux ou debian ou ubuntu, concrétement on va répondre automatiquement à chaque question de l'installation comme ça, à chaque nouvelle configuration on gagne du temps parce qu'on a pas besoin de répondre manuellement à toutes les questions. 

`Cas oubli du mot de passe `:






