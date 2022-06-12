# TP 1 Docker

## Documentation 

- **Use the Docker command line** https://docs.docker.com/engine/reference/commandline/cli/


# Travaux

## Prise en main des commandes
> Récupérer l'image nginx
```
docker pull nginx
```

> Voir la liste des images en local
```
docker image list
```

> Lancer un container à partir de l'image
```
docker run nginx
```

> Ctrl + C pour interrompre le process

> Relancer le container en mode detaché
```
docker run -d nginx
```

> Afficher la liste des containers en cours d'exécution
```
docker ps
```

## Publication de port
> Trouver la documentation de l'image nginx sur https://hub.docker.com/

*La documentation de l'image nginx precise que par default le service nginx ecoute sur le port 80*

> Tenter d'accèder au service nginx
```
curl localhost:80
```
ou
```
curl localhost
```

*Le service n'est pas accessible depuis le systeme hôte puisque le port 80 n'est pas publié*

> Arrêter le container
```
docker stop <CONTAINER ID>
```
ou 
```
docker stop <CONTAINER NAME>
```
*utiliser `docker ps` pour trouver le Container ID / Name ou l'auto-complétion*

> Relancer un nouveau container en publiant le port 80 sur le port 8080 du systeme hôte
```
docker run -d -p 8080:80 nginx
```

> Tenter d'accèder au service nginx via le port publié
```
curl localhost:8080
```
ou via l'apercu web de cloudshell (en haut à droite)

> Arrêter le container
```
docker stop <CONTAINER ID>
```

## Container nommé
> Création et lancement d'un container nommé explicitement
```
docker run -d -p 8080:80 --name mon_nginx nginx
```

> Arrêter le container
```
docker stop mon_nginx
```

> Afficher la liste complète des containers
```
docker ps -a
```
ou
```
docker container list -a
```

> Supprimer tous les containers (qui ne sont pas en cours d'exécution)
```
docker container prune
```

> Afficher la liste complète des containers
```
docker container list -a
```

*Dans le cas du lancement d'un container nommé explicitement, si il existe déjà un container correspondant au nom, c'est ce container qui est réutilisé...*

*Les containers ne sont pas immutable et peuvent évoluer au cours de leur cycle de vie (fichiers temporaires, logs...)*

*On souhaite donc toujours se baser sur des images immutables que sur des containers pour avoir des comportements idempotents*

> Création et lancement d'un container nommé explicitement avec l'option --rm
```
docker run -p 8080:80 --name mon_nginx --rm nginx
```
> Ctrl + C pour interrompre process

> Afficher la liste complète des containers
```
docker container list -a
```

## En conclusion
* Il vaut mieux nommer ses containers
* On va préférer se baser sur une image pour reconstruire un nouveau container à chaque fois

