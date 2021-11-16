---
id: 2
title: "Instalacion de Docker"
subtitle: "Instalacion de Docker con postgresSQL y Adminer"
date: "2021.11.10"
tags: "Puesta en produccion segura, Docker, Unidad 1, PPS"
---


# Enunciado del ejercicio

Instalación y uso de **Docker** para desplegar una BD Relacional mediante el SGBD PostgreSQL usando contenedores.

# Desarrollo del ejercicio

## Instalacion de Docker

Para la instalación de docker en el equipo, lo que vamos a realizar es ejecutar un **script en bash** que te va a ejecutar todas las instrucciones necesarias para su puesta en funcionamiento. El script seria el siguiente:

```rust
# Install dependencies.
  sudo apt install -y curl apt-transport-https \
       software-properties-common ca-certificates
  # Install docker.
  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
  echo "deb [arch=amd64] https://download.docker.com/linux/debian stretch stable  " | \
    sudo tee /etc/apt/sources.list.d/docker-engine.list
  
  sudo apt-get update -y
  sudo apt-get install -y docker-ce
  
  # Run docker.
  sudo systemctl start docker
  sudo systemctl enable docker
  
  # Add user to docker group for using docker without sudo command.
  sudo gpasswd -a "${USER}" docker
  
  # Reboot
  sudo reboot
```
[^1]

Una vez ejecutado este script **(es para debian)** ya tendriamos el docker instalado en nuestro equipo.

Comprobamos con la siguiente orden que nuestro Docker esta instalado correctamente en el equipo.

```rust
docker --version
```
Y nos tiene que dar algo asi:

![imgur](https://i.imgur.com/htffIVO.png)[^2]

### Instalacion de PostgresSQL y de Adminer

Ahora realizaremos una instalación, tanto de postgres como de adminer. Para ello lo que vamos a realizar son los siguientes comandos.

```rust
docker pull postgres

docker pull adminer
```
La salida de estos comandos por pantallan seran algo parecida a esta:

![imgur](https://i.imgur.com/ovdtPuS.png)

![imgur](https://i.imgur.com/60HIAKr.png)[^3]

Con esto, ya tendriamos instalados ambos contenedores en nuestro equipo.

#### Montar servicios de Docker

Una vez tenemos los contenedores instalados en nuestro equipo, vamos a arrancar estos servicios para poder trabajar con ellos.

Para arrancar estos servicios tenemos que usar las siguientes ordenes:

```rust
# Arrancar postgres
    docker run --name contpost -e POSTGRES_USER=juan -e POSTGRES_PASSWORD=123 
    -e POSTGRES_DB=postgres -p 5432:5432 -d postgres
    
# Explicacion del comando 
    docker run --name (NOMBRE DEL CONTENEDOR QUE LE QUEREMOS ASIGNAR)
    -e POSTGRES_USER=(NOMBRE DEL USUARIO QUE VA A TENER PERMISOS)
    -e POSTGRES_PASSWORD=(CONTRASEÑA DEL USUARIO)
    -e POSTGRES_DB=(BASE DE DATOS QUE SE ASIGNARA)
    -p (PUERTO QUE SE LE ASIGNARA)
    -d (CONTENEDOR A MONTAR)
    
# Arrancar Adminer
    docker run --name contadm -d --link contpost -p 81:8080 adminer

# Explicacion del comando
    docker run --name (NOMBRE DEL CONTADOR)
    --link (CONTENEDOR VINCULADO)
    -p (PUERTO ASIGNADO)
    -d (CONTENEDOR A MONTAR)
```
[^4]

Esto no deberia de devolver una salida tal que como esta:




## Ejecucion de Postgres y Adminer

Una vez hemos montado los servicios de Postgres y Adminer, vamos a ver si funcionan correctamente, para ello si nos vamos a localhost:81, deberiamos de ver nuestro gestor Adminer y podremos acceder a la base de datos de Postgres.

![imgur](https://i.imgur.com/kyzeRft.png)

En la ventana, tendremos que rellenar los datos con nuestros datos que registramos en el comando de Montar el Postgres

![imgur](https://i.imgur.com/sLvjOuN.png)


Una vez dentro realizado esto, ya podemos introducir datos en nuestra base de datos.

### Introduccion de datos en postgres

Ahora lo que vamos a realizar es la introduccion de datos a traves de Adminer en nuestra base de datos, simplemente con la introduccion de datos en SQL de dentro de nuestra aplicacion ya tendriamos los datos en nuestra base de datos.

```rust
DROP TABLE IF EXISTS "usuarios";
DROP SEQUENCE IF EXISTS usuarios_id_seq;
CREATE SEQUENCE usuarios_id_seq INCREMENT 1 MINVALUE 1 MAXVALUE
2147483647 CACHE 1;
CREATE TABLE "public"."usuarios" (
"id" integer DEFAULT nextval('usuarios_id_seq') NOT NULL,
"nombre" character varying NOT NULL,
"contrasena" character varying NOT NULL,
"desc" character varying NOT NULL,
CONSTRAINT "usuarios_pkey" PRIMARY KEY ("id")
) WITH (oids = false);

```

```rust
INSERT INTO "usuarios" ("id", "nombre", "contrasena", "desc")
VALUES
(1, 'admin', 'passadmin', 'Administrador'),
(2, 'usuario1', 'password1', 'Primer usuario'),
(3, 'usuario2', 'password2', 'Segundo Usuario'),
(4, 'leet', 'P@55w0rd', 'El Amigo Friky');
```



# Despedida

Gracias a este ejercicio, hemos aprendido a instalar docker en nuestro equipo, a instalar paquetes con docker y a lanzar esos paquetes de docker y correrlos en nuestro equipo, en un futuro usaremos la base de datos que hemos generado con los datos que ya tenemos.

Espero que os halla servido, un placer y hasta la proxima.


[^1]: Script en bash de instalacion de Docker.
[^2]: Comprobacion de la instalacion de Docker.
[^3]: Instalacion de postgres y Adminer.
[^4]: Montar contenedores en Docker.

