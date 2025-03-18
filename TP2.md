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

