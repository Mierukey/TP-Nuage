# TP Cloud

## Part I : Docker basics

### 1. Install

🌞 Installer Docker votre machine Azure :

Retirer les installations anciennes au cas où il y en aurait :

    azureuser@TP:~$ for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

Installation de Docker

    sudo apt-get update
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

    
