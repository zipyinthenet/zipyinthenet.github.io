---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## smtp-relay-server-con-postfix

Esta vez vamos a realizar un servidor de correo SMTP (solo de SMTP), con la finalidad de enviar correos con una cuenta de GMAIL (se podria conf para otros dominios , supongo). La idea realmente es parecida a la siguiente forma de verlo conceptualmente , el servidor SMTP que tengamos en la red Local , enviara los correos salientes al servidor SMTP de GMAIL y los enviara a la bandeja de salida de el servidor SMTP de GMAIL. El servidor de GMAIL confiara en nuestro servidor SMTP ya que al fin y al cabo , nuestro servidor SMTP local esta funcionando como un cliente mas de esa cuenta de GMAIL. Pero en vez de enviar los correos por la bandeja de salida de un cliente web de gmail , o un cliente de escritorio de gmail , es el servidor local smtp el que enviar al servidor smtp de gmail y gmail reenvía a el destinatario y ahí ya entraría … los servidores pop o imap o servidores smtp de otros dominios/organizaciones…etc.

El caso es que nos centramos en enviar MEDIANTE smtp LOCAL al servidor SMTP de GMAIL.

Para ello vamos a poner las características de como lo he configurado y que he necesitado, pero antes cabe destacar:

*   No he utilizado servidor DNS , por el momento no dispongo , así que en /etc/hosts nos vamos a auto apuntar para hacerlo todo mediante localhost.
*   El servidor SMTP que vamos a configurar es local, no hace falta abrir puertos en el router , en principio nuestro router ya realiza el propio NAT(si es un router de la compañía).
*   Debéis configurar si tenéis firewall en el servidor levantado , abrir el puerto 25 para dejar salir el trafico por el servidor , eso si que es elemental , queridos.
*   Otros puntos a tener en cuenta.. Va a ser realizado en Centos7.
*   Y mas cosas como que al tener un servidor local , en nuestro caso en un futuro si tenemos dns local , podremos cambiar que el servidor smtp apunte al servidor dns local y así resolver a Internet…
*   Y en caso de que queramos que otros servicios que tenemos en otro servidores , apunten y utilicen el relay de nuestro servidor smtp , debemos servir en la red local que se encuentren los servidores o redes para que el servidor smtp acepte peticiones de esas redes… Yo lo he realizado todo mediante Localhost. Si el mismo servidor que vais a utilizar va a tener el servicio smtp y otros mas .. Pues con servir en localhost , serviría. En caso de tener servidor dns en un futuro si que debemos servidor en la red mediante registro mx …etc

Para empezar:

cambiar nombre máquina

![x](https://miro.medium.com/max/441/0*NjMoG5-w7tQ6LgGX)

añadir al fichero hosts nombre fqdn y dominio que queramos apuntando a localhost (esto es en caso de no tener dns , resolvemos a localhost con el nombre de la máquina) , conviene reiniciar después la maquina.

![x](https://miro.medium.com/max/649/0*j6frasfALAKeHJCv)

instalamos los paquetes necesarios

![x](https://miro.medium.com/max/700/0*UhPEY9NzSGdHvUP-)

editamos el fichero main.cf de postfix ,antes de editar,realizar un backup del original.

/etc/postfix/main.cf

![x](https://miro.medium.com/max/620/0*__L1_G0DqoXblDrO)

Una vez realizado editar , con vim con nano . El editor que deseemos.

![x](https://miro.medium.com/max/577/0*Rmoo_kvtFJ08NLjn)

a continuación realizar cambios , descomentando o editando valores

línea 75 cambiar

![x](https://miro.medium.com/max/288/0*BLsnWLK7p5Q_HhIt)

linea 113–116 cambiar

![x](https://miro.medium.com/max/231/0*TXhVKAtgoz0fxCrn)

línea 119 cambiar

![x](https://miro.medium.com/max/193/0*leSDyUf3Db0W9Juq)

línea 164 cambiar

![x](https://miro.medium.com/max/412/0*h1wW-0KhQqATd5Yf)

al final del fichero añadir

![x](https://miro.medium.com/max/465/0*5Kv2-9ZrcKITz8Ad)

crear fichero sasl_passwd

![x](https://miro.medium.com/max/572/0*I6NvrqXCwRo7axfL)

añadir lo siguiente:

```
'[smtp.gmail.com]:587 nombredelcorreodegmail@gmail.com:passworddegmail'
```

Mediante postmap creamos fichero db de sasl_passwd para postfix

```
'# postmap /etc/postfix/sasl_passwd'
```

permisos lectura propietario solo

```
'# chmod 400 /etc/postfix/sasl_passwd'
```

convertimos en propietario y grupo a root de los 2 ficheros

```
'# chown root:root /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db'
```

'cambiamos permisos a root sobre los 2 ficheros'

```
# chmod 0600 /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
```

recargamos conf de postfix

```
# systemctl reload postfix
```

necesitamos conf la cuenta de gmail para activar accesos menos seguros desde otras apps , según google

ACTIVAR LA CUENTA nombredelcorreodegmail@gmail.com en → * [link](https://myaccount.google.com/lesssecureapps)

Ahora seria conveniente realizar la creacion de Self-Auto-signed-CA

Podeis seguir este post:

[post](https://medium.com/@Ruben.znet/crear-ssl-certificates-auto-self-signed-c54feb074621)

centos7

[ssl](https://www.server-world.info/en/note?os=CentOS_7&p=ssl)

centos8

[ssl](https://www.server-world.info/en/note?os=CentOS_8&p=ssl)

Una vez creado , acordarse de que coincida ruta , con la del fichero /etc/postfix/main.cf

linea al final del fichero main.cf

![x](https://miro.medium.com/max/368/0*okGrpZneODeX1uL2)

prueba de funcionamiento:

```
echo “Test mail from postfix” | mail -s “Test Postfix” otrocorreooelmismocorreoparaprobar@gmailohotmailoloquequieras.com
```

FUENTE(S)

* [smtp_authentication](https://documentation.wazuh.com/3.0/user-manual/manager/manual-email-report/smtp_authentication.html)
* [configure-postfix-with-gmail-smtp](https://restorebin.com/configure-postfix-smtp-relay/#configure-postfix-with-gmail-smtp)
* [video1](https://www.youtube.com/watch?v=5q44aoZQQIg)
* [video2](https://www.youtube.com/watch?v=EPvVoSP7fMc)

-----------------------------------------------------------------------------

ZipyintheNet¡ 2020!®