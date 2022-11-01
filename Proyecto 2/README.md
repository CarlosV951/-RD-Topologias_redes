# Proyecto 2
## Integrantes Grupo 3

| Nombre | Carnet |
| ------ | ------ |
| Carlos Antonio Velasquez Castellanos | 201403654 |
| Oscar Augusto Perez Tzunun | 201213498 |
| Daniel Enrique Santos Godoy | 201325512 |



## Topologia 1

![image](https://user-images.githubusercontent.com/57165427/199163094-178934eb-f55e-4833-8045-5fd54e1b1396.png)


## Configuracion del HSRP

## R4

```sh
conf t
int f1/0
ip address 10.3.0.1 255.255.255.240
standby 0 ip 10.3.0.3
standby priority 100
do write
end
copy run start

```

## R5

```sh
conf t
int f1/0
ip address 10.3.0.2 255.255.255.240
standby 0 ip 10.3.0.3
standby priority 99
do write
end
copy run start

```

## Configuracion del GLBP

## R3

```sh
conf t
int f1/0
ip address 10.3.0.4 255.255.255.240
glbp 10 ip 10.3.0.6
glbp 10 preempt
glbp 10 priority 250
glbp 10 timers 5 18
glbp 10 load-balancing host-dependent
no shut
exit
do write
end
copy run start

```

## R2

```sh
conf t
int f1/0
ip address 10.3.0.5 255.255.255.240
glbp 10 ip 10.3.0.6
glbp 10 preempt
glbp 10 priority 249
glbp 10 timers 5 18
glbp 10 load-balancing host-dependent
no shut
exit
do write
end
copy run start

```

## Topologia 2






## Topologia 3

![image](https://user-images.githubusercontent.com/57165427/198360753-3ba30131-d46c-48a0-826d-660c025be167.png)

##

## Configuracion de los server

##
| Paso  | Descripcion | Comando / Imagen | 
| ------ | ------ | ------ | 
| 1 | Creacion de la maquina virtual de los servicios, se conecto con el adaptador de red virtual para ser utilizado posteriormente con gns3. | ![image](https://user-images.githubusercontent.com/57165427/186697536-e4c97cbe-14aa-4852-b659-328e352d207e.png) | 
| 2 | Creacion de la maquina virtual de servidor de dns, se conecto con el adaptador de red virtual para ser utilizado posteriormente con gns3.  | ![image](https://user-images.githubusercontent.com/57165427/186698609-56eb95aa-7ed0-4118-a818-422fd05694ec.png) | 
| 3 | Instalacion de ubuntu en las maquinas virtuales.  | ![image](https://user-images.githubusercontent.com/57165427/186699578-3c6b68e5-d987-457a-b4ab-d28e3561be3d.png) | 
| 4 | Actualizamos paquetes en ubuntu  | ![image](https://user-images.githubusercontent.com/57165427/186700181-cc913da4-20c2-4991-b001-9081f3f01efc.png) | 
| 5 | Instalamos net stat para utilizar ifconfig  | ![image](https://user-images.githubusercontent.com/57165427/186700547-00c8ccd1-b24d-4d2e-b3f9-d1bc100642d5.png) |

## Iniciar el servidor de backend
```sh

pm2 start server.js

```

## Configuracion del servidor DNS
```sh

# sudo apt update
# sudo apt upgrade
# sudo apt install bind9 bind9-utils nano
# systemctl status bind9
# sudo ufw allow bind9
# sudo nano /etc/bind/named.conf.options
# sudo nano /etc/default/named
# sudo named-checkconf
# sudo systemctl restart bind9
# systemctl status bind9
# sudo nano /etc/bind/named.conf.local
# sudo mkdir /etc/bind/zonas
# sudo nano /etc/bind/zonas/db.networld.cu
# sudo nano /etc/bind/zonas/db.10.10.20
# sudo named-checkzone networld.cu /etc/bind/zonas/db.networld.cu
# sudo named-checkzone db.20.10.10.in-addr.arpa /etc/bind/zonas/db.10.10.20
# sudo systemctl restart bind9
ping www.servicios.redes


```


## Configuracion de las VLAN
##
## ESW2
```sh
conf t 
vlan 10
name RHUMANOS
exit

vlan 20
name CONTABILIDAD
exit

vlan 30
name VENTAS
exit

vlan 40
name INFORMATICA
exit

end
```

## Configuracion del modo access
## ESW2
```sh
Conf t
Int fa1/2
Switchport mode Access
Switchport Access vlan 10
Do wri
End

Conf t
Int fa1/1
Switchport mode Access
Switchport Access vlan 20
Do wri
End

Conf t
Int fa1/4
Switchport mode Access
Switchport Access vlan 30
Do wri
End

Conf t
Int fa1/5
Switchport mode Access
Switchport Access vlan 30
Do wri
End

Conf t
Int fa1/6
Switchport mode Access
Switchport Access vlan 30
Do wri
End

Conf t
Int fa1/3
Switchport mode Access
Switchport Access vlan 40
Do wri
End

copy running-config startup-config
```

## Asignarle ip a las interfaces vlan
## ESW2
```sh
Conf t
Int vlan 10
ip address 192.168.35.17 255.255.255.240
no shutdown
exit

Conf t
Int vlan 20
ip address 192.168.35.36 255.255.255.240
no shutdown
exit

Conf t
Int vlan 30
ip address 192.168.35.49 255.255.255.240
no shutdown
exit


Conf t
Int vlan 40
ip address 192.168.35.65 255.255.255.240
no shutdown
exit

do write
copy running-config startup-config
```

## Configuracion del etherswitch hacia router
## ESW2
```sh
conf t

int fa 1/0
no switchport
ip address 192.168.35.2 255.255.255.240
no shutdown
exit

do write
copy running-config startup-config
```

## Configuracion del router hacia etherswitch
## R6
```sh
conf t

int fa 0/0
ip address 192.168.35.1 255.255.255.240
no shutdown
exit

do write
copy running-config startup-config
```







