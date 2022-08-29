# Proyecto 1
## Integrantes Grupo 3

| Nombre | Carnet |
| ------ | ------ |
| Carlos Antonio Velasquez Castellanos | 201403654 |
| Oscar Augusto Perez Tzunun | 201213498 |
| Daniel Enrique Santos Godoy | 201325512 |


## Topologia 1

![image](https://user-images.githubusercontent.com/57165427/186696460-95f25e4f-7ad8-4bfd-9299-3cce5bd3edc8.png)

##

| Paso  | Descripcion | Comando / Imagen | 
| ------ | ------ | ------ | 
| 1 | Creacion de la maquina virtual de recursos humanos cliente, se conecto con el adaptador de red virtual para ser utilizado posteriormente con gns3. | ![image](https://user-images.githubusercontent.com/57165427/186697536-e4c97cbe-14aa-4852-b659-328e352d207e.png) | 
| 2 | Creacion de la maquina virtual de contabilidad cliente, se conecto con el adaptador de red virtual para ser utilizado posteriormente con gns3.  | ![image](https://user-images.githubusercontent.com/57165427/186698609-56eb95aa-7ed0-4118-a818-422fd05694ec.png) | 
| 3 | Instalacion de ubuntu en las maquinas virtuales.  | ![image](https://user-images.githubusercontent.com/57165427/186699578-3c6b68e5-d987-457a-b4ab-d28e3561be3d.png) | 
| 4 | Actualizamos paquetes en ubuntu  | ![image](https://user-images.githubusercontent.com/57165427/186700181-cc913da4-20c2-4991-b001-9081f3f01efc.png) | 
| 5 | Instalamos net stat para utilizar ifconfig  | ![image](https://user-images.githubusercontent.com/57165427/186700547-00c8ccd1-b24d-4d2e-b3f9-d1bc100642d5.png) |
| 6 | Agregar las maquina virtuales a GNS3  | ![image](https://user-images.githubusercontent.com/57165427/186701026-63893f30-ae66-4fac-9f96-3de4d8ae4d31.png) |

##
## Configuracion del modo truncal

## ESW1
```sh
conf t

int fa 1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int fa 1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int fa 1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

do write
copy running-config startup-config
```

## ESW2
```sh
conf t

int fa 1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int fa 1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

do write
copy running-config startup-config
```
## ESW3
```sh
conf t

int fa 1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int fa 1/1
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
Int fa1/3
Switchport mode Access
Switchport Access vlan 10
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
Switchport Access vlan 10
Do wri
End
copy running-config startup-config
```

## ESW3
```sh
Conf t
Int fa1/3
Switchport mode Access
Switchport Access vlan 30
Do wri
End

Conf t
Int fa1/4
Switchport mode Access
Switchport Access vlan 40
Do wri
End

Conf t
Int fa1/5
Switchport mode Access
Switchport Access vlan 20
Do wri
End
copy running-config startup-config
```


## Configuracion de los Etherswitch VTP


## ESW1
```sh
Conf t
Vtp domain Grupo3
Vtp password Grupo3
Vtp mode client
Do wri
End
copy running-config startup-config
```

## ESW2
```sh
Conf t
Vtp domain Grupo3
Vtp password Grupo3
Vtp mode client
Do wri
End
copy running-config startup-config
```

## ESW3
```sh
Conf t
Vtp domain Grupo3
Vtp password Grupo3
Vtp mode transparent
Do wri
End
copy running-config startup-config
```



## Topologia 2

![image](https://user-images.githubusercontent.com/57165427/186696614-6773316a-4ceb-4f5f-a03d-9a0a372d6d65.png)
##

## Configuracion de los etherswitch
##
## ESW4
```sh
conf t

vtp domain GRUPO3
vtp domain password GRUPO3
vtp mode server

end
```

## ESW6
```sh
conf t

vtp domain GRUPO3
vtp domain password GRUPO3
vtp mode client 

end
```

## ESW5
```sh
conf t

vtp domain GRUPO3
vtp domain password GRUPO3
vtp mode client 

end
```

## ESW7
```sh
conf t

vtp domain GRUPO3
vtp domain password GRUPO3
vtp mode client 

end
```


## Configuracion de las VLAN
##
## ESW4
```sh
conf t 
vlan 10
name RRHH
exit

vlan 20
name Informatica
exit

vlan 30
name Contabilidad
exit

vlan 40
name Ventas
exit

end
```



## Configuracion de los modos TRONCALES
##
## ESW4
```sh
conf t

int Po1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int Po2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int fa1/15
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

end
```

## ESW6
```sh
conf t

int Po1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int Po3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int Po4 
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

end
```

## ESW5
```sh
conf t

int Po4
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int Po5
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

end
```

## ESW7
```sh
conf t

int Po2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int Po3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

int Po5 
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1006
exit

end
```


## Configuracion de la STP
##
## ESW4
```sh
conf t
spanning-tree vlan 10 root primary 
spanning-tree vlan 20 root primary 
spanning-tree vlan 30 root primary 
spanning-tree vlan 40 root primary 
end
```

## Guardar la configuracion SAVE
##
```sh
copy running-config startup-config
```




## Topologia 3

![image](https://user-images.githubusercontent.com/57165427/186696728-b6d82bbc-a0b7-4e11-b065-1b20d9f43feb.png)

##
| Paso  | Descripcion | Comando / Imagen | 
| ------ | ------ | ------ | 
| 1 | Creacion de la maquina virtual de recursos humanos, se conecto con el adaptador de red virtual para ser utilizado posteriormente con gns3. | ![image](https://user-images.githubusercontent.com/57165427/186697536-e4c97cbe-14aa-4852-b659-328e352d207e.png) | 
| 2 | Creacion de la maquina virtual de contabilidad, se conecto con el adaptador de red virtual para ser utilizado posteriormente con gns3.  | ![image](https://user-images.githubusercontent.com/57165427/186698609-56eb95aa-7ed0-4118-a818-422fd05694ec.png) | 
| 3 | Instalacion de ubuntu en las maquinas virtuales.  | ![image](https://user-images.githubusercontent.com/57165427/186699578-3c6b68e5-d987-457a-b4ab-d28e3561be3d.png) | 
| 4 | Actualizamos paquetes en ubuntu  | ![image](https://user-images.githubusercontent.com/57165427/186700181-cc913da4-20c2-4991-b001-9081f3f01efc.png) | 
| 5 | Instalamos net stat para utilizar ifconfig  | ![image](https://user-images.githubusercontent.com/57165427/186700547-00c8ccd1-b24d-4d2e-b3f9-d1bc100642d5.png) |
| 6 | Agregar las maquina virtuales a GNS3  | ![image](https://user-images.githubusercontent.com/57165427/186701026-63893f30-ae66-4fac-9f96-3de4d8ae4d31.png) |
| 7 | Agregar las maquina virtuales a la topologia  | ![image](https://user-images.githubusercontent.com/57165427/186701188-42cc8234-f19a-406d-854a-511a4af049c3.png) |


## 
## Configuracion de los Etherswitch
##
## ESW8
```sh
conf t 
Int f1/0
Switchport mode trunk
Switchport trunk allowed vlan 1,1002-1005
Do wri
End
copy running-config startup-config

```
##
## ESW9
```sh
conf t 
Int f1/0
Switchport mode trunk
Switchport trunk allowed vlan 1,1002-1005
Do wri
End

conf t 
Int f1/2
Switchport mode trunk
Switchport trunk allowed vlan 1,1002-1005
Do wri
End

conf t 
Int f1/1
Switchport mode trunk
Switchport trunk allowed vlan 1,1002-1005
Do wri
End
copy running-config startup-config
```

##
## ESW10
```sh
conf t 
Int f1/1
Switchport mode trunk
Switchport trunk allowed vlan 1,1002-1005
Do wri
End

conf t 
Int f1/3
Switchport mode trunk
Switchport trunk allowed vlan 1,1002-1005
Do wri
End
copy running-config startup-config
```

##
## ESW11
```sh
conf t 
Int f1/2
Switchport mode trunk
Switchport trunk allowed vlan 1,1002-1005
Do wri
End

conf t 
Int f1/3
Switchport mode trunk
Switchport trunk allowed vlan 1,1002-1005
Do wri
End
copy running-config startup-config

```
## Configuracion de los Etherswitch VTP

## ESW8
```sh
Conf t
Vtp domain Grupo3
Vtp password Grupo3
Vtp mode client
Do wri
End
copy running-config startup-config
```

## ESW9
```sh
Conf t
Vtp domain Grupo3
Vtp password Grupo3
Vtp mode client
Do wri
End
copy running-config startup-config
```

## ESW10
```sh
Conf t
Vtp domain Grupo3
Vtp password Grupo3
Vtp mode client
Do wri
End
copy running-config startup-config
```

## ESW11
```sh
Conf t
Vtp domain Grupo3
Vtp password Grupo3
Vtp mode transparent
Do wri
End
copy running-config startup-config
```

