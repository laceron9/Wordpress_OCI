# Bienvenidos a Oracle Racing To The Cloud
## Laboratorio de Container Instances 
## Despliegue de Wordpress
#### El laboratorio consiste en el despliegue de Wordpress en una subred privada utilizando una Base de Datos MySQL creada como otro container dentro de la misma instancia. La seguridad lo mas importante !!! 

#### Para acceder a nuestro sistema Wordpress vamos a crear un Load Balancer publico protegido por un WAF (Web Appplication Firewall) como proteccion a posibles ciberataques

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/OCI_Container_instances.png)

#### Prerrequisitos para la realizacion del Laboratorio
* Creacion de VCN y subredes, una publica y una privada
* Creacion de Internet Gateway y entrada en la tabla de rutas para la subred publica
* Creacion de NAT Gateway y entrada en la tabla de rutas para la subred privada
+ Configuracion de Security Lists:
  + Para la subred publica permitir el trafico por los puertos 80 y 3306
  + Para la subred privada permitir todo el trafico desde la subred publica
  
# 1. Creación de Container Instance

### Menu principal >Developer Services > Container instances

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_container_instance.jpg)

## Configuración de la instancia
Debemos ingresar la informacion del nombre de la instancia, AD, Shape y capacidades de computo(OCPU y Memoria RAM)

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_container_instance1.jpg)

En la parte de Networking seleccionamos la VCN y la subred privada, luego desplegamos Advance Options e ingresamos una IP correspondiente al bloque de IPs de la subred privada
![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_container_instance2.jpg)

### Configuración de los contenedores
En esta parte vamos a asignar los nombres de los contenedores, para ello seleccionamos las imagenes a utilizar y creamos las variables de ambiente que necesita el contenedor para funcionar adecuadamente. Para el laboratorio vamos a utilizar las imagenes publicas del Docker Hub

### El primer container a crear es el de MySQL
Asignamos un nombre al container y seleccionamos la imagen a descargar desde el Docker Hub

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_container_2.jpg)

Configuracion de las variables de ambiente necesarias para el despliegue del container MySQL
Click en crear another container

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_container_4.jpg)

### El segundo container a crear es el de Wordpress
Asignamos un nombre al container y seleccionamos la imagen a descargar desde el Docker Hub

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_container_5.jpg)

Configuracion de las variables de ambiente necesarias para el despliegue del container Wordpress
El valor de la variable WORDPRESS_DB_HOST corresponde a la IP seleccionada durante la creacion del Container Instance en la parte de Networking

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_container_6.jpg)

Click en Create

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_container_7.jpg)

# 2. Creación del Load Balancer

#### Para acceder de forma publica al servicio de Wordpress es necesario configurar un Load Balancer para recibir el trafico desde internet

### Menu principal > Networking > Load Balancers

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_lb_1.jpg)

Asignamos el nombre del LB y seleccionamos las opciones de visibilidad publica e IP

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_lb_2.jpg)

Seleccionamos la VCN y la subred publica ceeada durante los prerrequisitos

![](https://github.com/johncdoracle/RacingToCloud/blob/main/images/create_lb_3.jpg)





