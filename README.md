# 🖥️ S03 : Atelier Proxmox, OPNsense & WireGuard

Atelier pratique de la S03 du cursus Administrateur d'Infrastructures Sécurisées (O'clock).

---

## 🍔 Au menu
- Configuration des bridges réseau sur **Proxmox VE**
- Mise en place d'un double **NAT via iptables** sur le nœud Proxmox
- Déploiement et configuration complète du routeur/pare-feu **OPNsense** (WAN, LAN1, LAN2)
- Configuration du service DHCP (**Kea DHCPv4**)
- Mise en place d'un accès distant sécurisé par VPN **WireGuard** (avec configuration en *split-tunnel*)
- Persistance et sauvegarde des règles de routage et de pare-feu au redémarrage

---

## 🛠️ Étapes clés de réalisation

### 1. Proxmox : Réseau & NAT
- Création des interfaces virtuelles (*Linux Bridges*) : `vmbr1` (WAN), `vmbr2` (LAN1), et `vmbr3` (LAN2).
- Activation de l'IP Forwarding (`net.ipv4.ip_forward=1`).
- Application de la règle de masquage réseau (`iptables -t nat -A POSTROUTING`).
- Sauvegarde et restauration automatique des règles au démarrage (`/etc/network/interfaces` et `/etc/iptables-rules.save`).

### 2. OPNsense : Pare-feu & Routage
- Création de la VM OPNsense et affectation des interfaces (gestion des correspondances d'adresses MAC).
- Configuration de l'interface WAN et de la passerelle vers Proxmox.
- Segmentation des réseaux internes (LAN1 en `10.0.0.0/16` et LAN2 en `172.16.0.0/16`).
- Désactivation des services concurrents et activation du serveur DHCP Kea.

### 3. VPN WireGuard & Accès distant
- Configuration de l'instance serveur `wg0` et génération des *Peers* via l'outil intégré.
- Ouverture des ports et redirection de flux (*DNAT*) sur Proxmox vers l'OPNsense.
- Configuration du client WireGuard sur la machine hôte en mode *split-tunneling* (`AllowedIPs = 10.0.0.0/16`).

---

## 👨‍💻 Auteur
- **Guillaume GEREMY** — *O'clock (2026)*
