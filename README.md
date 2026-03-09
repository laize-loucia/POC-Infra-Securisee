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



# NGINX et OpenLDAP 

services qui tournent en continu



