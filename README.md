


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



Afficher les conteneurs
```
docker ps
```

ENtrer dans le conteneur
```
docker compose up
```
