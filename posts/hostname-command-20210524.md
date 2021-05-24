---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## hostname-command

# PASO 1: checkear Hostname existente

```bash
hostnamectl
```

# PASO 2: Setear un nuevo hostname staticamente (sin reinicio)

```bash
hostnamectl set-hostname mi.nuevo-hostname.servidor
```

# PASO 3: checkear Hostname

```bash
hostnamectl
```

# PASO 4: editar el fichero /etc/hosts

```bash
sudo vim /etc/hosts
```

```bash
127.0.0.1  localhost localhost.localdomain localhost 4 localhost4.localdomain4 mi.nuevo-hostname.servidor
```

LINKS
[link1](https://phoenixnap.com/kb/how-to-set-or-change-a-hostname-in-centos-7)
[link2](https://www.tecmint.com/set-change-hostname-in-centos-7/)
[link3](https://www.asplhosting.com/portal/en/cambiar-hostname-en-tu-centos-7)

-----------------------------------------------------------------------------

ZipyintheNet¡