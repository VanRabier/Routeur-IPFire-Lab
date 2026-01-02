# Routeur-IPFire-Lab

## Présentation du projet
Ce projet consiste à utiliser IPFire comme routeur afin d’assurer le routage et la sécurisation du trafic réseau entre différents segments.  Il a été réalisé dans un environnement virtualisé afin de mieux comprendre le fonctionnement d’un routeur, du NAT et des règles de pare-feu.

## Configuration réalisée
### Préparation de l’environnement (VMware).
- Création d’un réseau personnalisé Host-only
	- Option 'Host-only' cochée
	- Option 'Local DHCP Service' désélectionnée
	
	**RT_IPfire-host-only**
	
- Création d’une machine virtuelle pour IPFire
	
	**RT_IPfire-VM**
	
	- OS: Linux
	- Version: Debian 12.x64-bit
	- Ressources attribuées :
		- 10 Go de disque
		- 512 Mo de mémoire
		- 4 CPU
	- ISO: IPFire
	- Configuration des cartes réseaux:
		- Carte réseau #1: 'Bridged'
			- Génération d’une adresse MAC
	**RT_IPfire-MACbridged**
	- Création d'une deuxieme carte réseau: 
		- Carte réseau #2: 'Custom Host-only'
			- Génération d’une adresse MAC
	**RT_IPfire-MAChost-only**

### Installation d’IPFire
- La machine virtuelle a été démarrée
- IPFire a été installé en suivant l’assistant d’installation
- La langue du système a été sélectionnée
- Le système de fichiers ext4 a été choisi
- Le clavier et le fuseau horaire ont été configurés

### Configuration des interfaces réseau
- Attribution des zones RED et GREEN
	- Dans le **Menu de configuration réseau**
		- Le type de configuration réseau GREEN + RED a été sélectionné
	- De retour dans le **Menu de configuration réseau**
		- Dans Affectation des pilotes et des cartes :
			- L’interface GREEN a été définie avec l’adresse MAC de la carte réseau n°2
			- L’interface RED a été définie avec l’adresse MAC de la carte réseau n°1
	**RT_IPfire-MACred-green**
	
- Configuration du routage IP
	- Toujours dans le **Menu de configuration réseau**
		- L’option Configuration d’adresses a été sélectionnée
	**RT_IPfire_Configurationdadress**
	
			- Pour l’interface RED, le DHCP a été activé
	**RT_IPfire_DHCP_RED**
	
			- Pour l'interface - GREEN, Pour l’interface GREEN, l’adresse IP du routeur et le masque de sous-réseau ont été renseignés
	**RT_IPfire-AdresseIP_GREEN**
	
	- Une fois la configuration terminée, le serveur DHCP a été activé et une plage d’adresses a été définie
	**RT_IPfire_ConfigurationDHCP**

   ### Tests de connectivité
  - Connexion à IPFire en tant que root
	- Vérification des paramètres réseau avec la commande ip a
	**RT_IPfire**
	
	- Vérification de la connexion Internet avec ping 8.8.8.8
	**RT_IPfire**
	
	- Vérification du DNS avec ping perdu.com
	**RT_IPfire_TestDNS**

### Accès et configuration via l’interface Web IPFire
- Creer une VM Windows client
	- Selectionner Host-only pour la carte reseau
	**RT_IPfireClienthostonly**
	
	- Demarre la VM et entrer ipconfig/all dans la ligne de commande
	to check network settings
	**RT_IPfireClientIPCONFIGALL**
	
	- Tests de diagnostic :
		- Ping du routeur afin de vérifier la communication entre les machines
	**RT_IPfireClient-router**
	
		- Ping de 8.8.8.8 afin de vérifier l’accès Internet depuis le réseau GREEN
	**RT_IPfire_ClientPING**
	
		- Exécution de la commande tracert perdu.com afin de valider le routage via IPFire
	**RT_IPfire_Clienttracert**

- Administration d’IPFire
	- Accès à l’interface Web via le navigateur: https://192.168.1.254:444
	- Connexion à l’interface d’administration
	**RT_IPfire_WEBlogin**
	**RT_IPfire_WEBpageprincipale**
