# Proyecto 2
## Integrantes Grupo 3

| Nombre | Carnet |
| ------ | ------ |
| Carlos Antonio Velasquez Castellanos | 201403654 |
| Oscar Augusto Perez Tzunun | 201213498 |
| Daniel Enrique Santos Godoy | 201325512 |

## Topologia 3

![image](https://user-images.githubusercontent.com/57165427/198360753-3ba30131-d46c-48a0-826d-660c025be167.png)

##

## Configuracion del modo truncal
## ESW2
```sh
conf t

int fa 1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

do write
copy running-config startup-config
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

## Asignarle ip a las interfaces
## ESW2
```sh
Conf t
Int fa1/2
ip address 192.168.35.16 255.255.255.240
exit

Conf t
Int fa1/1
ip address 192.168.35.32 255.255.255.240
exit

Conf t
Int fa1/4
ip address 192.168.35.48 255.255.255.240
exit

Conf t
Int fa1/5
ip address 192.168.35.48 255.255.255.240
exit

Conf t
Int fa1/6
ip address 192.168.35.48 255.255.255.240
exit

Conf t
Int fa1/3
ip address 192.168.35.64 255.255.255.240
exit

do write
copy running-config startup-config
```

## Configuracion del etherswitch hacia router
## ES"
```sh
conf t

int fa 1/0
ip address 192.168.35.1 255.255.255.240
exit

do write
copy running-config startup-config
```

## Configuracion del router hacia etherswitch
## R6
```sh
conf t

int fa 0/0
ip address 192.168.35.0
exit

do write
copy running-config startup-config
```







