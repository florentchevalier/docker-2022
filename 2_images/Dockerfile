FROM nginx:stable

RUN apt-get update && apt-get install -y caca-utils && rm -rf /var/lib/apt/lists/*

COPY --chown=nginx:nginx html /usr/share/nginx/html
ADD --chown=nginx:nginx https://api.thecatapi.com/v1/images/search?format=src /usr/share/nginx/html/cat.jpg
