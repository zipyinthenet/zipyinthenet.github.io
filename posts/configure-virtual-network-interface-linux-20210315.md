---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------
## Configure Virtual Network Interface Linux

ejemplo:

Static
```bash
/etc/sysconfig/network-scripts

vim /etc/sysconfig/network-scripts/ifcfg-eth0:0

DEVICE=eth0:0
IPADDR=123.123.22.22
NETMASK=255.0.0.0
NETWORK=123.0.0.0
BROADCAST=123.255.255.255
ONBOOT=yes
```

DHCP
```
DEVICE=eth0:0
BOOTPROTO=dhcp
ONBOOT=yes
```

Al final reiniciar servicio
```
 service network restart
```

[Link](https://linuxconfig.org/configuring-virtual-network-interfaces-in-linux#h3-redhat-fedora-centos)

-----------------------------------------------------------------------------

ZipyintheNet¡
