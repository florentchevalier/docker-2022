# TP 3 Volumes

# Travaux

## Volumes
> Dans le dossier `3_volumes`

> Lancer un container basé sur l'image nginx:alpine avec un volume contenant les fichiers html
```
docker run -p 8080:80 --name mon_site --rm -v $PWD/html:/usr/share/nginx/html nginx:alpine
```

> Accèder à votre page via le port publié
via l'apercu web de cloudshell (en haut à droite)

> Modifier le fichier `html/index.html`

> Recharger la page pour voir apparaitre la modification sans avoir à relancer le container

> Ctrl + C pour interrompre le process

## Variable d'environnement
> Lancer un container basé sur l'image postgres:14-bullseye
```
docker run --rm --name ma_bdd -e POSTGRES_PASSWORD=dinumDocker2022 -d postgres:14-bullseye
```

> Trouver l'ip du container
```
docker container inspect ma_bdd
```
ou
```
docker container inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ma_bdd
```

> Se connecter à la base avec la commande puis saisir le mot de passe défini dans la variable d'environnement `dinumDocker2022`
```
psql -h <IP> -U postgres
```

> Ctrl + D pour sortir de la commande psql

> Arrêter le container
```
docker stop ma_bdd
```
