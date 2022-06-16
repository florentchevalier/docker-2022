# TP 4 Networks

# Travaux

## Réseau par defaut `bridge`
> Dans le dossier `4_networks`

> Relancer le container basé sur l'image postgres
```
docker run --rm --name ma_bdd -e POSTGRES_PASSWORD=dinumDocker2022 -d postgres:14-bullseye
```

*Par défaut les containers se lancent sur le network `bridge`*

> Lancer un container basé sur l'image `dpage/pgadmin4`
```
docker run --rm -p 8080:80 --name pgadmin -e PGADMIN_DEFAULT_EMAIL=dinum.sin.agents@gouv.nc -e PGADMIN_DEFAULT_PASSWORD=F0rmation -d dpage/pgadmin4
```

> Accèder à votre pgadmin via le port publié `8080`
via l'apercu web de cloudshell (en haut à droite)

*L'interface pgadmin met quelques secondes à se lancer, recharger la page en cas d'erreur*

> S'authentifier avec `dinum.sin.agents@gouv.nc` `F0rmation`

> Trouver l'ip du container `ma_bdd`
```
docker container inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ma_bdd
```

> Dans l'interface pgadmin, ajouter un serveur
* Dans l'onglet `General`
  * Name : `ma-bdd`
* Dans l'onglet `connection`
  * Host name/address : **IP du container ma_bdd**
  * Username : `postgres`
  * Password : `dinumDocker2022`
* `Save`

> Tester la connection

*Les container sur le network `bridge` accèdent aux uns et aux autres*

> Arrêter les containers
```
docker stop ma_bdd pgadmin
```

## Créer un réseau spécifique
> Afficher la liste des réseau
```
docker network list
```

> Créer un réseau
```
docker network create mon_reseau
```

> Afficher la liste des réseau
```
docker network list
```

*Par défaut, `mon_reseau` va fonctionner comme le réseau `bridge`*

> Relancer `ma_bdd` sur `mon_reseau`
```
docker run --rm --name ma_bdd --network mon_reseau -e POSTGRES_PASSWORD=dinumDocker2022 -d postgres:14-bullseye
```

> Relancer `pgadmin` sur `mon_reseau`
```
docker run --rm -p 8080:80 --name pgadmin --network mon_reseau -e PGADMIN_DEFAULT_EMAIL=dinum.sin.agents@gouv.nc -e PGADMIN_DEFAULT_PASSWORD=F0rmation -d dpage/pgadmin4
```

> Accèder à votre pgadmin via le port publié `8080`
via l'apercu web de cloudshell (en haut à droite)

> S'authentifier avec `dinum.sin.agents@gouv.nc` `F0rmation`

> Dans l'interface pgadmin, ajouter un serveur
* Dans l'onglet `General`
  * Name : `ma-bdd`
* Dans l'onglet `connection`
  * Host name/address : `ma_bdd`
  * Username : `postgres`
  * Password : `dinumDocker2022`
* `Save`

> Tester la connection

*Les réseaux spécifiques permettent la résolution des noms de container (ici `ma_bdd`)*

> Arrêter les containers
```
docker stop ma_bdd pgadmin
```