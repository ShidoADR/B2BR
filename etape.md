# I - Mettre l ' utilisateur dans le groupe **Sudo** et **user42**

- NB : pour creer un groupe on utilise la commande `addgroup [option] [-- gid] groupe`
	- on ecris donc `addgroup hariandr42`
	- le groupe **sudo** se cree automatiquement lorsqu'on installe **Sudo**
 `apt install sudo`
	- **NB :** on doit se connecter en tant que ***Root*** pour pouvoir executer la commande
`su -`, il est important de bien ecrire le ' - ' sinon vous n'aurez pas acces au variable d'
environnement de ***Root***
- pour ajouter un utilisateur au groupe on utilise la commande `Usermod -aG groupe utilisateur`
	- -a : ajoute l'utilisateur au groupe
	- -G : specifie le groupe
	- **NB :** les deux flags doivent etre executer ensemble
- on ecris donc :
	- `usermod -aG sudo hariandr`
	- `usermod -aG hariandr42 hariandr`
