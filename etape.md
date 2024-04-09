# I - Mettre l ' utilisateur dans le groupe **Sudo** et **user42**

- **NB :** pour creer un groupe on utilise la commande `addgroup [option] [-- gid] groupe`
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
- Pour verifier les membres d'un groupe on utilise :
	- `getent group nomDuGroupe`
- **NB :** on a besoin de reboot la machine pour que les effets soient pris en compte

# II - Installation du serveur Openssh et configuration

- Pour verifier si l'application serveur **Openssh-server** est bien installe on utilise la commande :
	- `apt-cache policy openssh-server`
- Pour installer le serveur on utilise la commande :
	- `apt install openssh-server`
- **NB :** il faut verifier le status du serveur en utilisant 
	- `systemctl status sshd`
	- si le serveur n'est pas encore actif on utilise `systemctl start sshd` (on peut aussi l'arreter et le redemarrer)
- Maintenant on peut configurer le serveur ssh
	- on va dans le Dossier "/etc/ssh/sshd_config.d" puis on cree le fichier `config.conf`
	- on le port a l'ecoute '4242' on ecrivant `Port 4242`
	- on interdit au utilissateur de se connecter au serveur en tant que ***Root*** Directement en ecrivant `PermitRootLogin no`
	
- On doit interdire la connexion au autre port avec le pare feu **UFW Firewall**
	- on utilise la commande `apt install ufw`
	- pour verifier le status du pare feu on utilise `systemctl status ufw`
	- on active le pare feu au demarrage avec `ufw enable`
	- on interdit tout les ports avec `ufw default deny`
	- on autorise le port 4242 avec `ufw allow 4242`
	- pour verifier les status des port on utilise `ufw status`
	- puis on Reboot la machine

# III - Configuration du groupe sudo
- On modifie le fichier dans `/etc/sudoers.d`
	- on ajoute :
		- Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
		- Defaults	badpass_message="Dare?"
		- Defaults	passwd_tries=3
		- Defaults	log_input, log_output
		- Defaults	iolog_dir="/var/log/sudo/"
		- Defaults	requiretty

