---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------
## Rsync Command

Con el comando Rsync puedes sincronizar ficheros del sistema , de forma que se pueden hacer copias.

Referencias:
[link](https://www.linuxadictos.com/rsync-como-crear-copia-seguridad-incremental.html#Como_crear_las_copias_con_rsync)

ejemplo:

copia de seguridad completa
```bash
rsync -avh /ruta/origen /ruta/destino
```
copia de seguridad incremental
```bash
rsync -avhb --delete --backup-dir=/ruta/destino/copia_$(date +%d%m%Y%H%M) /ruta/origen/ /ruta/destino/
```
La sincronizacion incremental , realiza copias completas y a su vez guarda el fichero origen que se guardaba en destino de la anterior copia , de forma que guardamos los cambios en el tiempo de los ficheros. Siempre y en el momento que ejecutemos la herramienta/tool/programa rsync.

En caso de querer automatizar la sincronizacion de ficheros entre el fichero origen y destino , podemos usar crontab.

editamos crontab
```bash
crontab -e
```
Configuramos en Crontab cuando queremos que se ejecute el script de bash , el cual contiene la linea de nuestro rsync que se va a ejecutar...

La herramienta es potente y se puede usar en cualquier momento necesario en el sistema o cuando se este realizando ciertos scripts por ejemplo de Bash y se necesite para cualquier cosa.

Espero que sirva de ayuda.

Saludos

-----------------------------------------------------------------------------

ZipyintheNet¡ 2020!®
