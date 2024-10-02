# TP_1_UNIX

Titre: TP1_Unix 

1ère partie: Post Installation 

Configuration ssh: 
  on installe les paquets grâce à apt install
Nombre de paquets: 
  on exécute la commande "dpkg -l | wc -l", dpkg -l permet de lister les paquets, puis le pipe renvoit à la commande wc (word count) le nombre de paquets soit 326 paquets parce que je suis sur une machine virtuelle préinstallée. 6 paquets de plus ce n'est pas très dérangeant. 

  Après éxécution de la commande df -h, on obtient ceci: 
![image](https://github.com/user-attachments/assets/1818fa9e-8a92-4e07-b92b-ab582430ec75)

Il s'agit de la répartition du stockage, et on peut voir à la ligne "/dev/sda1" qui est la première partition du disque qu'elle est monté sur " / " soit la racine, et il y a 1,6 Go d'espace utilisé dans le cas de la VM pré-installé. 

Liste des commandes et leurs explications: 

echo $LANG: affiche la langue du terminal. 
hostname: affiche le nom du hots, ici "serveur-connection" 
man hostname: ouvre le manuel du hostname et ainsi on trouve la commande permettant d'afficher notre nom de domaine qui est domainname, cette commande une fois executée donne "(none)"

![image](https://github.com/user-attachments/assets/d280081d-857d-4e7d-b6a7-1a3faa51028e)

Ici, on peut voir que la commande "cat /etc/apt/sources.list | grep -v -E ’^#|^$’" affiche le contenu du fichier sources.list non commentée, il s'agit des dépôts actifs que le système utilise pour installer les paquets. Le "grep" et ce qui suit dans la commande permettent de rechercher et de filter par caractères. 

cat /etc/shadow | grep -vE ’:\*:|:!\*:’ : affiche les informations hashés des comptes actifs, ici on n'a que root. Il n'affiche pas les comptes désactivés. 
cat /etc/passwd | grep -vE ’nologin|sync’: affiche toutes les lignes des utilisateurs qui peuvent se connecter normalement en excluant les lignes contenant "nologin" et "sync" 

![image](https://github.com/user-attachments/assets/fb509149-5322-4d67-8af1-4b0abadb0a64)

Ici, la commande affiche les caractéristiques du disque + celles des partitions. Et fdisk-x, même chose mais avec plus de détails. 

A ce stade du TP, je n'avais pas compris la partie configuration SSH, grâce à l'aide de monsieur LeCocq, j'ai compris les commandes apt:

apt update: liste tout les paquets qui peuvent être installés ailleurs
apt search: cherche le paquet sélectionner
apt install: installe le paquet 

ainsi il faut faire ces commandes pour installer un serveur ssh: 
apt update
apt search openssh-server
apt install openssh-server







