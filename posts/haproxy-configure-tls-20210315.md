---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------
## HAPROXY tls configure server

Para configurar TLS sin verificar:

```bash
global
   # Bind the Runtime API to a UNIX domain socket and/or an IP address
   stats socket /var/run/hapee-2.1/hapee-lb.sock user hapee-lb group hapee mode 660 level admin
   stats socket ipv4@*:9024 level admin

   # Set a timeout for how long you can stay connected to the Runtime API,
   # which is useful for longer interactive terminal sessions
   stats timeout 10m

   # Set remote or local Syslog server addresses to send log files to
   log 127.0.0.1 local0
   log 127.0.0.1 local1 notice

   # Set the user and group to run HAProxy Enterprise as
   user  hapee-lb
   group hapee

   # Run the process in a chrooted directory
   chroot /var/empty

   # Set the path from which to load Enterprise modules
   module-path /opt/hapee-2.1/modules

frontend myfrontend
   mode http
   bind *:80
   default_backend web_servers

backend webservers
   server web1 10.0.0.5:443 ssl verify none
   server web2 10.0.0.6:443 ssl verify none
```

[Link](https://www.haproxy.com/documentation/hapee/2-1r1/security/tls/)


-----------------------------------------------------------------------------

ZipyintheNet¡
