## Integrantes Grupo 3

| Nombre | Carnet |
| ------ | ------ |
| Carlos Antonio Velasquez Castellanos | 201403654 |


## Configuracion de las VPC Tabla
| Numero de VPC | IP |  Mascara de subred | Puerta de enlace |
| ------ | ------ | ------ | ------ |
| VPC 1  | 192.168.71.2 | 255.255.255.0 | 192.168.71.1 |
| VPC 2  | 192.168.71.3 | 255.255.255.0 | 192.168.71.1 |
| VPC 3  | 192.168.72.2 | 255.255.255.0 | 192.168.72.1 |
| VPC 4  | 192.168.72.3 | 255.255.255.0 | 192.168.72.1 |
| VPC 5  | 192.168.73.2 | 255.255.255.0 | 192.168.73.1 |
| VPC 6  | 192.168.73.3 | 255.255.255.0 | 192.168.73.1 |

## Comandos VPC
```sh
VPC #1
ip 192.168.71.2 255.255.255.0 192.168.71.1

VPC #2
ip 192.168.71.3 255.255.255.0 192.168.71.1

VPC #3
ip 192.168.72.2 255.255.255.0 192.168.72.1

VPC #4
ip 192.168.72.3 255.255.255.0 192.168.72.1

VPC #5
ip 192.168.73.2 255.255.255.0 192.168.73.1

VPC #6
ip 192.168.73.3 255.255.255.0 192.168.73.1

```

## Comandos Router #1
```sh
conf t
interface serial 2/0
ip address 172.71.0.2 255.255.0.0
no shutdown
exit

interface serial 2/1
ip address 172.72.0.1 255.255.0.0
no shutdown

interface fa 0/0
ip address 192.168.73.1 255.255.255.0
no shutdown
copy run start

RUTEO DE INTERFACES SERIAL y FAST INTERNET
conf t
ip route 172.73.0.0 255.255.0.0 172.71.0.2
ip route 192.168.72.0 255.255.255.0 172.72.0.2
ip route 192.168.71.0 255.255.255.0 172.71.0.2
do write
copy run start
```

## Comandos Router #2
```sh
conf t
interface serial 2/0
ip address 172.71.0.1 255.255.0.0
no shutdown
exit

interface serial 2/2
ip address 172.73.0.1 255.255.0.0
no shutdown
copy run start

interface fa 0/0
ip address 192.168.71.1 255.255.255.0
no shutdown
copy run start

RUTEO DE INTERFACES SERIAL y FAST INTERNET
conf t
ip route 172.72.0.0 255.255.0.0 172.71.0.1
ip route 192.168.72.0 255.255.0.0 172.73.0.2
ip route 192.168.73.0 255.255.255.0 172.71.0.1
do write
copy run start
```

## Comandos Router #3
```sh
conf t
interface serial 2/1
ip address 172.72.0.2 255.255.0.0
no shutdown
exit

interface serial 2/2
ip address 172.73.0.2 255.255.0.0
no shutdown
copy run start

interface fa 0/0
ip address 192.168.72.1 255.255.255.0
no shutdown
copy run start

RUTEO DE INTERFACES SERIAL y FAST INTERNET
conf t
ip route 172.71.0.0 255.255.0.0 172.73.0.1
ip route 192.168.73.0 255.255.255.0 172.72.0.1
ip route 192.168.71.0 255.255.255.0 172.73.0.1
do write
copy run start
```

## Prueba de pings hacia las otras VPCS

## VPC Local Router 2 (192.168.71.1)

![image](https://user-images.githubusercontent.com/57165427/193470024-75e80eca-a234-45ae-9376-08afd72de44a.png)

## VPC Router 3 (192.168.72.1)

![image](https://user-images.githubusercontent.com/57165427/193470083-42d88582-fe64-4847-99af-2be6763c6793.png)

## VPC Router 1 (192.168.73.1)

![image](https://user-images.githubusercontent.com/57165427/193470133-1ab9b08b-0df0-4031-a3b4-6b796c9def3b.png)

