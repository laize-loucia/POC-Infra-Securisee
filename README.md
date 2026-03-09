
## 1 - Introduction

Ce projet vise à reproduire une petite infrastructure réelle. &nbsp;
J'ai utilisé Docker afin de simuler une architecture réseau simple avec plusieurs services qui tournent dans des conteneurs séparés :

- un service web exposé
- un service interne d'authentification
- une segmentation réseau

## 2 - Architecture

L'infrastructure est composée de deux services :

- un serveur web **NGINX**
- un serveur d'annuaire **OpenLDAP**

Le serveur web est placé dans une **DMZ** et exposé sur le port 8080.

Le serveur LDAP est placé dans un **réseau interne** et n'est pas accessible directement depuis l'extérieur.

<center>

![Architecture](screenshots/network_drawing.png)

</center>


Les conteneurs sont placés sur des réseaux différents :
- une DMZ pour les services exposés
- un réseau interne pour les services sensibles

  
## 3 - Déploiement

L'infrastructure est définie par et dans le fichier : docker-compose.yml

il contient :
- les images Docker utilisées
- les conteneurs à lancer
- les réseaux
- les ports exposés

### Lancement de l'infrastructure


```docker compose up -d```

Cette commande permet de:
- télécharge les images nécessaires
- crée les réseaux Docker
- crée les conteneurs
- démarre les services

Vérifier les conteneurs : ```docker ps```


&nbsp;

## 4 - Test du serveur web

Le serveur web NGINX est accessible via : ```http://localhost:8080```


Cela confirme que le conteneur web fonctionne correctement.


&nbsp;

## 5 - Analyse de sécurité

Un scan réseau a été réalisé avec la commande de scan réseau **Nmap** afin d'analyser les services exposés.


```nmap -sV localhost```


![Scan Nmap](screenshots/nmap_output.png)

On observe que 3 ports sont exposés :

- port 80 : Apache (service local du système)
- port 631 : CUPS (service d'impression Linux)
- port 8080 : NGINX (conteneur Docker)

Le port **8080** correspond au serveur web exposé par le conteneur NGINX.


&nbsp;

## 6 - Segmentation réseau

Les services sont placés sur deux réseaux Docker distincts :

- **dmz_net** : contient le serveur web
- **internal_net** : contient le serveur LDAP

Cette segmentation limite l'exposition des services sensibles.

&nbsp;


## 7 - Améliorations

Plusieurs choses pourraient être ajoutées :

- ajout d'un firewall
- ajout d'un conteneur client pour simuler un attaquant
- analyse réseau plus avancée
- supervision et logs
