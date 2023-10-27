

# Documentation - Infra Linux

## Prérequis

Avant de commencer, assurez-vous d'avoir téléchargez l'ISO de Debian 12 depuis le site officiel de Debian (https://www.debian.org/) et installez-le sur votre serveur.

## Étapes d'installation

### 1. Mise à jour du système
Mettez à jour le système Debian pour vous assurer que vous disposez des dernières mises à jour de sécurité et des paquets logiciels.
```bash
apt update & apt upgrade
```

### 2. Installation du serveur web apache
Installez le serveur web apache en utilisant la commande suivante :
```bash
apt install apache2
```

### 3. Installation de php
Installez le dernière version du langage de programmation phpe utilisant la commande suivante :
```bash
apt install php8.2
```

### 4. Configuration de l'interface réseau
Editer le fichier d'interface réseau :
```bash
nano /etc/network/interfaces
```
Ajoutez la configuration DHCP à votre interface réseau :
```plaintext
auto ens33
iface ens33 inet static
address 10.10.2.254/24
```

### 5. Redémarrage des services
Redémarrez les services réseau pour appliquer les modifications :
```bash
systemctl networking restart
```



