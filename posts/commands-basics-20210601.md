---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## commands-basics

# DIRECTORIOS

```bash
$ pwd
```

Muestra por pantalla el nombre del camino completo del directorio actual.

```bash
$ cd [directorio]
```

Una vez que ya sabemos en qué directorio nos encontramos podemos empezar a desplazarnos por el árbol de directorios con la orden cd. El nombre de cd le viene de "cambiar de directorio" (en inglés, "change directory") y sirve exactamente para lo que parece: cambia el directorio actual al que nosotros le especifiquemos en su argumento.

Por ejemplo, estamos en el directorio /usr/share/man y queremos ir a /usr/bin. Tenemos las siguientes opciones:

```bash
$ cd /usr/bin

$ cd ../../bin
```

Sin parametros, establece como directorio de trabajo el home del usuario

```bash
$ mkdir [opciones] directorio
```

Esta orden sirve para crear una carpeta o directorio cuyo nombre será el que le pasemos como argumento a dicha orden.

Si, por ejemplo ejecutamos el comando $ mkdir nuevodirectorio, se creará el directorio nuevodirectorio en el directorio de trabajo actual.

También podemos crear directorios en lugares distintos al que nos encontramos, mediante el uso de rutas absolutas o relativas. Así, si deseamos crear el directorio Musica en /etc y nos encontramos en /home/alumno, tenemos 2 opciones:

```bash
$ mkdir /etc/Musica, o bien $ mkdir ../../etc/Musica
```

Con el comando mkdir también podemos crear varios directorios en una misma orden. Para ello, no tenemos más que introducir tantos argumentos como carpetas queramos crear. Así, la orden $ mkdir Documentos Imagenes Musica, creará esos 3 directorios en el directorio actual de trabaj

```bash
$ rmdir  directorio
```

La orden rmdir sirve para eliminar un directorio cuyo nombre será el que le pasemos como argumento. Su nombre proviene del inglés Remove Directory, que significa Borrar Directorio Como condición para el borrado, el directorio deberá estar vacío. Si no, nos mostrará un mensaje diciendo que tiene contenido.

Así, si queremos borrar la carpeta Cosas que está en nuestro directorio de trabajo actual y no contiene nada, ejecutaremos $ rmdir Cosas.

Si el directorio no existiese, nos avisará y no sucederá nada.

# FICHEROS

```bash
$ touch fichero
```

La orden touch sirve para cambiar la fecha de acceso y modificación de un fichero que le pasemos como argumento. Si dicho fichero no existe, lo creará vacío con el nombre que le hayamos pasado como argumento.

Por ejemplo, si ejecutamos la orden $ touch ejemplo.txt, creará un archivo vación con el nombre "ejemplo.txt" si no existía anteriormente, o simplemente modificará su fecha de acceso y modificación con la fecha actual del sistema, si existía con anterioridad.

Al igual que con el comando mkdir, con la orden touch podemos crear varios archivos con una sola orden: $ touch fich1 fich2 fich3 fich4

```bash
$ cat [opciones] [fichero]
```

Muestra en el shell el contenido completo del fichero de texto que se le pasa como argumento. Si le pasamos varios argumentos, mostrará los ficheros de texto en el orden en que se lo indiquemos como si fuesen uno sólo, sin distinguir qué línea corresponde a qué fichero. Sus principales opciones son las siguientes:

* cat -n numera todas las líneas del texto, incluso las vacías. En concreto, pone un número delante de cada línea al mostrarlas por pantalla.
* cat -b numera todas líneas del texto que no sean vacías. Las líneas vacías las muestra pero no les pone ningún número delante.

Como podemos ver, la orden cat no dispone de demasiadas opciones en cuanto a la visualización de textos, por lo que es la manera más rudimentaria de verlos en el shell.

```bash
$ cp [opciones] fichero1 fichero2
```

Esta orden se utiliza para copiar ficheros. Proviene del inglés Copy, y copia el archivo que se le pasa por parámetro (origen) en otro cuyo nombre se le pasa como segundo parámetro (destino).

Por ejemplo, si ejecutamos la orden $ cp fichero1.txt copiafichero1.txt, se copiará el contenido del fichero fichero1.txt en copiafichero1.txt, encontrándose ambos en el directorio de trabajo actual.

Por otro lado, si en lugar de un fichero, indicamos como destino un directorio, lo que sucederá es que creará una copia del archivo origen en el destino especificado. Por ejemplo: $ cp fichero2.txt /home/alumno, creará un archivo con el mismo nombre que el original en el directorio /home/alumno.

En la orden cp, al igual que en la orden rm, disponemos de la opción -R para copiar directorios enteros con todo su contenido.

Así, si ejecutamos la orden $ cp -R /home/alumno/directorio1 /tmp, copiará todo el contenido de la carpeta directorio1 en el destino indicado, que en este caso es /tmp.

```bash
$ rm [opciones] fichero 
```

Sirve para eliminar un archivo cuyo nombre será el que le pasemos como argumento. Por ejemplo, para borrar el archivo con nombre borrame.txt, ejecutaremos la orden $ rm borrame.txt.

Si el archivo que queremos mostrar no existe, nos mostrará un error.

Al igual que hemos visto en otras órdenes, podemos borrar varios ficheros o directorios (según la orden) en una linea si se los pasamos como argumento. Así, si ejecutamos $ rmdir pepito juanito paquito, borrará esos 3 directorios del directorio de trabajo actual.

La orden rm tambiénn sirve para eliminar directorios completos. Si el directorio contiene ficheros y queremos borrar tanto el directorio como su contenido tendremos que usar la orden rm con la opción -R. Mucho cuidado al utilizar esta opción, ya que podríamos borrar información importante.

```bash
$ mv [opciones] fichero1 fichero2
```

Esta orden tiene el efecto de mover archivos de un directorio a otro, según se le indique. Proviene del inglés Move. Si, por ejemplo, queremos mover el archivo mueveme.txt que se encuentra en el directorio actual, al directorio /home ejecutaríamos mv mueveme.txt /home/mueveme.txt

La orden mv tiene otra utilidad, que es la de cambiar el nombre a un archivo. Para ello, no tenemos más que pasarle como argumentos el nombre del fichero que queremos renombrar y el nombre nuevo, de la siguiente manera: $ mv antiguonombre.txt nuevonombre.txt

```bash
$ ln [opciones] fichero enlace
```

Esta orden, se utiliza para crear un enlace duro al fichero que se le pasa como argumento. Así, si ejecutamos la orden

$ ln mifichero mifichero1, se creará un enlace duro al fichero "mifichero", que tendrá como nombre "mifichero1".

Para crear un enlace simbólico disponemos de la opción -s de esta misma orden, que se ejecutará de la misma manera que la anterior. Por ejemplo, la orden $ ls -s mifichero mifichero2, creará un enlace simbólico al fichero "mifichero", que tendrá como nombre "mifichero2".

```bash
$ unlink fichero
```

Para borrar un enlace, también podemos utilizar la orden rm, pero es más indicado utilizar unlink. La finalidad de esta orden es borrar un enlace existente. En el caso en que dicho enlace sea el último que hace referencia al inodo, el fichero se borrará dejando el espacio disponible. En caso de que exista algún otro, sólo se borrá el enlace.

Si, por ejemplo, deseamos borrar el enlace duro enldurofichero, ejecutaremos $ unlink enldurofichero.

```bash
$ file [opciones] fichero
```

Determina el tipo de fichero.

# SISTEMA DE FICHEROS

```bash
$ du
```

Muestra un resumen del uso de disco para cada fichero, recursivamente para directorios.

Opciones:

* -a --> Muestra todos los ficheros
* -b --> Muestra el tamaño en bytes
* -h --> Muestra los tamaños de forma legible (p.ej., 1K 234M 2G)

```bash
$ df [opciones] [fichero]
```

Muestra información sobre el sistema de ficheros en el que reside cada fichero, o por omisión sobre todos los sistemas de ficheros.

Opciones


* −h --> Imprime los tamaños en formato legible (p.e. 1K 234M 2G)
* −i --> Muestra la información de nodos-i en lugar del uso de bloques
* −l --> Limita el listado a los sistemas de ficheros locales

# INFORMACIÓN DEL USUARIO

```bash
$ whoami
```

Muestra el usuario

```bash
$ id [opciones] [usuario]
```

Muestra información del usuario especificado (uid, gid, grupos, etc.).

```bash
$ uname -a
```

Muestra la versión de Linux

```bash
$ hostname
```

Nombre de la máquina

```bash
$ who [opciones]
```

Muestra los usuarios conectados

Opciones 

* −b --> Tiempo del último inicio del sistema
* −H --> Muestra la línea de encabezados de columnas
* −r --> Muestra el runlevel actual

```bash
$ w [opciones]
```

Muestra información sobre los usuarios conectados

# FILTROS

```bash
$ tr [opciones] conjunto1 [conjunto2]
```
Traduce, comprime y borra caracteres de la entrada estándar, escribiendo el resultado en la salida estándar.

Opciones:

* −c --> Opera sobre el complemento (sobre cada carácter que no coincida)
* −d --> Borra caracteres de conjunto1, no traduce
* −s --> Remplaza cada sucesión de entrada de un carácter repetido del conjunto1 por una sola aparición de dicho carácter.

```bash
$ head [opciones] [fichero]
```

Muestra las 10 primeras líneas de cada fichero en la salida estándar.

Opciones:

* −cTAMAÑO --> Muestra los primeros TAMAÑO bytes
* −nN --> Muestra las N primeras líneas

```bash
$ tail [opciones] [fichero]
```

Muestra las 10 últimas lineas de cada fichero en la salida estandar

Opciones..

* cN --> muestra los ultimos N bytes.
* f --> muestra a medida que el fichero crece.
* nN --> muestra las ultimas N lineas.

Si el primer caracter despues de N es un +, muestra a partir de la linea N

```bash
$ sort [opciones] [fichero]
```

Muestra la concatenación ordenada de todos los ﬁcheros en la salida estándar.

Opciones de ordenación:

* -b --> Descarta los espacios en blanco al principio
* -g, n --> Compara de acuerdo con el valor numérico
* -r --> Invierte el resuItado de las comparaciones
* -k POS1[,POS2] --> Establece el criterio de ordenación en POS1 y la termina en POS2. Un sélo campo, POS1=POS2. Si no indicamos POS2, hasta el final. El primer campo es 1.
* -o FICHERO -> Escribe el resultado en FICHERO, en lugar de la salida estandar
* -t SEP --> Usa SEP en lugar de espacio para separar los campos
* -u --> Muestra solamente la primera de una serie de repeticiones

```bash
$ uniq [opciones] [ENTRADA] [SALIDA]
```

Descarta todas las líneas sucesivas idénticas, menos una de ENTRADA (o entrada estándar), escribiendo en SALIDA (o en la salida estándar).

Opciones:

* −c --> Precede a las líneas con el número de ocurrencias
* −d --> Muestra sólo las líneas duplicadas
* −u --> Muestra sólo las líneas que son únicas

```bash
$ cut [opciones] [fichero]
```

Extrae las partes seleccionadas de cada fichero en la salida estándar.

Opciones:

* −c --> muestra solamente los caracteres que ocupan la posición indicada
* −dDELIM --> Utiliza DELIM en vez del tabulador para delimitar los campos
* −f --> Muestra solamente los campos que ocupan la posición indicada
* −cN --> No muestra las líneas que no contienen delimitadores

```bash
$ more fichero
```

Permite avanzar por el documento línea a línea pulsando la tecla Intro o página a página mediante la barra espaciadora.

Opciones:

* -X --> permite especificar el número de líneas que queremos que muestre por cada página. Por ejemplo, si queremos visualizar 6 líneas por página ejecutaríamos more -6.
* +X -->  comienza la visualización delfichero en la línea X. Por ejemplo, si queremos ver un fichero a partir de su línea 13 pondríamos more +13.

Si estamos visualizando un documento con la orden more y pulsamos la letra h veremos todas las opciones que nos ofrece durante la visualización.

```bash
$ less fichero
```

Permite avanzar y retroceder línea a línea con las flechas de dirección o avanzar página a página mediante la barra espaciadora y retroceder una página mediante la tecla w. Si visualizamos un fichero con less y preionamos la tecla h veremos una ayuda que nos indicará las teclas que podemos usar para desplazarnos por el documento.

Opciones:

* -e --> Hace que se salga automáticamente de la visualización cuando se llega por segunda vez al final del fichero. La primera vez que se llega al final del fichero se permanece en la visualización. Es muy útil para no tener que acordarse de salir con la q.
* -E --> Es muy similar a la anterior opción, pero hace que se salga de la visualización cuando se llega al final del fichero por primera vez.
* -F --> Hace que se salga de la visualización automáticamente si el fichero puede ser mostrado en una sola página.
* -N --> Muestra un número de línea delante de cada línea de texto que contiene el fichero.
* -w -->Al avanzar una página nos señala cual es la primera línea que no estaba en la página anterior. Sirve para saber por donde nos habíamos quedado leyendo cuando cambiamos a la siguiente página.

```bash
$ grep [opciones] patron [fichero]
```

Muestra por la salida estándar el fichero filtrando la lineas en función del patrón y las opciones

Opciones

* -i --> Considera iguales mayúsculas y minúsculas
* -w --> Obliga a que patrón coincida solamente con palabras completas
* -x --> Obliga a que patrón coincida solamente con lineas completas
* -v --> Selecciona las lineas que no coinciden
* -mNUM --> Se detiene después de NUM coincidencias
* -n --> Muestra el namero de "ma junto con las líneas de salida

patron pude construirse mediante:

* Expresión regular
* Frase (entre comillas)

```bash
$ wc [-cwl] [fichero]
```

Cuenta los caracteres, palabras y llneas de un fichero

```bash
$ find ruta opciones
```

Busca los ficheros que satisfacen la expresión de búsqueda a partir de los directorios señalados

Opciones:

* −name --> nombre
* −type -->  f,d,l,etc.
* −size --> tamaño
        c --> byte, k kilobyte
        + --> mayor que
        - -->  menor que
        sin signo igual al tamaño
* perm --> Permisos
        en octal
        en simbolo ugo+-rwx;
        - delante indica al menos esos permisos, sin menos los permisos exactos
* links --> número de enlaces
* user --> propietario de los ficheros

Por defecto cada expresién va unida par and, explicitamente -a. También podemos unir las expresiones por or -o.

Se pueden poner paréntesis \(.... \).

Se pueden realizar ejecuciones para los ficheros que cumplan las condiciones

    - $ find ruta opciones -exec comando {} \;
    - $ find ruta opciones -ok comando {} \;
        Pide conﬁrmación


-----------------------------------------------------------------------------

ZipyintheNet¡