---
id: 0
title: "Captura la bandera 1"
subtitle: "Introduccion a los captura la bandera"
date: "2021.11.10"
tags: "Hacking Etico, CTF, Unidad 1"
---

Como introduccion al Hacking Etico, lo primero que vamos a realizar es un ejercicio de **Captura la Bandera**, esto lo vamos a realizar de la siguiente manera:

# Explicacion del ejercicio
En Hacking Ético son muy comunes los retos llamados **CTF** (**C**apture **T**he **F**lag) o capturar la bandera. Normalmente consiste en una máquina que prepara alguien, para que la comunidad trate de hackearla. Intentaremos hacer muchas, sobre todo en la recta final de curso, para consolidar todo lo aprendido.
Básicamente, tienes que acceder a la máquina, y encontrar lo que se llama **flag** o **bandera**. Es un fichero de texto con una palabra (normalmente un galimatías, un uuid, ...), que pruebe que has accedido con éxito.
Vamos a hacer una pequeña serie de retos CTF no muy complicados, para que más o menos puedas hacerte una idea de cómo son.

## Desarrollo del ejercicio

Para empezar, nos descargaremos [**este enlace**](https://mega.nz/file/eV4TwCyB#ZrLjdqlcpnGw9h3yd50hqvEv_2u3qtf2HjRuGrSb0-k) [^1]de Mega para tener los archivos.(No he podido subirlos a GitHub).
Empezando por el reto01, `descomprimimos el archivo y nos dara 2 archivos`, un libro y la explicacion de lo que tenemos que ir realizando para encontrar la clave del siguiente archivo, si no encontramos la clave del reto anterior, no podemos seguir avanzando en el ejercicio. Asi iremos completando todos los retos poco a poco.

# Reto 1: El Quijote

## Enunciado del problema

Desde la creación del instituto, algunos alumnos se han encargado de la gestión del periodido local, `"El noticiero"`, donde se intercambian mensajes y escriben artículos didácticos. En uno de los artículos alguien anónim@ ha lanzado un reto. Asegura haber escondido un mensaje en el libro más universal de la literatura castellana. En su mensaje advierte que para empezar, nos proporciona algunas coordenadas para que las mentes mas brillantes del instituto puedan resolverlo. 

|`Libro: "El quijote de la mancha" `|
|-----------------------------------|
|10:8:2|
|23:11:1|
|30:8:2|
|30:26:7|
|35:1:7|
|151:19:10|
|151:11:8|
|152:11:5|

### Resolucion reto 1


> Al observar el resultado que nos dan, podemos comprobar que parece como que nos facilitan unas coordenadas, probamos a ver si las coordenadas se corresponde con lo siguiente:

`Pagina del libro` : `Numero de la linea` : `Palabra en la linea`

Con lo cual si nos fueramos a la linea numero 10, fila numero 8, segunda palabrar obtendriamos la palabra **querer**.
Esto lo tendremos que realizar con cada una de las lineas para obtener el siguiente resultado:
|`Coordenada` --> **Clave**|
|--------------------------|
|`10:8:2` = **querer**|
|`23:11:1` = **saber**|
|`30:8:2` = **noticia**|
|`30:26:7` = **sobre**|
|`35:1:7` = **conocer**|
|`151:19:10` =**misterio**|
|`151:11:8` = **quien**|
|`152:11:5` = **hizo**|


Una vez ya hemos encontrado las palabras solo queda estructurarlas entre unos `corchetes` comenzando con `flag` y los espacios cambiarlos por `_`

```rust
flag{querer_saber_noticia_sobre_conocer_misterio_quien_hizo}
```

# Reto 2: Julio Cesar

## Descripcion del problema 2
>**Después de muchos años recopilando documentación**, fotos y artículos, se ha decidido realizar una limpieza y llevar la documentación antigua a una nueva sala que le ha cedido el instituto. 
En esta sala se pueden archivar de una forma sencilla por fecha todos los documentos del periodico.

Durante este proceso moviendo documentos, una hoja extraña se cae entre los documentos que lleváis. Contiene un texto ilegible junto a la **referencia del emperador Julio César**. ¿Podrás sacar en claro que quería decir la nota?

```rust
Yn fvthvragr vasbeznpvba rf pbasvqrapvny. Gr nlhqnen n cebfrthve ra yn 
vairfgvtnpvba. Ab gr pbasvrf, ab gbqnf ynf vasbeznpvbarf qr ynf dhr qvfcbarzbf
fba gna snpvyrf pbzb rfgn ebgnpvba qr pnenpgrerf. Sveznqb: ha nzvtb.  
synt{rfgnzbf_rzcrmnaqb_n_pbabpre_nytb_qr_uvfgbevn}
```

### Resolucion ejercicio 2

>Despues de ver el mensaje y saber que es del mismisimo Cesar, todo el mundo sabe que Cesar invento un sistema de cifrado que se encargaba de cambiar su colocacion en el abecedario de tal manera que una **"A"** en un mensaje cifrado con este sistema con una clave **1**, en el mensaje apareceria como una **"B"**.

 [**Aqui**](http://nosolomates.es/?page_id=760) [^2]Probando un poquito con un alternador, hemos descubierto que la clave de este mensaje es **13**, osea que tendriamos que mover la letra **13 veces**.

```rust
la siguiente informacion es confidencial. te ayudara a proseguir en la 
investigacion. no te confies,no todas las informaciones de las que 
disponemos son tan faciles como esta rotacion de caracteres.
firmado: un amigo.  

flag{estamos_empezando_a_conocer_algo_de_historia}

N=13
```

# Reto 3: El Codificador

## Enunciado del ejercicio 3

>Al darle la vuelta a la hoja, veis que tambien tiene otro texto escrito en esa parte, aunque tampoco lo entendéis. 

Se adjunta también un fichero con extensión **pyc**. ¿Nos servirá de ayuda?

¿Podrás proporionarnos la otra información que está en la otra cara de la hoja?
Datos proporcionados (generado con xor.pyc): 

```rust
**Ax8VCB4HEAAGDDMEBRERPhENAh8DLQQcEQERMAgaBjERAhwEGgADHA==**
```

### Resolucion del ejercicio 3

Lo primero que podemos observar es que nos han facilitado un archivo pyc.
Este archivo es un archivo python compilado, asi que vamos a buscar un
descompilador online de este tipo de archivos[**descompilador pyc**](https://www.toolnb.com/tools-lang-en/pyc.html) [^3]. Una vez descompilado este archivo
obtenemos esto:

```rust
# uncompyle6 version 3.5.0
# Python bytecode 2.7 (62211)
# Decompiled from: Python 2.7.5 (default, Nov 16 2020, 22:23:17) 
# [GCC 4.8.5 20150623 (Red Hat 4.8.5-44)]
# Embedded file name: xor.py
# Compiled at: 2021-02-01 23:35:44
import binascii, itertools, base64, sys

def xor_crypt_string(data, key='estoesunaclaveparacifrar', encode=False, decode=False):
    from itertools import izip, cycle
    import base64
    if decode:
        data = base64.decodestring(data)
    xored = ('').join(chr(ord(x) ^ ord(y)) for x, y in izip(data, cycle(key)))
    if encode:
        return base64.encodestring(xored).strip()
    return xored


secret_data = sys.argv[1]
print 'Cifrado'
print xor_crypt_string(secret_data, encode=True)
print 'Descifrado'
print xor_crypt_string(xor_crypt_string(secret_data, encode=True), decode=True)
```

Podemos observar que este archivo python 2.7 lo que nos esta haciendo es una funcion de encriptacion y una funcion de desencriptacion.
Parece que la clave que nos han facilitado esta cifrada con un algoritmo xor. Si modificamos este codigo y lo dejamos de la siguiente manera podemos obtener la clave descifrada.

```rust
def xor_crypt_string(data, key='estoesunaclaveparacifrar', encode=False, decode=False):
    from itertools import izip, cycle
    import base64
    if decode:
        data = base64.decodestring(data)
    xored = ('').join(chr(ord(x) ^ ord(y)) for x, y in izip(data, cycle(key)))
    if encode:
        return base64.encodestring(xored).strip()
    return xored

secret_data = **Ax8VCB4HEAAGDDMEBRERPhENAh8DLQQcEQERMAgaBjERAhwEGgADHA==**
print xor_crypt_string(xor_crypt_string(secret_data, encode=True), decode=True)
```
Con este pequeño fragmento de codigo podriamos obtener la clave.

```rust
flag{tengo_esta_clave_entre_mis_papeles}
```
# Reto 4: Mensaje Enigmatico

## Enunciado del ejercicio 4

>Con la información que habeis obtenido, intentais utilizar las credenciales para poder acceder al ordenador del periodico y al entrar os descargais un archivo. 

El fichero original ha cifrado alguna información secreta que debes obtener para que la investigación no se atasque. 
Esto es lo que sabemos que ha devuelto la salida del fichero que has obtenido al entrar en la web del periódico. 

**Hemos recibido este mensaje junto a unas instrucciones para su manejo. Parece un completo enigma.**

```rust
59556843656d517a545764684d3035355a4735425a317074526e526a626d646e57544a61633249794e476461534842785a55644e5a316b7a566a42615630316e596c684f4d5751795a32646156315a6f5a4668765a325674536e4e684d6e4e6e576d3543626d4e595157645a57454a74576a4a6e5a32517962486c684d30316e596c6857613246755a32645a5748426f597a4e725a316c59516d356957456c6e59556477626c6c745557646c57484278595663775a324e496144466b6257396e5a56646f64574a745a326469563342785930646a5a32466e5054303d
```

|`Modelo: M3 Reflector: ????" `|
|-----------------------------------|
|ROT1.: 1   -->   POS1.: A   -->   ANILLO1.: A|
|ROT2.: 2   -->   POS1.: B   -->   ANILLO1.: B|
|ROT3.: 3   -->   POS1.: C   -->   ANILLO1.: C|

PLUGBOARD: bq cr di ej kw mt os px uz gh

### Resolucion del ejercicio 4

El mensaje parece que esta cifrado de alguna manera, y mirando el codigo parece que esta en hexadecimal, pues no hay ninguna letra mas halla de la F. Primero vamos a pasar este mensaje.

Utilizando [**esta utilidad**](https://gchq.github.io/CyberChef/) [^4]ciberchef, hemos podido pasar de un sistema a otro.

```rust
YUhCemQzTWdhM055ZG5BZ1ptRnRjbmdnWTJac2IyNGdaSHBxZUdNZ1kzVjBaV01nYlhOMWQyZ2daV1ZoZFhvZ2VtSnNhMnNnWm5CbmNYQWdZWEJtWjJnZ2QybHlhM01nYlhWa2FuZ2dZWHBoYzNrZ1lYQm5iWElnYUdwblltUWdlWHBxYVcwZ2NIaDFkbW9nZVdodWJtZ2diV3BxY0djZ2FnPT0=
```
Este segundo mensaje tiene pinta de que ahora esta cifrado en Base64 asi que vamos a descifrarlo tambien.

```rust
aHBzd3Mga3NydnAgZmFtcnggY2Zsb24gZHpqeGMgY3V0ZWMgbXN1d2ggZWVhdXogemJsa2sgZnBncXAgYXBmZ2ggd2lya3MgbXVkanggYXphc3kgYXBnbXIgaGpnYmQgeXpqaW0gcHh1dmogeWhubmggbWpqcGcgag==
```
Y este parece que tambien esta cifrado en Base64, si nos equivocamos, pensaremos otra cosa.

```rust
hpsws ksrvp famrx cflon dzjxc cutec msuwh eeauz zblkk fpgqp apfgh wirks mudjx azasy apgmr hjgbd yzjim pxuvj yhnnh mjjpg j
```
Ahora parece que tenemos algo que si encaja con una descripcion de enigma. Vamos a irnos a un descifrador de enigma y pasemosle los parametros que nos ha facilitado el enunciado.

```rust
ponga atenc ionsi fraca samos enest amisi onnos verem osabo cados aperd erlot odoan otees taban derae nigma mtres ukwbv i
```
Con esto ya tenemos un mensaje legible, solo nos queda obviar los espacios y nos queda este mensaje tan bonito:

>Ponga atencion si fracasamos en esta mision nos veremos abocados a perderlo todo anote esta bandera enigmamtresukwbvi

Con esto, podemos decir que la clave es:
```rust
flag{enigmamtresukwbvi}
```

# Reto 5: Archivo Wireshark

## Enunciado del ejercicio 5
>Hablais con el director del instituto y os permite acceder al contenido del disco. Al entrar encontrais un pcap. ! Qué es un pcap ! os preguntáis. No lo sabemos pero habrá que investigar. 

Los datos os suenan codificados en hexadecimal pero ... ¿Cómo recomponer estas piezas de cada petición? Además,hay mucho ruido de navegación en el fichero.  

`Se proporciona un archivo wireshark para verlo`

### Resolucion del ejercicio 5

>En este ejercicio se nos pide que descubramos la ultima bandera. Para hacer esto abrimos el archivo facilitado con WireShark.
Este archivo contiene muchisimas tramas de red. Nos paramos a ver las todas las tramas y al final del documento me fijo en algo muy extraño, ¿Que es localghost? y ¿que es esa trama hexadecimal que tiene delante?

Vamos copiando poco a poco y metiendo en el descriptor poco a poco todas las tramas.

```rust
45737465206669636865726f206573206d757920696d706f7274616e7465
2e20446573747275697220756e612076657a206c6569646f2e204e6f2074
69656e652073656e7469646f20717565206f74726f73206f6a6f73207175
65206e6f207365616e206c6f73207475796f73206c6f207665616e2e200a
4c65616e202c207665616e20c2bf517565206d61732064613f0a0a666c61

677b646e735f7370795f657866696c74726174696f6e7d200a0a
```
Estas serian todas las tramas separadas con lo que una vez traducidas, el mensaje quedaria tal que asi:

```rust
Este fichero es muy importante. Destruir una vez leido.
No tiene sentido que otros ojos que no sean los tuyos lo vean. 
Lean , vean ¿Que mas da?

flag{dns_spy_exfiltration}
```

# Despedida

Con esto terminamos los 5 retos de CTF que queriamos hacer hoy, algunos han sido bastante enrrevesados pero han sido entretenidos.
Un saludo y hasta la proxima.


[^1]: Enlace de descarga del ejercicio.
[^2]: Descifrador Julio Cesar.
[^3]: Descompilador de Pyc Online.
[^4]: Utilidad CyberChef

