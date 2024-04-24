### Definitions
- `SELinux` et `AppArmor` sont deux LSM **(Linux Security Modules)**

- `AppArmor` : AppArmor ("Application Armor") est un logiciel libre de sécurité pour Linux. AppArmor permet à l'administrateur système d'associer à chaque programme un profil de sécurité qui restreint les capacités de celui-ci.

- `SELinux` : SELinux est un système de sécurité pour Linux permettant de limiter les actions possibles en fonction d’une politique de sécurité, il permet d’appliquer notamment différentes méthodes de contrôle d’accès obligatoire. SELinux a un fonctionnement différent de celui d’Apparmor, mais il est également bien plus complet (et complexe !).

- `ssh`(Secure Shell) : Le protocole Secure Shell (SSH) est une méthode permettant d'envoyer en toute sécurité des commandes à un ordinateur sur un réseau non sécurisé. SSH a recours à la cryptographie pour authentifier et chiffrer les connexions entre les appareils. SSH permet également la tunnellisation, ou le transfert de port, c'est-à-dire que les paquets peuvent traverser des réseaux qu'il ne pourrait pas traverser autrement. SSH est souvent utilisé pour contrôler des serveurs à distance, dans le but de gérer l'infrastructure et de transférer des fichiers.
	- Que fait ssh ? : Connexions chiffrées à distance et Possibilité de tunnellisation
	- SSH s'exécute parallèlement à la suite de protocoles TCP/IP ( Transmission Control Protocol/Internet Protocol )
	- À quoi sert SSH ? : Gestion à distance des serveurs, Transfert de fichiers en toute sécurité, Connexion à distance aux services d'un réseau privé, Contournement des restrictions d'un pare-feu.
	- par defaut, ssh utilise le port `22`

- `Sudo`(Substitute user do) : La commande Linux sudo donne aux utilisateurs des droits d’accès temporaires à des zones sensibles du système. Ces droits d’accès sont protégés à l’aide d’un mot de passe. De même, ils ne restent valides que pour une période limitée.

- `UFW Firewall` (Uncomplicated Firewall) : Le pare-feu tout simplement. UFW est un nouvel outil de configuration simplifié en ligne de commande de Netfilter.

- `Virtualisation` (Machine Virtuelle) : La virtualisation est une technologie qui vous permet de créer plusieurs environnements simulés ou ressources dédiées à partir d'un seul système physique. Son logiciel, appelé hyperviseur, est directement relié au matériel et vous permet de fragmenter ce système unique en plusieurs environnements sécurisés distincts.
	- les types de virtualisations :
		- La virtualisation de serveurs
		- La virtualisation des postes de travail
		- La virtualisation des systèmes d’exploitation
		- La virtualisation d’applications
		- La virtualisation du stockage
		- La virtualisation des réseaux

- `LVM` (Logical Volume Manager) : permet la création et la gestion de volumes logiques sous Linux. L'utilisation de volumes logiques remplace en quelque sorte le partitionnement des disques. C'est un système beaucoup plus souple, qui permet par exemple de diminuer la taille d'un système de fichier pour pouvoir en agrandir un autre, sans se préoccuper de leur emplacement sur le disque.

### Quelques commandes Utiles
- Pour verifier les services disponible on utilise `systemctl status`
- Pour ajouter un Utilisateur on utilise `adduser nomUser`
- Pour changer de Hostname on utilise `hostnamectl set-hostname`
- Pour arreter/demarrer/redemarrer (stop/start/restart) un service, il suffit d'utiliser `systemctl laRegleAAppliquer nomDuService`
- `Disable/enable` permet de demarrer ou non un service au demarrage
- `chage` pour les delai de mots de passe
