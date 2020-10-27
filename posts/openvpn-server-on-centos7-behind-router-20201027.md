---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## openvpn-server-on-centos7-behind-router

Se ha escogido para realizar la tarea Openvpn ya que ofrece la posibilidad de ajustarse a un montón de configuraciones y escenarios que requiera la red y los servidores o máquinas que requieran conexión. La documentación es muy extensa y la comunidad es muy proactiva por tanto es un punto a favor. Otro punto a favor es la documentación y ejemplos que ya trae con comentarios que explica cómo funcionan los ficheros. El uso de easy rsa al principio puede ser un poco lioso ya que la documentación de openvpn en la web oficial está realizada tanto para linux como windows. En cuanto a easy-rsa, el script y versión es mayor a la especificada en la documentación openvpn pero mediante la ayuda que trae el comando es fácil acabar de comprender su uso. Por último me gustaría destacar que openvpn es muy potente pero requiere de un estudio de implementación mediante iptables para manejar las rutas de los host mediante el firewall de las máquinas donde esté instalado openvpn, en este caso solo en el servidor, pero en otro aspecto podría ser en un router de enlace punto a punto. 

Implementación:

Instalar paquete openvpn y easy-rsa.

![x](https://miro.medium.com/max/471/0*cHemmL7p2NzAumot)

Copiamos directorio easy-rsa en el directorio de configuración de openvpn.

![x](https://miro.medium.com/max/318/0*EeWdGdYUT99T2_IO)

Copiamos el fichero vars.example en el directorio easy-rsa ubicado en configuración de openvpn.

![x](https://miro.medium.com/max/700/0*z3yaBSFUobi-EOEn)

Renombrar el fichero vars.example a “vars”.

![x](https://miro.medium.com/max/617/0*DOMOVP5m3dp83MLS)

Editamos el fichero vars descomentar y editar en las líneas 95 a 100 dando los valores específicos para el certificado.

Descomentar y línea 108.

![x](https://miro.medium.com/max/434/0*_Qxt08-wcb3NNMqn)

Descomentar líneas 125 y 129.

![x](https://miro.medium.com/max/449/0*xYEJtO7kOpdmHlSI)

Si ejecutamos en el directorio easy-rsa “./easyrsa help” nos muestra la ayuda del script.

![x](https://miro.medium.com/max/700/0*qmA7TSPiNT3b4kmZ)

Creamos la request para construir la CA mediante init-pki con script easyrsa. (tomará los valores de vars, mismo directorio /etc/openvpn/easy-rsa/3/“”)

![x](https://miro.medium.com/max/700/0*kYlnbhjjVkF9G08x)

Construimos la CA mediante script easyrsa y mediante build-ca construimos la ca. Añadimos nopass para en este caso ,no ponerle contraseña a la CA que vamos a construir.

![x](https://miro.medium.com/max/700/0*0sQbzxbM7erACYWW)

Generamos el certificado y llave del servidor mediante el script easyrsa y con la opción gen-req generamos el certificado y llave.

Mediante server indicamos que va a ser certificado y clave de servidor y mediante nopass no se añade contraseña al certificado del servidor.

![x](https://miro.medium.com/max/700/0*_ABRjxw0v5oGgagS)

Con el script easyrsa , utilizamos sign-req para firmar el certificado que hemos generado e indicamos server para firmar el tipo de certificado y el nombre del certificado. Se creará el certificado firmado.

![x](https://miro.medium.com/max/700/0*JZ4fNH1TS_-z6GVs)

Podemos verificar con herramienta openssl , mediante la CA que hemos creado si está correcto el certificado del servidor. En este caso es OK.

![x](https://miro.medium.com/max/700/0*hmje6alz7yYvOJam)

Mediante script easyrsa también podemos generar clave diffie hellman.

![x](https://miro.medium.com/max/700/0*UD1aEMpPwN3ZmwTT)

Por último generamos el certificado del cliente 1 , en este caso sin firmar también. Podríamos poner contraseña al certificado para autenticarse pero este caso el cliente podrá autenticarse teniendo los ficheros del cliente sin contraseña.

![x](https://miro.medium.com/max/700/0*aHNMcejhiNbDgXML)

Firmamos el certificado del cliente y tendremos el certificado firmado mediante script rsa.

![x](https://miro.medium.com/max/700/0*-CFFF1XL0XAJ6Teo)

Copiamos ficheros generados para configuración servidor. CA , dh.pem , certificado servidor y clave servidor.

![x](https://miro.medium.com/max/700/0*-ASBV6DhZXJlHowh)

Creamos un directorio llamado ficheros_clientes para alojar ficheros que deben de tener los clientes.

![x](https://miro.medium.com/max/428/0*SC7jdDsMh_CHIVg7)

Copiamos la CA del servidor para los clientes.

![x](https://miro.medium.com/max/700/0*jqG8xMC9oPTFEQy_)

Copiamos la clave y certificado generado para el cliente en el directorio de los ficheros de los clientes.

![x](https://miro.medium.com/max/700/0*VAjIpNmFvk_1iDN6)

Copiamos el ejemplo de fichero de configuración de openvpn server en el directorio de configuración de openvpn.

![x](https://miro.medium.com/max/700/0*BE3d32UabI51l3sZ)

Editamos el fichero de configuración server.conf.

![x](https://miro.medium.com/max/600/0*ShZfxg-coQ9Sv-qu)

línea 25 añadimos ip donde queremos que el servicio openvpn escuche.

![x](https://miro.medium.com/max/240/0*nPceAVXXE1WMrGKV)

línea 32 añadimos el puerto utilizado en el servidor para el servicio openvpn , puerto 4444.

![x](https://miro.medium.com/max/227/0*XfL-m6jnjdc6SAvl)

línea 36 editamos y utilizamos protocolo udp.

línea 53 editamos y utilizamos interfaz de red tun

![x](https://miro.medium.com/max/158/0*4sHWLn29vzCkOJOF)

línea 78–80 editamos y apuntamos donde se encuentran ubicados la CA del servidor , el certificado del servidor , y la llave.

![x](https://miro.medium.com/max/345/0*PEh-RQ2II1O5aYKp)

línea 85 editamos y apuntamos donde se encuentra ubicado la llave diffie hellman.

![x](https://miro.medium.com/max/391/0*M2I6DxNSzvntJLVv)

linea 92 editamos y utilizamos subnet.

![x](https://miro.medium.com/max/228/0*MsUksOeOSdjEql5R)

línea 101 editamos la red virtual y la máscara.

![x](https://miro.medium.com/max/352/0*2sHsO28F6bNoNj7t)

línea 108 editamos para guardar ips asignadas a clientes.

![x](https://miro.medium.com/max/373/0*exaZn2U345znv5yg)

linea 141 editamos para poder ir a otros host de la red del servidor.

![x](https://miro.medium.com/max/483/0*8UAsDVhjfNmYjiJx)

línea 231 descomentamos activamos keepalive para mantener conexiones clientes(ping timeout).

![x](https://miro.medium.com/max/221/0*NMPZAZfEhy_OUTVf)

linea 244 Comentamos para no utilizar en este caso autenticado tls. Para más seguridad utilizarlo.

![x](https://miro.medium.com/max/224/0*nyjxKjNHBDiR-Pvg)

linea 252 utilizamos cifrado aes256.

![x](https://miro.medium.com/max/285/0*04IsEb7Se2uzBL9T)

linea 281–282 ya viene descomentada para utilizar llave y conexión reabiertas con el túnel.

![x](https://miro.medium.com/max/173/0*SRHCmA_Kx9GnI0Ap)

línea 287 editamos y ubicamos log de openvpn

![x](https://miro.medium.com/max/390/0*tFstV4MEokZj2gT0)

linea 296–297 editamos y ubicamos log de openvpn

![x](https://miro.medium.com/max/422/0*VsOAB_69_8zBPpV6)

activamos el servicio openvpn@server y añadimos el servicio al arranque del sistema con systemd.

![x](https://miro.medium.com/max/700/0*7UtZARzoZ-ZGo7za)

Configuramos y activamos ip forwarding.

![x](https://miro.medium.com/max/271/0*pPgncBo4Q-q0mjeH)

Añadimos la siguiente línea con valor activado en 1.

![x](https://miro.medium.com/max/334/0*xAgAVaaR-llh0Yi9)

Comprobamos si está activado.

![x](https://miro.medium.com/max/396/0*rIXEFeIdsdPYuDiM)

Editamos reglas del firewall para openvpn(en caso de manejar fichero script con reglas iptables)

![x](https://miro.medium.com/max/322/0*VrJKNzIrOQY7TGDq)

Añadimos reglas de forwarding , entrada tunel y salida interfaz de red física del servidor y añadimos otra regla de forwarding con related y established de una red cualquier a otra para que los paquetes que se enrutan de una red por una interfaz de vuelta vuelvan a enrutar.

También añadimos regla nat de modo que enmascara todo el tráfico que sale de la red virtual por la interfaz de red física del servidor.

![x](https://miro.medium.com/max/700/0*Pr7PXwx4TOlDTkcn)

Añadimos reglas de entrada y salida puerta 4444 que utilizara el servicio con la interfaz de red física del servidor y protocolos udp. También añadimos regla entrada al servidor para en la interfaz virtual, de modo que mediante established editado en el fichero firewall podrá volver a salir por la interfaz virtual todo el tráfico.

![x](https://miro.medium.com/max/667/0*jLErqhvToZbg6ZPW)

Copiamos a la maquina del cliente los ficheros del cliente generados en el servidor.

![x](https://miro.medium.com/max/693/0*d8XDDCbu7HY4qI0B)

Copiamos y utilizamos el ejemplo de configuración de cliente en windows.

![x](https://miro.medium.com/max/700/0*0beBygh5rAiFTq_c)

Añadimos ficheros del cliente y editamos el fichero ejemplo ovpn del cliente copiado.

![x](https://miro.medium.com/max/700/0*EB0cnUQa6gUY52-T)

Línea 16 utilizamos client.

![x](https://miro.medium.com/max/404/0*OLwQF4cp04JFxS4t)

Línea 24 utilizamos interfaz de red tun

![x](https://miro.medium.com/max/382/0*FmcjFUJXS-mhLzW5)

Línea 37 utilizamos protocolo udp

![x](https://miro.medium.com/max/328/0*uI0unjpaLxi2xOQl)

Línea 42 editamos y añadimos dirección ip servidor y puerto.

![x](https://miro.medium.com/max/342/0*oy3WsMtpTKcddfnB)

Línea 53 utilizamos para resolver indefinidamente con el servidor.

![x](https://miro.medium.com/max/396/0*dk9fJ-_cLXb3mUtv)

Linea 57 utilizamos nobind.

![x](https://miro.medium.com/max/336/0*xKWyXu9cjObyX5M_)

Línea 64 y 65 utilizamos para reconectar con clave y túnel en el servidor

Linea 87 a 89 editamos la ubicación de los ficheros del cliente. CA , certificado y llave.

![x](https://miro.medium.com/max/331/0*Nmd-bwyVgWc9sX1B)

Utilizamos cifrado aes 256 línea 116

![x](https://miro.medium.com/max/429/0*Y0-gehDBv_AZ_OHK)

Linea 124 nivel verbosidad fichero log cliente5.

![x](https://miro.medium.com/max/256/0*48HxXGPKdF7qTT84)

Después de instalar los ficheros en el cliente. Conectamos con otra máquina en otra red para simular estar en internet.

![x](https://miro.medium.com/max/515/0*AsYwMIwnLXZldqqm)

Copiamos los ficheros en la siguiente ubicación del cliente

![x](https://miro.medium.com/max/700/0*BjNu0k4uAifT6C8V)

Una vez copiados podremos comenzar a conectar.

![x](https://miro.medium.com/max/700/0*zwU7ItB48b85Nqvr)

Para conectar en el agente de openvpn escogemos el cliente que queremos y clicamos en connect.

![x](https://miro.medium.com/max/488/0*nCMyd2KV0_kJQ35E)

Cabe destacar que habría que abrir los puertos en el router para simular que el servidor esté en internet mediante puerto 4444. Router compañía realizará port mirroring hacia el servidor.

![x](https://miro.medium.com/max/700/0*jATZQGXXlON7x9-1)

Y podremos conectarnos mediante nuestro cliente.

![x](https://miro.medium.com/max/568/0*gTmEvKOwsLYGJEbk)

Podemos comprobar que ip tenemos tanto local en la red que nos encontramos conectados, como la ip que tenemos en el túnel de la conexión virtual mediante openvpn

![x](https://miro.medium.com/max/320/1*fmEKxOLAdAQWxmiFF03nFQ.png)

Nos haría falta copiar a un cliente la clave del cliente ssh para probar el túnel openvpn.

![x](https://miro.medium.com/max/482/1*ZKT0vcQWGuy0yThqWfTVnw.png)

Realizamos la primera conexión, comprobamos que podemos conectar desde la red 192.168.53.0/24 mediante el tunel openvpn a la red 192.168.1.0/24 donde se encuentra el servidor.

![x](https://miro.medium.com/max/693/1*A-d5cL5sNbX8jEMejNyGDg.png)

Cerraremos la conexión y volveremos a abrir y podremos fijarnos que ssh nos comenta el último log de sesión con la ip del túnel.

![x](https://miro.medium.com/max/640/1*kXF34w-7cfLL0q02aFbpxg.png)

Fuentes:

* [crear-una-vpn-en-debian](https://www.creadpag.com/2020/05/crear-una-vpn-en-debian-10.html)
* [server-world openvpn](https://www.server-world.info/en/note?os=CentOS_7&p=openvpn&f=1)
* [BridgingAndRouting](https://community.openvpn.net/openvpn/wiki/BridgingAndRouting)
* [arashmilani](https://arashmilani.com/post?id=53)
* [creating-configuration-files-for-server-and-clients](https://openvpn.net/community-resources/how-to/#creating-configuration-files-for-server-and-clients)
* [how-to/#vpntype](https://openvpn.net/community-resources/how-to/#vpntype)
* [how-to-install-openvpn-on-centos-7](https://www.howtoforge.com/tutorial/how-to-install-openvpn-on-centos-7/)

-----------------------------------------------------------------------------

ZipyintheNet¡ 2020!®