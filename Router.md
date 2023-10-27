
# Documentation - Infra Linux

## Prérequis

Avant de commencer, assurez-vous d'avoir téléchargez l'ISO de Debian 12 depuis le site officiel de Debian (https://www.debian.org/) et installez-le sur votre serveur.

Sélectionnez votre machine virtuelle routeur et modifiez sa configuration réseau pour utiliser la même interface réseau virtuelle et lui ajouté un réseau NAT. 
Cela devrait être une interface de réseau interne et externe. L'interface réseau virtuelle doit être la même pour toutes les machines.
Assurez-vous que les machines virtuelles sont toutes connectées à la même interface réseau virtuelle.

![configuration du réseau LAN](https://github.com/elisee9571/Infrastructure-linux/blob/main/config-router-lan.png)

Démarrez les machines virtuelles après avoir apporté ces modifications.

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
Ajoutez la configuration du router à votre interface réseau :
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
