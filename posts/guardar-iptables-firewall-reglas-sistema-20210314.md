---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------
## Guardar reglas iptables sistema 

Para guardar las reglas editadas de iptables y que sean persistentes en el sistema

guardar reglas debian ubuntu realizar:
```bash
iptables-save > /etc/iptables/rules.v4

ip6tables-save > /etc/iptables/rules.v6
```

restaurar ubuntu o debian:
```bash
iptables-restore < /etc/iptables/rules.v4

iptables-restore < /etc/iptables/rules.v6
```

para mantener reglas:
```bash
apt-get install iptables-persistent
```

* * *

realizar(server centOS) guardar reglas:
```bash
iptables-save > /etc/sysconfig/iptables

ip6tables-save > /etc/sysconfig/ip6tables
```

habilitar servicio
```bash
chkconfig iptables on
```

por seguridad
```bash
service iptables save
```

[link](https://www.sololinux.es/mantener-las-reglas-de-iptables-al-reiniciar-el-sistema/) [link2](https://www.thomas-krenn.com/en/wiki/Saving_Iptables_Firewall_Rules_Permanently)


-----------------------------------------------------------------------------

ZipyintheNet¡ 2020!®
