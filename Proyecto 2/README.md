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







