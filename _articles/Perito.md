---
id: 3
title: "Peritaje Forense"
subtitle: "Instalacion de Docker con postgresSQL y Adminer"
date: "2021.11.16"
tags: "AFI, Analisis Forense Informatico, Unidad 1, Tarea2"
---


# Enunciado del ejercicio

Extraer, documentar y firmar mediante los tipos de funciones hash md5 y sha256, una posible **evidencia digital** relativa a los mensajes de diagnostico del kernel, dentro de un **peritaje forense básico** sobre un escenario de un SO Linux Debian 10.

# Desarrollo del ejercicio

## Instalacion de RaspberryPi

Vamos a instalar una imagen de RaspberryPi como maquina para peritar, vamos a usar esta maquina virtual debido a que tiene muy pocos requerimientos minimos sobre el sistema anfitrion.

El proceso de instalacion de esta maquina es muy sencillo, lo unico que necesitamos es descargarnos [**esta imagen**](https://downloads.raspberrypi.org/rpd_x86/images/rpd_x86-2021-01-12/2021-01-11-raspios-buster-i386.iso) [^1] para montarla en nuestra maquina virtual e instalar esta maquina, tambien hemos decidido actualizar todos sus componentes a la ultima version.

Una vez instalada y actualizada, como ultimo paso, tendremos que crear un DISCO DURO de 1GB e introducirselo como si de un disco duro adicional se tratara en la maquina.

Deberia de quedar de la siguiente manera:

![imgur](https://i.imgur.com/YRGDtjv.png)[^2]

## Configuracion del nuevo Disco Duro

Ahora lo que vamos a hacer es formatear ese disco duro para que tenga un formato.

Iniciamos la maquina con el disco duro nuevo y comprobamos que se ha conectado correctamente.

```rush
sudo fdisk -l
```

![imgur](https://i.imgur.com/tyZwZLI.png)

![imgur](https://i.imgur.com/uAKFdz9.png)

![imgur](https://i.imgur.com/DlR5Hay.png)

Para aplicar el Sistema de archivos al disco duro tenemos que ejecutar la siguiente orden:

```rush
sudo mkfs.vfat -F 32 /dev/sdb1
```

Con esto, ya tendriamos la tabla de particiones asignada en la unidad nueva.

## Montar la carpeta en el Disco duro

Para continuar vamos a montar una carpeta en el disco duro para trabajar con ella, vamos a la carpeta /tmp y en esta carpeta vamos a crear evidencias.

```rust
cd /tmp
mkdir evidencias
cd evidencias
sudo mount /dev/sdb1 evidencias/
```
## Montar el supuesto

Dentro de la carpeta de evidencias, vamos a crear una carpeta llamada escenarioLinux, y vamos a introducir un archivo dmesg en el como salida.

![imgur](https://i.imgur.com/VNiEaQq.png)

## Cifrado del archivo

Una vez extraido los datos, vamos a cifrar el documento con un **HASH MD5** y con un **HASH SHA256**

```rush
md5sum tarea2AFI.dmesg.txt >> tarea2AFI.dmesg.txt
sha256 tarea2AFI.dmesg.txt >> tarea2AFI.dmesg.txt
```
![imgur](https://i.imgur.com/0fOj30I.png)

Con esto ya habriamos extraido el archivo de carga del sistema y los hemos guardado con una clave MD5 y SHA256.


# Despedida

Gracias a este ejercicio, hemos aprendido a extraer los datos del sistema guardados en volatil y ademas hemos dejado la firma en 2 formatos.

Espero que os halla servido, un placer y hasta la proxima.


[^1]: Imagen de descarga de Raspberry.
[^2]: Estado de la maquina RaspberryPi.

