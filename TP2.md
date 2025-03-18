# TP 2

## Part I : Programmatic approach

### I. Premiers pas

🌞 Créez une VM depuis le Azure CLI

    az vm create -g GroupeJSPCloud -n big_vm --image Ubuntu2204 --size Standard_B1s --admin-username mierukey --ssh-key-values "C:\Users\killi\.ssh\id_rsa.pub"

Ma VM "big_vm" est bien visible sur l'interface azure.

🌞 Assurez-vous que vous pouvez vous connecter à la VM en SSH sur son IP publique.

    mierukey@bigvm:~$ sudo systemctl status walinuxagent
    ● walinuxagent.service - Azure Linux Agent
         Loaded: loaded (/lib/systemd/system/walinuxagent.service; enabled; vendor preset:>
         Active: active (running) since Tue 2025-03-18 09:23:51 UTC; 3min 12s ago
       Main PID: 733 (python3)
          Tasks: 6 (limit: 1003)
         Memory: 41.2M
            CPU: 1.801s
         CGroup: /system.slice/walinuxagent.service
                 ├─ 733 /usr/bin/python3 -u /usr/sbin/waagent -daemon
                 └─1023 python3 -u bin/WALinuxAgent-2.12.0.2-py3.9.egg -run-exthandlers

    Mar 18 09:23:59 bigvm python3[1023]:     pkts      bytes target     prot opt in     ou>
    Mar 18 09:23:59 bigvm python3[1023]:        0        0 ACCEPT     tcp  --  *      *   >
    Mar 18 09:23:59 bigvm python3[1023]:       96    13090 ACCEPT     tcp  --  *      *   >
    Mar 18 09:23:59 bigvm python3[1023]:        0        0 DROP       tcp  --  *      *   >
    Mar 18 09:23:59 bigvm python3[1023]: 2025-03-18T09:23:59.302588Z INFO ExtHandler ExtHa>
    Mar 18 09:23:59 bigvm python3[1023]: 2025-03-18T09:23:59.303374Z INFO ExtHandler ExtHa>
    Mar 18 09:23:59 bigvm python3[1023]: 2025-03-18T09:23:59.303657Z INFO ExtHandler ExtHa>
    Mar 18 09:23:59 bigvm python3[1023]: 2025-03-18T09:23:59.307087Z INFO ExtHandler ExtHa>
    Mar 18 09:23:59 bigvm python3[1023]: 2025-03-18T09:23:59.355113Z INFO ExtHandler ExtHa>
    Mar 18 09:23:59 bigvm python3[1023]: 2025-03-18T09:23:59.749095Z INFO ExtHandler ExtHa
#
    mierukey@bigvm:~$ cloud-init status --wait
    status: done

### II. Un ptit LAN

Ping de la VM 1 vers la VM 2 : 

    mierukey@vm2:~$ ping 10.0.0.6
    PING 10.0.0.6 (10.0.0.6) 56(84) bytes of data.
    64 bytes from 10.0.0.6: icmp_seq=1 ttl=64 time=28.9 ms
    64 bytes from 10.0.0.6: icmp_seq=2 ttl=64 time=7.01 ms
    ^C
    --- 10.0.0.6 ping statistics ---
    2 packets transmitted, 2 received, 0% packet loss, time 1001ms
    rtt min/avg/max/mdev = 7.005/17.941/28.878/10.936 ms
#
    mierukey@vm1:~$ ping 10.0.0.4
    PING 10.0.0.4 (10.0.0.4) 56(84) bytes of data.
    64 bytes from 10.0.0.4: icmp_seq=1 ttl=64 time=2.92 ms
    64 bytes from 10.0.0.4: icmp_seq=2 ttl=64 time=0.903 ms
    ^C
    --- 10.0.0.4 ping statistics ---
    2 packets transmitted, 2 received, 0% packet loss, time 1002ms
    rtt min/avg/max/mdev = 0.903/1.911/2.920/1.008 ms

## Part II : cloud-init

### 2. Gooooo

🌞 Tester cloud-init

Avec le fichier cloud-init.txt : 

    #cloud-config
    users:
      - default
      - name: mierukeybis
        sudo: false
        shell: /bin/bash
        ssh_authorized_keys:
          - <clé publique>

J'ai fais :

    az vm create -g GroupeJSPCloud -n vm --image Ubuntu2204 --size Standard_B1s --admin-username mierukey --ssh-key-values "C:\Users\killi\.ssh\id_rsa.pub" --custom-data "C:\Users\killi\OneDrive\Bureau\Père\B2\Cloud\cloud-init.txt"

🌞 Vérifier que cloud-init a bien fonctionné

    PS C:\Users\killi> ssh -i C:\Users\killi\.ssh\id_rsa mierukeybis@20.169.9.170
    Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1021-azure x86_64)

     * Documentation:  https://help.ubuntu.com
     * Management:     https://landscape.canonical.com
     * Support:        https://ubuntu.com/pro

     System information as of Tue Mar 18 10:38:44 UTC 2025

      System load:  0.02              Processes:             108
      Usage of /:   5.2% of 28.89GB   Users logged in:       0
      Memory usage: 31%               IPv4 address for eth0: 10.0.0.4
      Swap usage:   0%


    Expanded Security Maintenance for Applications is not enabled.

    0 updates can be applied immediately.

    Enable ESM Apps to receive additional future security updates.
    See https://ubuntu.com/esm or run: sudo pro status


    The list of available updates is more than a week old.
    To check for new updates run: sudo apt update
    New release '24.04.2 LTS' available.
    Run 'do-release-upgrade' to upgrade to it.



    The programs included with the Ubuntu system are free software;
    the exact distribution terms for each program are described in the
    individual files in /usr/share/doc/*/copyright.

    Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
    applicable law.

    mierukeybis@vm:~$

### 3. Write your own

🌞 Utilisez cloud-init pour préconfigurer la VM :

cloud-init.txt :

    #cloud-config
    users:
      - default
      - name: mierukey
        sudo: false
        lock_passwd: false
        passwd: "$6$rounds=656000$lCrdXDksMuxSdpxM$EMoIYI3TbFhw8yVxdK8nZhkNrQUPUjji2xLoqbWGh50BCoEn/NqXclvDWcXnSrfsXnOy7kSLfbZIccDoTjMSu/"
        shell: /bin/bash
        ssh_authorized_keys:
          - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCjJx4EyHLlx7A5UqSu56YOXzMp5Tg8uIr+agmVGjzh1j6Gj9msUQfS2p1/jaGHbktXOjPdzIH/hJcU7B4+OXdHqqfSickOY/EvqNqRkhUnN2XSESgUCUDA6RzgvdZDPXqHGYH8P1uAHnuTajz+4XaVs8YqZE2THlkEpdH0cEeaR3pyw5cFfigOjYUVR62EPMye/jn3/nltC21GMBc+u0ua4CJI+GMIuLh/XO84sVO4s4Y/PqMaiaDlGj6NYdG7rZqDn5Be7B/ZMVeqeEsugHjAIil/mc1oSlLm6UjNwHlT/BCHTq0JkULhmLA///CHp8O/NuD1h3XaDJuOe6Tl+Mwp

    runcmd:
      - sudo apt-get update
      - sudo apt-get install ca-certificates curl
      - sudo install -m 0755 -d /etc/apt/keyrings
      - sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
      - sudo chmod a+r /etc/apt/keyrings/docker.asc
      - echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      - sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
      - sudo usermod -aG docker mierukey
      - docker pull alpine:latest

Commande : 

    az vm create -g GroupeJSPCloud -n vm2 --image Ubuntu2204 --size Standard_B1s --admin-username administrateur --ssh-key-values "C:\Users\killi\.ssh\id_rsa.pub" --custom-data "C:\Users\killi\OneDrive\Bureau\Père\B2\Cloud\cloud-init.txt"

## Part III : Terraform

### 2. Copy paste

🌞 Constater le déploiement

    az>> az vm show --name tp2magueule-vm --resource-group tp2magueule-resources -o table
    Name            ResourceGroup          Location    Zones
    --------------  ---------------------  ----------  -------
    tp2magueule-vm  tp2magueule-resources  westeurope

### 3. Do it yourself

🌞 Créer un plan Terraform avec les contraintes suivantes

Avec ce main.tf : 

    provider "azurerm" {
      features {}
      subscription_id = "id-azure-absent-car-privé"
    }
    resource "azurerm_resource_group" "main" {
      name     = "${var.prefix}-resources"
      location = var.location
    }
    resource "azurerm_virtual_network" "main" {
      name                = "${var.prefix}-network"
      address_space       = ["10.0.0.0/16"]
      location            = azurerm_resource_group.main.location
      resource_group_name = azurerm_resource_group.main.name
    }
    resource "azurerm_subnet" "internal" {
      name                 = "internal"
      resource_group_name  = azurerm_resource_group.main.name
      virtual_network_name = azurerm_virtual_network.main.name
      address_prefixes     = ["10.0.2.0/24"]
    }
    resource "azurerm_public_ip" "node1_pip" {
      name                = "${var.prefix}-node1-pip"
      resource_group_name = azurerm_resource_group.main.name
      location            = azurerm_resource_group.main.location
      allocation_method   = "Static"
    }
    resource "azurerm_network_interface" "node1_nic" {
      name                = "${var.prefix}-node1-nic1"
      resource_group_name = azurerm_resource_group.main.name
      location            = azurerm_resource_group.main.location
      ip_configuration {
        name                          = "primary"
        subnet_id                     = azurerm_subnet.internal.id
        private_ip_address_allocation = "Dynamic"
        public_ip_address_id          = azurerm_public_ip.node1_pip.id
      }
    }
    resource "azurerm_network_interface" "node2_nic" {
      name                = "${var.prefix}-node2-nic"
      resource_group_name = azurerm_resource_group.main.name
      location            = azurerm_resource_group.main.location
      ip_configuration {
        name                          = "internal"
        subnet_id                     = azurerm_subnet.internal.id
        private_ip_address_allocation = "Dynamic"
      }
    }
    resource "azurerm_network_security_group" "ssh" {
      name                = "ssh"
      location            = azurerm_resource_group.main.location
      resource_group_name = azurerm_resource_group.main.name
      security_rule {
        access                     = "Allow"
        direction                  = "Inbound"
        name                       = "ssh"
        priority                   = 100
        protocol                   = "Tcp"
        source_port_range          = "*"
        source_address_prefix      = "*"
        destination_port_range     = "22"
        destination_address_prefix = "*"
      }
    }
    resource "azurerm_network_interface_security_group_association" "node1_assoc" {
      network_interface_id      = azurerm_network_interface.node1_nic.id
      network_security_group_id = azurerm_network_security_group.ssh.id
    }
    resource "azurerm_network_interface_security_group_association" "node2_assoc" {
      network_interface_id      = azurerm_network_interface.node2_nic.id
      network_security_group_id = azurerm_network_security_group.ssh.id
    }
    resource "azurerm_linux_virtual_machine" "node1" {
      name                            = "${var.prefix}-node1"
      resource_group_name             = azurerm_resource_group.main.name
      location                        = azurerm_resource_group.main.location
      size                            = "Standard_F2"
      admin_username                  = "mierukey"
      network_interface_ids = [
        azurerm_network_interface.node1_nic.id
      ]
      admin_ssh_key {
        username   = "mierukey"
        public_key = file("C:\\Users\\killi\\.ssh\\id_rsa.pub")
      }
      source_image_reference {
        publisher = "Canonical"
        offer     = "0001-com-ubuntu-server-jammy"
        sku       = "22_04-lts"
        version   = "latest"
      }
      os_disk {
        storage_account_type = "Standard_LRS"
        caching              = "ReadWrite"
      }
    }
    resource "azurerm_linux_virtual_machine" "node2" {
      name                  = "${var.prefix}-node2"
      resource_group_name   = azurerm_resource_group.main.name
      location              = azurerm_resource_group.main.location
      size                  = "Standard_F2"
      admin_username        = "mierukey"
      network_interface_ids = [azurerm_network_interface.node2_nic.id]

      admin_ssh_key {
        username   = "mierukey"
        public_key = file("C:\\Users\\killi\\.ssh\\id_rsa.pub")
      }

      source_image_reference {
        publisher = "Canonical"
        offer     = "0001-com-ubuntu-server-jammy"
        sku       = "22_04-lts"
        version   = "latest"
      }

      os_disk {
        storage_account_type = "Standard_LRS"
        caching              = "ReadWrite"
      }
    }

et ce variables.tf :

    variable "prefix" {
      description = "da prefix"
      default = "citron"
    }
    variable "location" {
      description = "da location"
      default = "West Europe"
    }

En faisant : 

    ssh -J 20.160.83.223 10.0.2.4

J'obtiens :

    PS C:\Users\killi> ssh -J mierukey@20.160.83.223 mierukey@10.0.2.4
    The authenticity of host '10.0.2.4 (<no hostip for proxy command>)' can't be established.
    ED25519 key fingerprint is SHA256:ABsbzRKju780lbydpqleQS8xpNP0wxxsIKUXVnNCaX8.
    This key is not known by any other names.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added '10.0.2.4' (ED25519) to the list of known hosts.
    Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 6.8.0-1021-azure x86_64)

     * Documentation:  https://help.ubuntu.com
     * Management:     https://landscape.canonical.com
     * Support:        https://ubuntu.com/pro

     System information as of Tue Mar 18 14:20:41 UTC 2025

      System load:  0.0               Processes:             123
      Usage of /:   5.2% of 28.89GB   Users logged in:       0
      Memory usage: 7%                IPv4 address for eth0: 10.0.2.4
      Swap usage:   0%

    Expanded Security Maintenance for Applications is not enabled.

    0 updates can be applied immediately.

    Enable ESM Apps to receive additional future security updates.
    See https://ubuntu.com/esm or run: sudo pro status


    The list of available updates is more than a week old.
    To check for new updates run: sudo apt update


    The programs included with the Ubuntu system are free software;
    the exact distribution terms for each program are described in the
    individual files in /usr/share/doc/*/copyright.

    Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
    applicable law.

    To run a command as administrator (user "root"), use "sudo <command>".
    See "man sudo_root" for details.

    mierukey@citron-node2:~$

### 4. cloud-iniiiiiiiiiiiiit

🌞 Intégrer la gestion de cloud-init



