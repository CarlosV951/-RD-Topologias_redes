## Integrantes Grupo 3

| Nombre | Carnet |
| ------ | ------ |
| Carlos Antonio Velasquez Castellanos | 201403654 |
| Oscar Augusto Perez Tzunun | 201213498 |
| Daniel Enrique Santos Godoy | 201325512 |

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
```

