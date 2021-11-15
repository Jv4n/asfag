---
id: 1
title: "Cifrado con MD5 y SHA"
subtitle: "Como cifrar con MD5 y SHA"
date: "2021.11.15"
tags: "AFI, Actividad 1 ,MD5, SHA, HASH"
---

Lo que vamos a realizar en este ejercicio es cifrar una frase con distintos algoritmos de cifrado, tales como **MD5**, **SHA256** o **SHA512** de diversas maneras, y despues comprobar que de cualquiera de las maneras el Hash que nos da, coincide siempre.

>Uso de firmas mediante funciones hash md5, sha256 y sha512 con la utilidad 
ciberchef y con herramientas propias del sistema operativo.

[**PAGINA DE CYBERCHEF**](https://gchq.github.io/CyberChef/) [^1]

El texto que vamos a cifrar es el siguiente:

>**juan cifra este texto**

Bueno, pues ahora nos vamos a la pagina de CyberChef y vamos a cifrar nuestro texto.
A la vez vamos a irnos al terminal y vamos a cifrar el texto para comprobar que funcionan igual.

Vamos a comenzar realizandolo con MD5, en consola para comprobar el hash del archivo con md5 se usaria el comando **md5sum** fichero.


![imgur](https://i.imgur.com/qdNK5TI.png)[^2]

Vamos a realizar lo mismo con SHA256. La orden que necesitamos seria **sha256sum** fichero.

![imgur](https://i.imgur.com/kro20qM.png)[^3]

Por ultimo vamos a realizar el SHA512. La orden que usaremos sera **sha512sum** fichero.

![imgur](https://i.imgur.com/FVcVOYY.png)[^4]

Con este ejercicio hemos aprendido como funcionan los hash, como comprobarlos y para que sirven, ya que si modificamos algo de nuestro texto, este cambiara la salida de todos los hash.

Espero que os halla servido, Un saludo y hasta la proxima.


[^1]: Pagina de CyberChef
[^2]: Cifrado MD5
[^3]: Cifrado SHA256
[^4]: Cifrado SHA512
