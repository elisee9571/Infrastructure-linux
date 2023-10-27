
# Documentation - Infra Linux

## Prérequis

Avant de commencer, assurez-vous d'avoir téléchargez l'ISO de Debian 12 depuis le site officiel de Debian (https://www.debian.org/) et installez-le sur votre serveur.

## Étapes d'installation

### 1. Mise à jour du système
Mettez à jour le système Debian pour vous assurer que vous disposez des dernières mises à jour de sécurité et des paquets logiciels.
```bash
apt update & apt upgrade
```

### 2. Configuration du systeme
Ouvrez le fichier de configuration du système :
```bash
nano /etc/sysctl.conf

#décommenter
net.ipv4.ip_forward=1
```
```bash
sysctl -p /etc/sysctl.conf
```

### 3. Installation et configuration de iptables
```bash
apt install iptables-persistant
```
Editer le fichier d'interface réseau :
```bash
iptables -t nat -A POSTROUTING -o ens33 -j MASQUERADE
```

### 4. Configuration de l'interface réseau
Editer le fichier d'interface réseau :
```bash
nano /etc/network/interfaces
```
Ajoutez la configuration DHCP à votre interface réseau :
```plaintext
auto ens33
iface ens33 inet dhcp

auto ens36
iface ens36 inet dhcp
address 10.10.1.254/24
```
### 5. Redémarrage des services
Redémarrez les services réseau pour appliquer les modifications :
```bash
systemctl networking restart
```
