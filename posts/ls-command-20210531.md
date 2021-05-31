---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## ls-command-20210531

```bash
$ ls [opciones] [fichero]
```

Una vez que estamos en un directorio concreto lo más probable es que queramos saber el contenido del directorio. Para ello disponemos de la orden ls. Su nombre viene de "listar" (en inglés, "list") y eso es precisamente lo que hace, listar el contenido de un directorio. Si le pasamos un argumento nos mostrará el contenido del directorio que le pasamos y si no, nos mostrará el contenido del directorio actual. La orden ls tiene multitud de opciones. A continuación vamos a ver las más destacadas:

* ls -a muestra todos los archivos y directorios, incluso los ocultos (los que comienzan con un punto).
* ls -l muestra un listado en el formato largo, con información de permisos (que ya explicaremos más adelante), número de enlaces duros asociados al archivo, usuario, grupo, tamaño en bytes y fecha de última modificación además del nombre.
* ls -lh muestra la misma información que con la opción -l pero el tamaño del fichero se muestra en unidades más entendibles (K, M, G...).
* ls -S muestra el contenido ordenado por tamaño de archivo.
* ls -t muestra el contenido ordenado por la fecha de última modificación.
* ls -r muestra el contenido ordenado de forma inversa.
* ls -R muestra la estructura de directorios que cuelga del directorio actual o del que le pasemos como argumento.
* ls -i muestra el número del inodo en el que están los datos de cada fichero o directorio. Si tenemos 2 ficheros que son enlaces duros del mismo fichero veremos que el número del inodo es el mismo.
* ls -m muestra los ficheros y directorios en una sola fila, separados por comas.
* ls -1 muestra los ficheros y directorios en una sola columna.

Las opciones pueden combinarse entre sí. Por ejemplo, si ejecutamos la orden ls -lSa se mostrará por pantalla el contenido del directorio actual ordenado por el tamaño de los ficheros (por la opción -S) mostrando también los archivos ocultos (por la opción -a) y en formato de lista larga (por la opción -l).


-----------------------------------------------------------------------------

ZipyintheNet¡