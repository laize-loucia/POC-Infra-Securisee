


## Arborescence des fichiers
poc-infra-lab
docker-compose.yml
README.md
architecture.png
screenshots/


***docker-compose.yml*** sert à décrire l’infrastructure :
quels conteneurs lancer, quelles images utiliser, quels réseaux, quels ports, etc.
Ensuite Docker Compose lit ce fichier et lance tout automatiquement.


## Docker compose 


```
sudo apt install docker-compose
```

```
docker compose up
```
Ca permet de 
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




ENtrer dans le conteneur
```
docker exec -it celtak_ubuntu bash
```




