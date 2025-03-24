# TP3 : Automatisation et gestion de conf

## I. Premiers pas Ansible

### 1. Mise en place

#### A. Setup Azure

🌞 Les deux fichiers en compte-rendu

main.tf :

    provider "azurerm" {
      features {}
      subscription_id = "id-abonnement-azure"
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
    resource "azurerm_public_ip" "node2_pip" {
      name                = "${var.prefix}-node2-pip"
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
      name                = "${var.prefix}-node2-nic1"
      resource_group_name = azurerm_resource_group.main.name
      location            = azurerm_resource_group.main.location
      ip_configuration {
        name                          = "primary"
        subnet_id                     = azurerm_subnet.internal.id
        private_ip_address_allocation = "Dynamic"
        public_ip_address_id          = azurerm_public_ip.node2_pip.id
      }
    }
    resource "azurerm_network_security_group" "nsg" {
      name                = "nsg"
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
      network_security_group_id = azurerm_network_security_group.nsg.id
    }
    resource "azurerm_network_interface_security_group_association" "node2_assoc" {
      network_interface_id      = azurerm_network_interface.node2_nic.id
      network_security_group_id = azurerm_network_security_group.nsg.id
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
      custom_data = base64encode(file("cloud-init.txt"))
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
      name                            = "${var.prefix}-node2"
      resource_group_name             = azurerm_resource_group.main.name
      location                        = azurerm_resource_group.main.location
      size                            = "Standard_F2"
      admin_username                  = "mierukey"
      network_interface_ids = [
        azurerm_network_interface.node2_nic.id
      ]
      admin_ssh_key {
        username   = "mierukey"
        public_key = file("C:\\Users\\killi\\.ssh\\id_rsa.pub")
      }
      custom_data = base64encode(file("cloud-init.txt"))
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

variables.tf :

    variable "prefix" {
      description = "da prefix"
      default = "citron"
    }
    variable "location" {
      description = "da location"
      default = "West Europe"
    }

cloud-init.txt : 

    #cloud-config
    users:
      - name: mierukinit
        sudo:
          - ALL=(ALL) NOPASSWD:ALL
        lock_passwd: false
        passwd: "$6$rounds=656000$lCrdXDksMuxSdpxM$EMoIYI3TbFhw8yVxdK8nZhkNrQUPUjji2xLoqbWGh50BCoEn/NqXclvDWcXnSrfsXnOy7kSLfbZIccDoTjMSu/"
        shell: /bin/bash
        ssh_authorized_keys:
          - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCjJx4EyHLlx7A5UqSu56YOXzMp5Tg8uIr+agmVGjzh1j6Gj9msUQfS2p1/jaGHbktXOjPdzIH/hJcU7B4+OXdHqqfSickOY/EvqNqRkhUnN2XSESgUCUDA6RzgvdZDPXqHGYH8P1uAHnuTajz+4XaVs8YqZE2THlkEpdH0cEeaR3pyw5cFfigOjYUVR62EPMye/jn3/nltC21GMBc+u0ua4CJI+GMIuLh/XO84sVO4s4Y/PqMaiaDlGj6NYdG7rZqDn5Be7B/ZMVeqeEsugHjAIil/mc1oSlLm6UjNwHlT/BCHTq0JkULhmLA///CHp8O/NuD1h3XaDJuOe6Tl+Mwp
    
    package_update: true
    package_upgrade: true
    packages:
      - python3
      - python3-pip
      - git
    
    runcmd:
      - pip install ansible
      - git clone https://github.com/holmanb/vmboot.git /opt/vmboot
      - cd /opt/vmboot && ansible-playbook ubuntu.yml

#### B. Setup sur votre poste

Fait

### 2. La commande ansible

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible-inventory -i hosts.ini --list
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an
    ansible.cfg source. For more information see
    https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-
    writable-dir
    {
        "_meta": {
            "hostvars": {
                "52.174.139.157": {
                    "ansible_ssh_private_key_file": "/mnt/c/Users/killi/.ssh/id_rsa",
                    "ansible_user": "mierukinit"
                },
                "52.232.20.134": {
                    "ansible_ssh_private_key_file": "/mnt/c/Users/killi/.ssh/id_rsa",
                    "ansible_user": "mierukinit"
                }
            }
        },
        "all": {
            "children": [
                "ungrouped",
                "tp3"
            ]
        },
        "tp3": {
            "hosts": [
                "52.174.139.157",
                "52.232.20.134"
            ]
        }
    }
#
    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible all -m ping -i hosts.ini
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an
    ansible.cfg source. For more information see
    https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-
    writable-dir
    52.174.139.157 | SUCCESS => {
        "ansible_facts": {
            "discovered_interpreter_python": "/usr/bin/python3"
        },
        "changed": false,
        "ping": "pong"
    }
    52.232.20.134 | SUCCESS => {
        "ansible_facts": {
            "discovered_interpreter_python": "/usr/bin/python3"
        },
        "changed": false,
        "ping": "pong"
    }
#
    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible -i hosts.ini tp3 -m setup
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an
    ansible.cfg source. For more information see
    https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-
    writable-dir
    52.174.139.157 | SUCCESS => {
        "ansible_facts": {
            "ansible_all_ipv4_addresses": [
                "10.0.2.4"
            ],
            "ansible_all_ipv6_addresses": [
                "fe80::7e1e:52ff:fe73:1677"
            ],
            "ansible_apparmor": {
                "status": "enabled"
            },
            "ansible_architecture": "x86_64",
            "ansible_bios_date": "12/07/2018",
            "ansible_bios_vendor": "American Megatrends Inc.",
            "ansible_bios_version": "090008",
            "ansible_board_asset_tag": "NA",
            "ansible_board_name": "Virtual Machine",
            "ansible_board_serial": "NA",
            "ansible_board_vendor": "Microsoft Corporation",
            "ansible_board_version": "7.0",
            ...
#
    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible -i hosts.ini tp3 -m command -a 'uptime'
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an
    ansible.cfg source. For more information see
    https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-
    writable-dir
    52.232.20.134 | CHANGED | rc=0 >>
     13:41:33 up  1:20,  1 user,  load average: 0.00, 0.00, 0.00
    52.174.139.157 | CHANGED | rc=0 >>
     13:41:33 up  1:46,  1 user,  load average: 0.00, 0.00, 0.00

### 3. Un premier playbook

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible-playbook -i hosts.ini first.yml
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an
    ansible.cfg source. For more information see
    https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-
    writable-dir
    
    PLAY [Install nginx] ******************************************************************
    
    TASK [Gathering Facts] ****************************************************************
    ok: [52.232.20.134]
    ok: [52.174.139.157]
    
    TASK [Install nginx] ******************************************************************
    changed: [52.174.139.157]
    changed: [52.232.20.134]
    
    TASK [Insert Index Page] **************************************************************
    changed: [52.174.139.157]
    changed: [52.232.20.134]
    
    TASK [Start NGiNX] ********************************************************************
    ok: [52.174.139.157]
    ok: [52.232.20.134]
    
    PLAY RECAP ****************************************************************************
    52.174.139.157             : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
    52.232.20.134              : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

### 4. Création de nouveaux playbooks

#### A. NGINX

nginx.yml : 

    ---
    - name: Déployer nginx
      hosts: tp3
      become: true
    
      tasks:
      - name: Installer nginx
        apt:
          name: nginx
          state: present
          update_cache: yes
    
      - name: Creer les dossiers de certificat
        file:
          path: "{{ item }}"
          state: directory
          owner: root
          group: root
          mode: '0755'
        loop:
          - /etc/pki/tls/certs
          - /etc/pki/tls/private
    
      - name: Generer les certificats auto-signés
        command: >
          openssl req -x509 -nodes -days 365 -newkey rsa:2048
          -keyout /etc/pki/tls/private/nginx-selfsigned.key
          -out /etc/pki/tls/certs/nginx-selfsigned.crt
          -subj "/CN=example.com"
    
      - name: créer le dossier racine du serv web
        file:
          path: /var/www/tp3_site
          state: directory
          owner: www-data
          group: www-data
          mode: '0755'
    
      - name: Créer la page index.html de base
        copy:
          dest: /var/www/tp3_site/index.html
          content: "Oups la bouleeeeette"
          owner: www-data
          group: www-data
          mode: '0644'
    
      - name: Déployer le fichier de conf
        copy:
          dest: /etc/nginx/sites-available/tp3_site
          content: |
            server {
                listen 443 ssl;
                server_name example.com;
    
                ssl_certificate /etc/pki/tls/certs/nginx-selfsigned.crt;
                ssl_certificate_key /etc/pki/tls/private/nginx-selfsigned.key;
    
                root /var/www/tp3_site;
                index index.html;
    
                location / {
                    try_files $uri $uri/ =404;
                }
            }
          owner: root
          group: root
          mode: '0644'
    
      - name: Activer la conf
        file:
          src: /etc/nginx/sites-available/tp3_site
          dest: /etc/nginx/sites-enabled/tp3_site
          state: link
    
      - name: Redémarrer nginx
        systemd:
          name: nginx
          state: restarted
          enabled: yes
    
      - name: Ouverture du port 443
        ufw:
          rule: allow
          port: "443"
          proto: tcp

hosts.ini :

    [tp3]
    20.160.17.64 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa
    172.201.198.10 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa

    [web]
    20.160.17.64 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa

curl :

    PS C:\Users\killi\OneDrive\Bureau\Père\B2\Cloud\TP3> curl -k https://20.160.17.64
    Oups la bouleeeeette

#### B. MariaDB ou MySQL

mysql.yml :

    ---
    - name: Déployer MySQL
      hosts: db
      become: true
      tasks:
      - name: Installer MySQL
        ansible.builtin.apt:
          name: mysql-server
          state: present
          update_cache: yes

      - name: Installer PyMySQL pour régler l'erreur sur le module de MySQL
        ansible.builtin.apt:
          name: python3-pymysql
          state: present
          update_cache: yes

      - name: Démarrer et activer MySQL
        ansible.builtin.service:
          name: "mysql"
          state: started
          enabled: yes

      - name: Créer l'utilisateur
        community.mysql.mysql_user:
          name: mysqluser
          password: "modepassonsenfou"
          priv: "*.*:ALL"
          host: "%"
          state: present
          login_unix_socket: /var/run/mysqld/mysqld.sock

      - name: Créer la db
        community.mysql.mysql_db:
          name: db
          state: present
          login_user: mysqluser
          login_password: "modepassonsenfou"
          login_unix_socket: /var/run/mysqld/mysqld.sock

hosts.ini :

    [tp3]
    40.91.208.143 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa
    52.136.229.184 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa

    [web]
    40.91.208.143 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa

    [db]
    52.136.229.184 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa

## II. Range ta chambre

### 1. Structure du dépôt : inventaires

Test ansible-playbook :

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible-playbook -i inventories/vagrant_lab/hosts.ini mysql.yml --limit db
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an ansible.cfg source. For more
    information see https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-writable-dir

    PLAY [Déployer MySQL] **************************************************************************************************

    TASK [Gathering Facts] *************************************************************************************************
    ok: [51.124.246.64]

    TASK [Installer MySQL] *************************************************************************************************
    changed: [51.124.246.64]

    TASK [Installer PyMySQL pour régler l'erreur sur le module de MySQL] ***************************************************
    changed: [51.124.246.64]

    TASK [Démarrer et activer MySQL] ***************************************************************************************
    ok: [51.124.246.64]

    TASK [Créer l'utilisateur] *********************************************************************************************
    [WARNING]: Option column_case_sensitive is not provided. The default is now false, so the column's name will be
    uppercased. The default will be changed to true in community.mysql 4.0.0.
    changed: [51.124.246.64]

    TASK [Créer la db] *****************************************************************************************************
    changed: [51.124.246.64]

    PLAY RECAP *************************************************************************************************************
    51.124.246.64              : ok=6    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

### 2. Structure du dépôt : rôles

Test ansible-playbook :

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible-playbook -i inventories/vagrant_lab/hosts.ini playbooks/main.yml
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an ansible.cfg source. For more
    information see https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-writable-dir

    PLAY [tp3] *************************************************************************************************************

    TASK [Gathering Facts] *************************************************************************************************
    ok: [51.124.246.64]
    ok: [51.124.246.80]

    TASK [../roles/common : Install common packages] ***********************************************************************
    ok: [51.124.246.64] => (item=vim)
    ok: [51.124.246.80] => (item=vim)
    ok: [51.124.246.64] => (item=git)
    ok: [51.124.246.80] => (item=git)

    PLAY RECAP *************************************************************************************************************
    51.124.246.64              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
    51.124.246.80              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

### 3. Structure du dépôt : variables d'inventaire

Test ansible-playbook :

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible-playbook -i inventories/vagrant_lab/hosts.ini playbooks/main.yml
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an ansible.cfg source. For more
    information see https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-writable-dir

    PLAY [tp3] *************************************************************************************************************

    TASK [Gathering Facts] *************************************************************************************************
    ok: [51.124.246.80]
    ok: [51.124.246.64]

    TASK [../roles/common : Install common packages] ***********************************************************************
    ok: [51.124.246.80] => (item=vim)
    ok: [51.124.246.64] => (item=vim)
    ok: [51.124.246.80] => (item=git)
    ok: [51.124.246.64] => (item=git)
    ok: [51.124.246.64] => (item=rsync)

    PLAY RECAP *************************************************************************************************************
    51.124.246.64              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
    51.124.246.80              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

Test ansible-playbook :

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible-playbook -i inventories/vagrant_lab/hosts.ini playbooks/main.yml
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an ansible.cfg source. For more
    information see https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-writable-dir

    PLAY [tp3] *************************************************************************************************************

    TASK [Gathering Facts] *************************************************************************************************
    ok: [51.124.246.80]
    ok: [51.124.246.64]

    TASK [../roles/common : Install common packages] ***********************************************************************
    ok: [51.124.246.80] => (item=vim)
    ok: [51.124.246.64] => (item=vim)
    ok: [51.124.246.80] => (item=git)
    ok: [51.124.246.64] => (item=git)
    ok: [51.124.246.64] => (item=rsync)

    TASK [../roles/common : Create default users] **************************************************************************
    ok: [51.124.246.64] => (item=le_nain)
    ok: [51.124.246.80] => (item=le_nain)
    ok: [51.124.246.80] => (item=l_elfe)
    ok: [51.124.246.64] => (item=l_elfe)
    ok: [51.124.246.80] => (item=le_ranger)
    ok: [51.124.246.64] => (item=le_ranger)

    PLAY RECAP *************************************************************************************************************
    51.124.246.64              : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
    51.124.246.80              : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

### 4. Structure du dépôt : rôle avancé

Test ansible-playbook :

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible-playbook -i inventories/vagrant_lab/hosts.ini playbooks/main.yml
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an ansible.cfg source. For more
    information see https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-writable-dir

    PLAY [tp3] *************************************************************************************************************

    TASK [Gathering Facts] *************************************************************************************************
    ok: [51.124.246.80]
    ok: [51.124.246.64]

    TASK [../roles/common : Install common packages] ***********************************************************************
    ok: [51.124.246.80] => (item=vim)
    ok: [51.124.246.64] => (item=vim)
    ok: [51.124.246.80] => (item=git)
    ok: [51.124.246.64] => (item=git)
    ok: [51.124.246.64] => (item=rsync)

    TASK [../roles/common : Create default users] **************************************************************************
    ok: [51.124.246.80] => (item=le_nain)
    ok: [51.124.246.64] => (item=le_nain)
    ok: [51.124.246.80] => (item=l_elfe)
    ok: [51.124.246.64] => (item=l_elfe)
    ok: [51.124.246.80] => (item=le_ranger)
    ok: [51.124.246.64] => (item=le_ranger)

    PLAY [web] *************************************************************************************************************

    TASK [Gathering Facts] *************************************************************************************************
    ok: [51.124.246.80]

    TASK [../roles/nginx : Installer NGINX] ********************************************************************************
    ok: [51.124.246.80]

    TASK [../roles/nginx : Main NGINX config file] *************************************************************************
    ok: [51.124.246.80]

    TASK [../roles/nginx : Create webroot] *********************************************************************************
    changed: [51.124.246.80]

    TASK [../roles/nginx : Create index] ***********************************************************************************
    changed: [51.124.246.80]

    TASK [../roles/nginx : NGINX Virtual Host] *****************************************************************************
    changed: [51.124.246.80]

    PLAY RECAP *************************************************************************************************************
    51.124.246.64              : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
    51.124.246.80              : ok=9    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

curl : 

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ exit
    logout
    PS C:\Users\killi\OneDrive\Bureau\Père\B2\Cloud\TP3> curl http://74.234.226.219/
    <!DOCTYPE html>
    <html>
    <head>
    <title>Welcome to nginx!</title>
    <style>
        body {
            width: 35em;
            margin: 0 auto;
            font-family: Tahoma, Verdana, Arial, sans-serif;
        }
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

## III. Repeat

### 1. NGINX

vhosts.yml : 

    - name: Create webroot
      become: true
      file:
        path: "{{ item.nginx_webroot }}"
        state: directory
      loop: "{{ vhosts }}"

    - name: Create index
      become: true
      copy:
        dest: "{{ item.nginx_webroot }}/index.html"
        content: "{{ item.nginx_index_content }}"
      loop: "{{ vhosts }}"

    - name: NGINX Virtual Host
      become: true
      template:
        src: vhost.conf.j2
        dest: /etc/nginx/conf.d/{{ item.nginx_servername }}.conf
      loop: "{{ vhosts }}"
      notify: Restart Nginx

config.yml : 

    - name : Main NGINX config file
      become: true
      copy:
        src: nginx.conf
        dest: /etc/nginx/nginx.conf
      notify: Restart Nginx

vhost.conf.j2 :

    server {
            listen {{ item.nginx_port }} ;
            server_name {{ item.nginx_servername }};

            location / {
                root {{ item.nginx_webroot }};
                index index.html;
            }
    }

<IPSERVER>.yml :

    vhosts:
      - nginx_servername: test1
        nginx_port: 8082
        nginx_webroot: /var/www/html/test1
        nginx_index_content: "<h1>TEST 1</h1>"  
      - nginx_servername: test2
        nginx_port: 8083
        nginx_webroot: /var/www/html/test2
        nginx_index_content: "<h1>TEST 2</h1>"

Test ansible-playbook :

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ ansible-playbook -i inventories/vagrant_lab/hosts.ini  playbooks/main.yml
    [WARNING]: Ansible is being run in a world writable directory
    (/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible), ignoring it as an ansible.cfg source. For more
    information see https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-world-writable-dir

    PLAY [web] *************************************************************************************************************

    TASK [Gathering Facts] *************************************************************************************************
    ok: [4.180.152.124]

    TASK [../roles/nginx : Installer NGINX] ********************************************************************************
    ok: [4.180.152.124]

    TASK [../roles/nginx : Main NGINX config file] *************************************************************************
    changed: [4.180.152.124]

    TASK [../roles/nginx : Create webroot] *********************************************************************************
    ok: [4.180.152.124] => (item={'nginx_servername': 'test1', 'nginx_port': 8082, 'nginx_webroot': '/var/www/html/test1', 'nginx_index_content': '<h1>TEST 1</h1>'})
    ok: [4.180.152.124] => (item={'nginx_servername': 'test2', 'nginx_port': 8083, 'nginx_webroot': '/var/www/html/test2', 'nginx_index_content': '<h1>TEST 2</h1>'})

    TASK [../roles/nginx : Create index] ***********************************************************************************
    ok: [4.180.152.124] => (item={'nginx_servername': 'test1', 'nginx_port': 8082, 'nginx_webroot': '/var/www/html/test1', 'nginx_index_content': '<h1>TEST 1</h1>'})
    ok: [4.180.152.124] => (item={'nginx_servername': 'test2', 'nginx_port': 8083, 'nginx_webroot': '/var/www/html/test2', 'nginx_index_content': '<h1>TEST 2</h1>'})

    TASK [../roles/nginx : NGINX Virtual Host] *****************************************************************************
    ok: [4.180.152.124] => (item={'nginx_servername': 'test1', 'nginx_port': 8082, 'nginx_webroot': '/var/www/html/test1', 'nginx_index_content': '<h1>TEST 1</h1>'})
    ok: [4.180.152.124] => (item={'nginx_servername': 'test2', 'nginx_port': 8083, 'nginx_webroot': '/var/www/html/test2', 'nginx_index_content': '<h1>TEST 2</h1>'})

    RUNNING HANDLER [../roles/nginx : Restart Nginx] ***********************************************************************
    changed: [4.180.152.124]

    PLAY RECAP *************************************************************************************************************
    4.180.152.124              : ok=7    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

### 2. Common

tp3.yml : 

    users:
      - name: chevalier
        password: "$6$rounds=656000$lCrdXDksMuxSdpxM$EMoIYI3TbFhw8yVxdK8nZhkNrQUPUjji2xLoqbWGh50BCoEn/NqXclvDWcXnSrfsXnOy7kSLfbZIccDoTjMSu/"
        home: /home/chevalier
        ssh_key: chevalier.pub
      - name: samurai
        password: "$6$rounds=656000$lCrdXDksMuxSdpxM$EMoIYI3TbFhw8yVxdK8nZhkNrQUPUjji2xLoqbWGh50BCoEn/NqXclvDWcXnSrfsXnOy7kSLfbZIccDoTjMSu/"
        home: /home/samurai
        ssh_key: samurai.pub
      - name: roi
        password: "$6$rounds=656000$lCrdXDksMuxSdpxM$EMoIYI3TbFhw8yVxdK8nZhkNrQUPUjji2xLoqbWGh50BCoEn/NqXclvDWcXnSrfsXnOy7kSLfbZIccDoTjMSu/"
        home: /home/roi
        ssh_key: roi.pub

users.yml : 

    - name: Création du groupe admin
      become: true
      group:
        name: admin
        state: present

    - name: Création des utilisateurs
      become: true
      ansible.builtin.user:
        name: "{{ item.name }}"
        password: "{{ item.password }}"
        home: "{{ item.home }}"
        shell: /bin/bash
        groups: admin
        append: yes
        state: present
      loop: "{{ users }}"

    - name: Création des dossiers ssh
      become: true
      file:
        path: "{{ item.home }}/.ssh"
        state: directory
        owner: "{{ item.name }}"
        group: "{{ item.name }}"
        mode: '0700'
      loop: "{{ users }}"

    - name: Ajout des clés
      become: true
      copy:
        src: "ssh_keys/{{ item.ssh_key }}"
        dest: "{{ item.home }}/.ssh/authorized_keys"
        owner: "{{ item.name }}"
        group: "{{ item.name }}"
        mode: '0600'
      loop: "{{ users }}"

    - name: Ajout des utilisateus au groupe sudo
      become: true
      user:
        name: "{{ item.name }}"
        groups: sudo
        append: yes
      loop: "{{ users }}"

    - name: sudo sans mdp
      become: true
      lineinfile:
        path: /etc/sudoers
        regexp: '^%sudo'
        line: '%sudo ALL=(ALL) NOPASSWD: ALL'
        state: present
        validate: 'visudo -cf %s'

### 3. Dynamic loadbalancer

hosts.ini : 

    [webapp]
    20.126.128.197 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa
    20.126.35.186 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa

    [rproxy]
    20.126.35.192 ansible_user=mierukinit ansible_ssh_private_key_file=/mnt/c/Users/killi/.ssh/id_rsa

webapp.yml (Affiche l'ip du serveur pour savoir si le load balancing fonctionne) :

    vhosts:
      - nginx_servername: test
        nginx_port: 80
        nginx_webroot: /var/www/html/test
        nginx_index_content: "<!DOCTYPE html><html><head><title>Load Balancing Test</title></head><body><h1>Bienvenue !</h1><p>Ce serveur tourne sur l'IP : <span id='server-ip'></span></p><script> fetch(window.location.href, { method: 'HEAD' }).then(response => {document.getElementById('server-ip').innerText = response.headers.get('X-Server-IP');}).catch(error => console.error('Erreur:', error));</script></body></html>"

config.yml : 

    - name: Générer la configuration du reverse proxy
      become: true
      ansible.builtin.template:
        src: reverse_proxy.conf.j2
        dest: /etc/nginx/conf.d/reverse_proxy.conf
      notify: Restart nginx

reverse_proxy.conf.j2 :

    upstream application {
        server 20.126.128.197;
        server 20.126.35.186;
    }

    server {
        listen 8082;
        server_name 20.126.35.192;

        location / {
        
            proxy_pass http://application;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_cache_bypass $http_cache_control;
        }
    }

Je sais plus ce que j'ai modifié d'autre et j'ai la flemme de tout mettre je vais te montrer avec des curl :

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ curl -I http://104.45.11.218:8082/
    HTTP/1.1 200 OK
    Server: nginx/1.18.0 (Ubuntu)
    Date: Mon, 24 Mar 2025 16:47:24 GMT
    Content-Type: text/html
    Content-Length: 392
    Connection: keep-alive
    Last-Modified: Mon, 24 Mar 2025 16:45:18 GMT
    ETag: "67e18c1e-188"
    X-Server-IP: 10.0.2.5
    Accept-Ranges: bytes

    mierukey@Mierukey:/mnt/c/Users/killi/OneDrive/Bureau/Père/B2/Cloud/TP3/ansible$ curl -I http://104.45.11.218:8082/
    HTTP/1.1 200 OK
    Server: nginx/1.18.0 (Ubuntu)
    Date: Mon, 24 Mar 2025 16:47:39 GMT
    Content-Type: text/html
    Content-Length: 392
    Connection: keep-alive
    Last-Modified: Mon, 24 Mar 2025 16:45:18 GMT
    ETag: "67e18c1e-188"
    X-Server-IP: 10.0.2.6
    Accept-Ranges: bytes
