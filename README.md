# Routeur-IPFire-Lab

## Présentation du projet
Ce projet consiste à utiliser IPFire comme routeur afin d’assurer le routage et la sécurisation du trafic réseau entre différents segments.  Il a été réalisé dans un environnement virtualisé afin de mieux comprendre le fonctionnement d’un routeur, du NAT et des règles de pare-feu.

## Compétences développées
- Réseaux: routage IP (bases)
- Sécurité réseau (notions de base)
- Pare-feu et filtrage réseau
- Administration système
- Diagnostic et dépannage réseau
- Documentation technique

## Configuration réalisée
### Préparation de l’environnement (VMware).
- Création d’un réseau personnalisé Host-only
	- Option 'Host-only' cochée
	- Option 'Local DHCP Service' désélectionnée
###### *Ref 1: Virtual Network Editor*
<img width="455" height="395" alt="RT_IPfire_host-only" src="https://github.com/user-attachments/assets/b0fb9d97-21a2-4ff8-9ddc-42cb44ee7e2a" />

- Création d’une machine virtuelle pour IPFire
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
     	- Création d'une deuxieme carte réseau: 
			- Carte réseau #2: 'Custom Host-only'
				- Génération d’une adresse MAC

###### *Ref 2: Virtual Machine Settings*
<img width="327" height="325" alt="RT_IPfire_VM" src="https://github.com/user-attachments/assets/7bb0ac2b-0daf-4997-a023-03f4110bc70b" />

###### *Ref 3: Network Adapter Advanced Settings: Carte réseau #1*
<img width="560" height="504" alt="RT_IPfire_MACbridged" src="https://github.com/user-attachments/assets/c06c94f2-e475-45c6-b4ba-3fea46b2a27b" />

###### *Ref 4: Network Adapter Advanced Settings: Carte réseau #2*
<img width="561" height="505" alt="RT_IPfire_MAChost-only" src="https://github.com/user-attachments/assets/64fe9f7d-7093-4e6f-ac51-215314667d88" />

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
			- L’interface GREEN a été définie avec l’adresse MAC de la carte réseau #2
			- L’interface RED a été définie avec l’adresse MAC de la carte réseau #1
###### *Ref 1: Adapteur Reseau pour l'interface - GREEN*
<img width="326" height="251" alt="RT_IPfire_MACgreen" src="https://github.com/user-attachments/assets/ff3029ca-448a-4b3d-bdaf-81e8e865433a" />

###### *Ref 1: Adapteur Reseau pour l'interface - RED*
<img width="328" height="248" alt="RT_IPfire_MACred" src="https://github.com/user-attachments/assets/bfad7491-c4b3-46e3-a18c-e48eebee74b1" />

- Configuration du routage IP
	- Toujours dans le **Menu de configuration réseau**
		- L’option Configuration d’adresses a été sélectionnée
			- Pour l’interface RED, le DHCP a été activé
			- Pour l'interface - GREEN, Pour l’interface GREEN, l’adresse IP du routeur et le masque de sous-réseau ont été renseignés
	- Une fois la configuration terminée, le serveur DHCP a été activé et une plage d’adresses a été définie
###### *Ref 1: Virtual Network Editor*
<img width="329" height="249" alt="RT_IPfire_Configurationdadresse" src="https://github.com/user-attachments/assets/50c35d0b-8278-4b7f-962a-887f767c005a" />

###### *Ref 1: Virtual Network Editor*
<img width="326" height="248" alt="RT_IPfire_DHCP_RED" src="https://github.com/user-attachments/assets/fe43cb09-30ec-4f46-a488-80ad857cfad2" />

###### *Ref 1: Virtual Network E*
<img width="327" height="247" alt="RT_IPfire_AdresseIP_GREEN" src="https://github.com/user-attachments/assets/0aeed4a3-5875-458e-979d-5f5df62d12a1" />

###### *Ref 1: Virtual Network Editor*
<img width="323" height="248" alt="RT_IPfire_ConfigurationDHCP" src="https://github.com/user-attachments/assets/16e1dedb-3e1d-4c0a-8400-290a03d89d03" />

   ### Tests de connectivité
  - Connexion à IPFire en tant que root
	- Vérification des paramètres réseau avec la commande ip a
*Ref 1: Virtual Network Editor*
**RT_IPfire**
	
	- Vérification de la connexion Internet avec ping 8.8.8.8
*Ref 1: Virtual Network Editor*
**RT_IPfire**
	
	- Vérification du DNS avec ping perdu.com
*Ref 1: Virtual Network Editor*
**RT_IPfire_TestDNS**

### Accès et configuration via l’interface Web IPFire
- Creer une VM Windows client
	- Selectionner Host-only pour la carte reseau
*Ref 1: Virtual Network Editor*
**RT_IPfireClienthostonly**
	
	- Demarre la VM et entrer ipconfig/all dans la ligne de commande
	to check network settings
**RT_IPfireClientIPCONFIGALL**
*Ref 1: Virtual Network Editor*
	
	- Tests de diagnostic :
		- Ping du routeur afin de vérifier la communication entre les machines
**RT_IPfireClient-router**
*Ref 1: Virtual Network Editor*
	
		- Ping de 8.8.8.8 afin de vérifier l’accès Internet depuis le réseau GREEN
**RT_IPfire_ClientPING**
*Ref 1: Virtual Network Editor*
	
		- Exécution de la commande tracert perdu.com afin de valider le routage via IPFire
**RT_IPfire_Clienttracert**
*Ref 1: Virtual Network Editor*

- Administration d’IPFire
	- Accès à l’interface Web via le navigateur: https://192.168.1.254:444
	- Connexion à l’interface d’administration
*Ref 1: Virtual Network Editor*
**RT_IPfire_WEBlogin**
*Ref 1: Virtual Network Editor*
**RT_IPfire_WEBpageprincipale**
