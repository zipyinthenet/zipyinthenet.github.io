---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------
## Tar Command over SSH

Para realizar un fichero comprimido y el destino sea otro hosts

```bash
# tar zcvf - /wwwdata | ssh user@dumpserver.nixcraft.in "cat > /backup/wwwdata.tar.gz"
``` 

En caso de querer realizar sin poner el password tenemos varias opciones , entre ellas:

- Configurar llave ssh
- Usar sshpass antes de ssh

[Link](https://www.cyberciti.biz/faq/howto-use-tar-command-through-network-over-ssh-session/)

-----------------------------------------------------------------------------

ZipyintheNet¡
