# TP3 : Automatisation et gestion de conf

## I. Premiers pas Ansible

### 1. Mise en place

#### A. Setup Azure

🌞 Les deux fichiers en compte-rendu

main.tf :

    provider "azurerm" {
      features {}
      subscription_id = "13d5e082-0b50-43df-ae72-234ed0d6ae90"
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

