# TP 2 Images

## Documentation 

- **Dockerfile reference** https://docs.docker.com/engine/reference/builder/


# Travaux

## Utilisation des tags

> Récupérer l'image nginx avec le tag `stable`
```
docker pull nginx:stable
```

> Voir la liste des images en local
```
docker image list
```

## Créer votre propre image
> Dans le dossier `2_images`, créer un fichier `Dockerfile` avec ce contenu
```
FROM nginx:stable

RUN apt-get update && apt-get install -y caca-utils && rm -rf /var/lib/apt/lists/*

COPY --chown=nginx:nginx html /usr/share/nginx/html
ADD --chown=nginx:nginx https://api.thecatapi.com/v1/images/search?format=src /usr/share/nginx/html/cat.jpg
```

> Dans le dossier `2_images`, construire l'image
```
docker build -t mon_image:v1 .
```

> Afficher la liste des images
```
docker image list
```

> Lancer un container basé sur votre image en publiant le port 80 sur le port hôte 8080
```
docker run --rm -d -p 8080:80 --name mon_site mon_image:v1
```

> Accèder à votre page via le port publié
via l'apercu web de cloudshell (en haut à droite)

> Executer la commande `sh` avec l'option `tty` et `interactive`
```
docker exec -ti mon_site bash
```

> Afficher l'image dans le terminal avec `cacaview`
```
cacaview /usr/share/nginx/html/cat.jpg
```

> Sortir de la visualisation `q` 

> Ctrl + D pour sortir du container

> Arrêter le container
```
docker stop mon_site
```
