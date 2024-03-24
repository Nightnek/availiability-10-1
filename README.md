# 10-1 Стасенко Григорий Домашнее задание к занятию «Disaster recovery и Keepalived» 10-1

## Задание 1

![image](https://github.com/Nightnek/availiability-10-1/assets/127677631/67b65246-f13a-49a0-8d6a-0b985d1677a4)



---

## Задание 2

 
скрипты для настройки Keepalived:

Main:

````
global_defs {
        enable_script_security
}

vrrp_script myhealth {
        script "/usr/local/bin/healthch.sh"
        interval 3
        user nobody
        }

vrrp_instance VI_1 {
        state MASTER
        interface enp0s3
        virtual_router_id 15
        priority 255
        advert_int 1

        virtual_ipaddress {
             192.168.0.100/24
        }
        track_script {
        myhealth
        }
````

Backup:

````
vrrp_instance VI_1 {
        state BACKUP
        interface enp0s3
        virtual_router_id 15
        priority 205
        advert_int 1

        virtual_ipaddress {
             192.168.0.100/24
        }

}
````

Script:

````
#!/bin/bash

/bin/nc -z -w 2 127.0.0.1 80 && [ -f /var/www/html/index.nginx-debian.html ]
````

![image](https://github.com/Nightnek/availiability-10-1/assets/127677631/c83b708f-2327-457b-8b78-3cdda6ef76e9)
![image](https://github.com/Nightnek/availiability-10-1/assets/127677631/f1596a70-81bf-4c97-8bb4-ac8f464bacf2)


---

## Задание 3


---

## Задание 4



