# TP Cloud

## Part I : Docker basics

### 1. Install

🌞 Installer Docker votre machine Azure :

Retirer les installations anciennes au cas où il y en aurait :

    azureuser@TP:~$ for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

Installation de Docker

    azureuser@TP:~$ sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update

Démarrage de Docker

    azureuser@TP:~$ sudo systemctl start docker

Ajout de l'utilsateur azureuser au groupe docker

    azureuser@TP:~$ sudo usermod -aG docker azureuser

### 3. Lancement de conteneurs

🌞 Utiliser la commande docker run

    azureuser@TP:~$ docker run -p 80:80 -d nginx
#
    azureuser@TP:~$ docker run -p 9999:80 -d nginx

🌞 Rendre le service dispo sur internet

    PS C:\Users\killi> curl http://20.168.8.136:9999/
    <!DOCTYPE html>
    <html>
    <head>
    <title>Welcome to nginx!</title>
    <style>
    html { color-scheme: light dark; }
    body { width: 35em; margin: 0 auto;
    font-family: Tahoma, Verdana, Arial, sans-serif; }
    </style>
    </head>
    <body>
    <h1>Welcome to nginx!</h1>
    <p>If you see this page, the nginx web server is successfully installed and
    working. Further configuration is required.</p>

    <p>For online documentation and support please refer to
    <a href="http://nginx.org/">nginx.org</a>.<br/>
    Commercial support is available at
    <a href="http://nginx.com/">nginx.com</a>.</p>

    <p><em>Thank you for using nginx.</em></p>
    </body>
    </html>
    
🌞 Custom un peu le lancement du conteneur

NGINX doit avoir un fichier de conf personnalisé pour écouter sur le port 7777 (pas le port 80 par défaut) :

Après avoir créé un fichier de conf basique "nginx2.conf" :

    azureuser@TP:/tp$ docker run -v $(pwd)/nginx2.conf:/etc/nginx/conf.d/nginx2.conf -p 80:7777 -d nginx

Après avoir créé un fichier "index.html" :

    azureuser@TP:/tp$ docker run -v $(pwd)/nginx2.conf:/etc/nginx/conf.d/nginx2.conf -v $(pwd)/index.html:/var/www/html/index.html -p 80:7777 -d nginx

l'application doit être joignable grâce à un partage de ports (vers le port 7777) :

    azureuser@TP:/tp$ docker run -v $(pwd)/nginx2.conf:/etc/nginx/conf.d/nginx2.conf -v $(pwd)/index.html:/var/www/html/index.html -p 7777:7777 -d nginx

Limiter l'utilisation de la RAM du conteneur à 512M :

    docker run -v $(pwd)/nginx2.conf:/etc/nginx/conf.d/nginx2.conf -v $(pwd)/index.html:/var/www/html/index.html --memory 512m -p 7777:7777 -d nginx

le conteneur devra avoir un nom : meow

    azureuser@TP:/tp$ docker run --name meow -v $(pwd)/nginx2.conf:/etc/nginx/conf.d/nginx2.conf -v $(pwd)/index.html:/var/www/html/index.html --memory 512m -p 7777:7777 -d nginx

## Part II : Images

### Construisez votre propre Dockerfile

🌞 Construire votre propre image

Dockerfile : 

    FROM debian

    RUN apt update -y

    RUN apt install -y apache2

    COPY index.html /var/www/html/

    ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
    
    EXPOSE 80

## Part III : docker-compose

### 2. WikiJS

🌞 Installez un WikiJS en utilisant Docker












