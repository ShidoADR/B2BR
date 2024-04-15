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
		- Defaults	logfile="/var/log/sudo/sudo.log"
		- Defaults	requiretty

# IV - Configuration du mots de passe fort
- pour la permiere etape on change quelques parametre du fichier **login.defs** dans `/etc/`
	- PASS_MAX_DAYS	30
	- PASS_min_DAYS	2
	- PASS_WARN_AGE 7
	
	- **NB :** ces parametres ne sont pas pris en compte par les utilisateur deja present c'est a dire 
***hariandr*** et ***root***
	pour changer ces parametres il suffit d'utiliser la commande `chage [option] Login`
	*exemple :* chage -M 30 hariandr
		- -M 30 : change le PASS_MAX_DAYS en 30
- pour les politiques de mots de passe on utilise le module appartenant a **PAM** qui est **pam_pwquality**
	- pour installer le module il suffit d'utiliser la commande `apt install libpam-pwquality`
	- emsuite il suffit d'ajouter les parametres suivant dans le fichier **common-password** se trouvant dans `/etc/pam.d/` (on mets les parametres apres `pam_pwquality.so`)
		- retry=3
		- minlen=10
		- ucredit=-1
		- lcredit=-1
		- dcredit=-1
		- maxrepeat=3
		- usercheck=3
		- enforce_for_root
		- difok=7
	- on **Reboot** la machine
# V - creation du script 'Monitoring.sh'

# VI - Bonus
- intallation de ***WORDPRESS***
	- installation de *lmp* stack (lighttpd, mariaDB, php)
		- intallation de lighttpd
			```
				apt install lighttpd
			```
		- autorisation du port http
			```
				ufw allow http
			```
		- installation de wordpress
