# Projet 



lab Docker = un environnement réaliste d’infrastructure, où lusiseurs services différents tournent dans des conteneurs différents.

Le projet permet d'obtenir une mini-infra virtuelle pour essayer de reproduire une petite entreprise.

Les conteneurs sont sur des réseaux différents (DMZ vs Internal).

On peut tester la communication entre eux, la segmentation, le scan Nmap, etc.



# Arborescence
poc-infra-lab
docker-compose.yml
README.md
architecture.png
screenshots/


***docker-compose.yml*** sert à décrire l’infrastructure :
quels conteneurs lancer, quelles images utiliser, quels réseaux, quels ports, etc.
Ensuite Docker Compose lit ce fichier et lance tout automatiquement.

# Architecture



NGINX est isolé et bridge les fait communiquer bridge veut dire Docker crée un réseau virtuel interne.


NGINX est un réseau DMZ, et LDAP est un réseau interne, ces réseaux sont segmentés.

Si les conteneurs dans le même réseau peuvent communiquer. Ici les deux services non car ils sont dans des réseaux différents.



# Docker compose 


## Redaction du YAML

### ajout des services 

NGINX pour le web, OpenLDAP pour l’authentification



## Commandes de base
```
sudo apt install docker-compose
```

```
docker compose up
```

A partir du fuchier yaml ca permet de 
- téléchargé l’image
- créé un réseau
- créé le conteneur
- lancé le conteneur



```
docker ps
```


Afficher les conteneurs
Si les informations du conteneur ne s'affichent pas alors faire:

```
docker ps -a
```
Le conteneur a du se crée puis s'arrêter (une image, celtak/ubuntu-ping-ip n’a pas de processus qui tourne en continu)
Pour l'afficher il faut ensuite faire:


```
docker run -it --name celtak_ubuntu ubuntu:22.04 bash
```

ou modifier le fichier yaml




Vérifier que le conteneur ubunutu de test apparait actif
A chaque ajout de conteneurs :

```
docker compose up -d
```

puis tester nginx
```
http://localhost:8080
```



```
nmap -sV localhost
```



ENtrer dans le conteneur
```
docker exec -it celtak_ubuntu bash
```



1️⃣ repo GitHub
2️⃣ docker compose
3️⃣ lancement services
4️⃣ test web
5️⃣ scan réseau
6️⃣ README + schéma



# Réseau

1️⃣ Interprétation de ton scan

Résultat :

80/tcp   open  http    Apache httpd
631/tcp  open  ipp     CUPS
8080/tcp open  http    nginx

Cela veut dire :

Port 80
80/tcp open Apache

➡️ serveur Apache HTTP Server sur ta machine hôte (ton PC).

Ce n’est pas ton conteneur Docker.

Port 631
631/tcp open ipp CUPS

➡️ service d’impression Linux :

CUPS

Encore une fois → ton système local, pas Docker.

Port 8080
8080/tcp open nginx

➡️ ça c’est ton conteneur Docker avec NGINX.

Parce que dans ton docker-compose.yml tu as :

8080:80

Donc :

machine → 8080
docker nginx → 80
2️⃣ Ce que ton scan montre vraiment

Ton scan montre la surface d’attaque de ta machine :

Internet
   |
Machine locale
   |
----------------------
|  Apache   |  CUPS  |
|  NGINX    |

Donc 3 services exposés.

Ça c’est exactement une analyse de sécurité basique.

3️⃣ Phrase parfaite pour ton README

Tu peux écrire quelque chose comme :

A network scan was performed using Nmap to analyze the exposed services. The scan revealed multiple open ports on the host system including Apache (80), CUPS printing service (631) and the NGINX container exposed on port 8080. This demonstrates how service exposure can increase the attack surface of a system.

Ça fait très cybersécurité / infra.

4️⃣ Ce qu’on pourrait scanner ensuite (encore mieux)

Tu peux scanner le conteneur lui‑même.

Trouve son IP :

docker inspect web_server | grep IPAddress

Puis :

nmap -sV <IP>

Tu verras les ports internes du conteneur.


# NGINX et OpenLDAP 

services qui tournent en continu



