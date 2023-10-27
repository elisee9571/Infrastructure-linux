# Documentation - Infra Linux

## Prérequis

Avant de commencer, assurez-vous d'avoir téléchargez l'ISO de Debian 12 depuis le site officiel de Debian (https://www.debian.org/) et installez-le sur votre serveur.

## Étapes d'installation

### 1. Mise à jour du système
Mettez à jour le système Debian pour vous assurer que vous disposez des dernières mises à jour de sécurité et des paquets logiciels.
```bash
apt update & apt upgrade
```

### 2. Installation du serveur DHCP
Installez le serveur DHCP (isc-dhcp-server) en utilisant la commande suivante :
```bash
apt install isc-dhcp-server
```

### 3. Configuration du serveur DHCP
Ouvrez le fichier de configuration du serveur DHCP pour l'éditer :
```bash
nano /etc/dhcp/dhcpd.conf
```
Ajoutez ou modifiez les paramètres de configuration DHCP en fonction de vos besoins. Voici un exemple de configuration de base :
```plaintext
option domain-name-servers 10.10.1.1;
option domain-name "zerolab.lab";

subnet 10.10.1.0 netmask 255.255.255.0 {
  range 10.10.1.10 10.10.1.20;
  option domain-name-servers 10.10.1.1;
  option domain-name "zerolab.lab";
  option routers 10.10.1.254;
  option broadcast-address 10.10.1.254;
}
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
address 10.10.1.1/24
```

### 5. Redémarrage des services
Redémarrez les services réseau pour appliquer les modifications :
```bash
systemctl networking restart
```
Redémarrez le serveur DHCP pour appliquer les modifications :
```bash
systemctl restart isc-dhcp-server
```


