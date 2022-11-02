# Proyecto 2
## Integrantes Grupo 3

| Nombre | Carnet |
| ------ | ------ |
| Carlos Antonio Velasquez Castellanos | 201403654 |
| Oscar Augusto Perez Tzunun | 201213498 |
| Daniel Enrique Santos Godoy | 201325512 |





## Topologia 1

![image](https://user-images.githubusercontent.com/57165427/199291552-5e0cf2b3-f430-449e-b6e3-59fe2e4b62cb.png)

## Subnetting topologia 1

| Subred | Network | Mask | P.Asignable | U.Asignable | Broadcast | Cantidad de hosts | Host totales |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- |
| 1 | 10.3.0.0   | 255.255.255.248 | 10.30.0.1   | 10.30.0.14  | 10.30.0.15  | 2  | 16  |
| 2 | 10.3.0.16  | 255.255.255.248 | 10.30.0.17  | 10.30.0.30  | 10.30.0.31  | 2  | 16  |
| 3 | 10.3.0.32  | 255.255.255.248 | 10.30.0.33  | 10.30.0.46  | 10.30.0.47  | 2  | 16  |
| 4 | 10.3.0.48  | 255.255.255.248 | 10.30.0.49  | 10.30.0.62  | 10.30.0.63  | 2  | 16  |
| 5 | 10.3.0.64  | 255.255.255.248 | 10.30.0.65  | 10.30.0.78  | 10.30.0.79  | 2  | 16  |

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

## Configuracion de las interfaces

## R4

```sh
conf t
int f1/1
ip address 10.3.0.49 255.255.255.240
no shut
do write
end
copy run start

```

## R5

```sh
conf t
int f1/1
ip address 10.3.0.65 255.255.255.240
no shut
do write
end
copy run start

```

## R3

```sh
conf t
int f1/1
ip address 10.3.0.17 255.255.255.240
no shut
exit
do write
end
copy run start

```

## R2

```sh
conf t
int f1/1
ip address 10.3.0.33 255.255.255.240
no shut
exit
do write
end
copy run start

```

## Ruteo estatico

## R4

```sh
conf t
conf t
ip route 10.3.0.16 255.255.255.240 10.3.0.6
ip route 10.3.0.32 255.255.255.240 10.3.0.6
ip route 192.168.34.128 255.255.255.128 10.3.0.18
ip route 192.168.34.48 255.255.255.240 10.3.0.18
ip route 192.168.34.0 255.255.255.224 10.3.0.18
ip route 192.168.34.64 255.255.255.192 10.3.0.18
ip route 192.168.34.128 255.255.255.128 10.3.0.34
ip route 192.168.34.48 255.255.255.240 10.3.0.34
ip route 192.168.34.0 255.255.255.224 10.3.0.34
ip route 192.168.34.64 255.255.255.192 10.3.0.34

ip route 192.168.35.16 255.255.255.240 10.3.0.50
ip route 192.168.35.32 255.255.255.240 10.3.0.50
ip route 192.168.35.48 255.255.255.240 10.3.0.50
ip route 192.168.35.64 255.255.255.240 10.3.0.50
ip route 192.168.35.16 255.255.255.240 10.3.0.66
ip route 192.168.35.32 255.255.255.240 10.3.0.66
ip route 192.168.35.48 255.255.255.240 10.3.0.66
ip route 192.168.35.64 255.255.255.240 10.3.0.66
do write
end
copy run start

```

## R5

```sh
conf t
conf t
ip route 10.3.0.16 255.255.255.240 10.3.0.6
ip route 10.3.0.32 255.255.255.240 10.3.0.6
ip route 192.168.34.128 255.255.255.128 10.3.0.18
ip route 192.168.34.48 255.255.255.240 10.3.0.18
ip route 192.168.34.0 255.255.255.224 10.3.0.18
ip route 192.168.34.64 255.255.255.192 10.3.0.18
ip route 192.168.34.128 255.255.255.128 10.3.0.34
ip route 192.168.34.48 255.255.255.240 10.3.0.34
ip route 192.168.34.0 255.255.255.224 10.3.0.34
ip route 192.168.34.64 255.255.255.192 10.3.0.34
ip route 192.168.35.16 255.255.255.240 10.3.0.50
ip route 192.168.35.32 255.255.255.240 10.3.0.50
ip route 192.168.35.48 255.255.255.240 10.3.0.50
ip route 192.168.35.64 255.255.255.240 10.3.0.50
ip route 192.168.35.16 255.255.255.240 10.3.0.66
ip route 192.168.35.32 255.255.255.240 10.3.0.66
ip route 192.168.35.48 255.255.255.240 10.3.0.66
ip route 192.168.35.64 255.255.255.240 10.3.0.66
do write
end
copy run start

```

## R3

```sh
conf t
ip route 10.3.0.48 255.255.255.240 10.3.0.3
ip route 10.3.0.64 255.255.255.240 10.3.0.3
ip route 192.168.34.128 255.255.255.128 10.3.0.18
ip route 192.168.34.48 255.255.255.240 10.3.0.18
ip route 192.168.34.0 255.255.255.224 10.3.0.18
ip route 192.168.34.64 255.255.255.192 10.3.0.18
ip route 192.168.34.128 255.255.255.128 10.3.0.34
ip route 192.168.34.48 255.255.255.240 10.3.0.34
ip route 192.168.34.0 255.255.255.224 10.3.0.34
ip route 192.168.34.64 255.255.255.192 10.3.0.34
ip route 192.168.35.16 255.255.255.240 10.3.0.50
ip route 192.168.35.32 255.255.255.240 10.3.0.50
ip route 192.168.35.48 255.255.255.240 10.3.0.50
ip route 192.168.35.64 255.255.255.240 10.3.0.50
ip route 192.168.35.16 255.255.255.240 10.3.0.66
ip route 192.168.35.32 255.255.255.240 10.3.0.66
ip route 192.168.35.48 255.255.255.240 10.3.0.66
ip route 192.168.35.64 255.255.255.240 10.3.0.66
do write
end
copy run start

```

## R2

```sh
conf t
ip route 10.3.0.48 255.255.255.240 10.3.0.3
ip route 10.3.0.64 255.255.255.240 10.3.0.3
ip route 192.168.34.128 255.255.255.128 10.3.0.18
ip route 192.168.34.48 255.255.255.240 10.3.0.18
ip route 192.168.34.0 255.255.255.224 10.3.0.18
ip route 192.168.34.64 255.255.255.192 10.3.0.18
ip route 192.168.34.128 255.255.255.128 10.3.0.34
ip route 192.168.34.48 255.255.255.240 10.3.0.34
ip route 192.168.34.0 255.255.255.224 10.3.0.34
ip route 192.168.34.64 255.255.255.192 10.3.0.34
ip route 192.168.35.16 255.255.255.240 10.3.0.50
ip route 192.168.35.32 255.255.255.240 10.3.0.50
ip route 192.168.35.48 255.255.255.240 10.3.0.50
ip route 192.168.35.64 255.255.255.240 10.3.0.50
ip route 192.168.35.16 255.255.255.240 10.3.0.66
ip route 192.168.35.32 255.255.255.240 10.3.0.66
ip route 192.168.35.48 255.255.255.240 10.3.0.66
ip route 192.168.35.64 255.255.255.240 10.3.0.66
do write
end
copy run start

```



## Topologia 2

![image](https://user-images.githubusercontent.com/57165427/199316110-eb7d90ae-46f9-4b82-85e9-4bf661e74c7b.png)

## Subnetting topologia 2

| Vlan | Network | Mask | P.Asignable | U.Asignable | Broadcast | Cantidad de hosts | Host totales |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- |
| 10 | 192.168.34.0   | 255.255.255.224 | 192.168.34.1   | 192.168.34.30  | 192.168.34.31  | 20  | 32  |
| 20 | 192.168.34.48  | 255.255.255.240 | 192.168.34.49  | 192.168.34.62  | 192.168.34.63  | 7   | 16  |
| 30 | 192.168.34.128 | 255.255.255.128 | 192.168.34.129 | 192.168.34.254 | 192.168.34.255 | 122 | 128 |
| 40 | 192.168.34.64  | 255.255.255.192 | 192.168.34.65  | 192.168.35.126 | 192.168.34.127 | 37  | 64  |

## Configuracion de las VLAN
##
## ESW1
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
do write

end
```


## Modo troncal
## ESW1
```sh
conf t
int f 1/0
switchport trunk encapsulation dot1q
switchport mode trunk
spanning-tree portfast trunk
exit

int f 1/1
switchport trunk encapsulation dot1q
switchport mode trunk
spanning-tree portfast trunk

exit
int f 1/2
switchport trunk encapsulation dot1q
switchport mode trunk
spanning-tree portfast trunk

do write
end
copy running-config startup-config
```

## Configuracion del router hacia etherswitch
## R6
```sh
conf t

int f 0/0
no shutdown
exit

int fastEthernet 0/0.10
encapsulation  dot1Q 10
ip address 192.168.34.1 255.255.255.224
no shut
do write
exit

int fastEthernet 0/0.20
encapsulation  dot1Q 20
ip address 192.168.34.49 255.255.255.240
no shut
do write
exit

int fastEthernet 0/0.30
encapsulation  dot1Q 30
ip address 192.168.34.129 255.255.255.128
no shut
do write
exit

int fastEthernet 0/0.40
encapsulation  dot1Q 40
ip address 192.168.34.65 255.255.255.192
no shut
do write
exit
end

copy running-config startup-config
```

## Configuracion del DHCP por vlan

```sh
interface fastEthernet 0/0.10
ip dhcp pool diez
network 192.168.34.0 255.255.255.224
default-router 192.168.34.1
exit
do write

interface fastEthernet 0/0.20
ip dhcp pool veinte
network 192.168.34.48 255.255.255.240
default-router 192.168.34.49
exit
do write

interface fastEthernet 0/0.30
ip dhcp pool treinta
network 192.168.34.128 255.255.255.128
default-router 192.168.34.129
exit
do write

interface fastEthernet 0/0.40
ip dhcp pool cuarenta
network 192.168.34.64 255.255.255.192
default-router 192.168.34.65
exit
do write

```

## Topologia 3

![image](https://user-images.githubusercontent.com/57165427/198360753-3ba30131-d46c-48a0-826d-660c025be167.png)


## Subnetting topologia 3

| Vlan | Network | Mask | P.Asignable | U.Asignable | Broadcast | Cantidad de hosts | Host totales |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- |
| 10 | 192.168.35.16 | 255.255.255.240 | 192.168.35.17 | 192.168.35.30 | 192.168.35.31 | 2 | 16 |
| 20 | 192.168.35.32 | 255.255.255.240 | 192.168.35.33 | 192.168.35.46 | 192.168.35.47 | 2 | 16 |
| 30 | 192.168.35.48 | 255.255.255.240 | 192.168.35.49 | 192.168.35.62 | 192.168.35.63 | 2 | 16 |
| 40 | 192.168.35.64 | 255.255.255.240 | 192.168.35.65 | 192.168.35.78 | 192.168.35.79 | 2 | 16 |

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
do write

end
```

## Configuracion del modo access
## ESW2
```sh
Conf t
Int fa1/1
Switchport mode Access
Switchport Access vlan 10
Do wri
End

Conf t
Int fa1/2
Switchport mode Access
Switchport Access vlan 20
Do wri
End

Conf t
Int fa1/3
Switchport mode Access
Switchport Access vlan 30
Do wri
End

Conf t
Int fa1/5
Switchport mode Access
Switchport Access vlan 40
Do wri
End



copy running-config startup-config
```

## Modo troncal hacia router
## ESW2
```sh
conf t
int f 1/0
switchport trunk encapsulation dot1q
switchport mode trunk
spanning-tree portfast trunk

do write
end
copy running-config startup-config
```

## Configuracion del router hacia etherswitch
## R6
```sh
conf t

int f 0/0
no shutdown
exit

int fastEthernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.35.17 255.255.255.240
no shut
do write
exit

int fastEthernet 0/0.20
encapsulation  dot1Q 20
ip address 192.168.35.33 255.255.255.240
no shut
do write
exit

int fastEthernet 0/0.30
encapsulation  dot1Q 30
ip address 192.168.35.49 255.255.255.240
no shut
do write
exit

int fastEthernet 0/0.40
encapsulation  dot1Q 40
ip address 192.168.35.65 255.255.255.240
no shut
do write
exit
end

copy running-config startup-config
```







