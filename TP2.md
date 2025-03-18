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

    #cloud-config
    users:
      - default
      - name: mierukey
        sudo: false
        lock_passwd: false
        passwd: "$6$rounds=656000$lCrdXDksMuxSdpxM$EMoIYI3TbFhw8yVxdK8nZhkNrQUPUjji2xLoqbWGh50BCoEn/NqXclvDWcXnSrfsXnOy7kSLfbZIccDoTjMSu/"
        shell: /bin/bash
        ssh_authorized_keys:
          - ssh-rsa    AAAAB3NzaC1yc2EAAAADAQABAAABAQCjJx4EyHLlx7A5UqSu56YOXzMp5Tg8uIr+agmVGjzh1j6Gj9msUQfS2p1/jaGHbktXOjPdzIH/hJcU7B4+OXdHqqfSickOY/EvqNqRkhUnN2XSESgUCUDA6RzgvdZDPXqHGYH8P1uAHnuTajz+4XaVs8YqZE2THlkEpdH0cEeaR3pyw5cFfigOjYUVR62EPMye/jn3/nltC21GMBc+u0ua4CJI+GMIuLh/XO84sVO4s4Y/PqMaiaDlGj6NYdG7rZqDn5Be7B/ZMVeqeEsugHjAIil/mc1oSlLm6UjNwHlT/BCHTq0JkULhmLA///CHp8O/NuD1h3XaDJuOe6Tl+Mwp

    runcmd:
      - sudo apt-get update
      - sudo apt-get install ca-certificates curl
      - sudo install -m 0755 -d /etc/apt/keyrings
      - sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
      - sudo chmod a+r /etc/apt/keyrings/docker.asc
      - echo \
          "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      - sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
      - sudo usermod -aG docker mierukey
      - docker pull alpine:latest


