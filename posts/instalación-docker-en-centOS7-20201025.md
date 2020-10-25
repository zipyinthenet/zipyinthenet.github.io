---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## instalación-docker-en-centOS7-20201025

Para la instalación de Docker en Centos7 existen 3 posibilidades:

*   Mediante script y herramienta curl con el link get.docker.com --> [install-using-the-convenience-script](https://docs.docker.com/engine/install/centos/#install-using-the-convenience-script).
*   Desde repositorios utilizando yum --> [install-using-the-repository](https://docs.docker.com/engine/install/centos/#install-using-the-repository).
*   Mediante paquetes rpm descargados --> [install-from-a-package](https://docs.docker.com/engine/install/centos/#install-from-a-package).

Yo he decidido realizar la tarea de instalación mediante script y herramienta curl.

Descargar tal script y ejecutarlo , mediante sudo con un usuario con privilegios o gestionarlo mediante root , realizar la tarea de una forma u otra:

![x](https://miro.medium.com/max/444/1*ZQIBBEq6h4Pg1311DVsRWw.png)

Si lo realizamos con un usuario

![x](https://miro.medium.com/max/358/1*Bm755am358MhOFmDzWEohA.png)

Arrancamos el servicio

![x](https://miro.medium.com/max/444/1*vvV5kTdbPJCAMhfl-LCqeQ.png)

Y configuramos arranque al inicio del sistema también.

![x](https://miro.medium.com/max/700/1*Z09NAg5l2RRvHiEND-O6Tg.png)

Mediante Docker info , podemos ver información de docker en el sistema.

![x](https://miro.medium.com/max/147/1*PNPnbdfC6-4LTcXSmA7gDg.png)

Con Docker version , podremos ver version de docker

![x](https://miro.medium.com/max/158/1*EVhR2Bz6nPUUbw0pT-rvOQ.png)

Podemos comprobar el primer contenedor de prueba corriendo

![x](https://miro.medium.com/max/652/1*v3gxCQXl0KBi1DFhzQlUAA.png)

Con docker images , podemos ver las imagenes que tenemos

![x](https://miro.medium.com/max/700/1*rNbaOdQFAcC0GFGZPh5r-Q.png)

Próximos capítulos , configuración de docker en el sistema..

Fuentes:

* [install-using-the-convenience-script](https://docs.docker.com/engine/install/centos/#install-using-the-convenience-script)

Video:
* [Instalar Docker en CentOS 7 o Fedora](https://www.youtube.com/watch?v=xkIJH-swqPc)

-----------------------------------------------------------------------------

ZipyintheNet¡ 2020!®