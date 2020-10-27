---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## crear-ssl-certificates-auto-self-signed

En la Siguiente Guía vamos a crear certificado(s) , auto firmados.

No es lo mas conveniente, ya que esto lo vamos a realizar , para después utilizar estos certificados en servicios que vamos a instalar en un servidor que solamente esta pensado para funcionar y dar cara ‘LOCALMENTE’ , y no estar expuesto nunca a INTERNET (ip publica.)

Cabe destacar que en caso de querer por ejemplo.. dar cara a Internet con un servidor WEB , vamos a necesitar que nuestra CA , (nuestro certificado) , sea firmado por otra CA superior , para que se confié en nuestro CA , ya que una vez firmado nuestra CA , por la CA superior. Muchos navegadores web u otros servicios que no sean web , confiaran en nuestra CA.. Pero para esto necesitamos o pagar por ejemplo.. en comodo? O podemos utilizar LETS ENCRYPT….pero… este no es el caso….

Nosotros como repito estamos creando CA (autoridad certificadora)para utilizarlas localmente. ¿utilizarlas localmente , estas loco?

-No , algunas veces , hay configuraciones que requieren de certificaciones para que puedan correr bien sin problemas ya que algunos servicios están pensados para dar cara a internet.. Y en caso de no poner Certificaciones , podemos tener problemas con el servicio o el sistema a la hora de configurar lo y hacer que funcione… Por ejemplo postfix , en caso de querer hacer relay , se necesita CA para comunicarnos con 2º o 3º servidores de internet. De forma que ….

Para crear certificados , vamos a realizar lo siguiente:

Yo me baso en una VM,MV(VirtualMachine o MaquinaVirtual) , que tiene instalado Centos7 , y si debería utilizar Centos8.. lo se … o no se… todavía le queda vida a Centos7.. ok….

Os dejo antes 2 links por si acaso… tenéis que echarle un vistazo a la fuente consultada

[centos7](https://www.server-world.info/en/note?os=CentOS_7&p=ssl)

[centos8](https://www.server-world.info/en/note?os=CentOS_8&p=ssl)

Bueno dicho esto vamos a lo GORDO:

Realmente es fácil

Yo realmente lo realizaría todo con sudo… Pero ya sabéis que root no es de fiar ni de utilizar por si se caga y se jode realmente el sistema con algún cambio. Aun asi soy valiente y lo realizo.. No lo hagáis así, utilizar sudo , creerme que os ahorrara problemas y os creara al principio dolores de cabeza pero…. es mejor.

Vamos al directorio (en /etc/ssl/… ) tenéis también el directorio , si no me equivoco ahora mismo mientras redacto esto creo recordar que /etc/pki , monta un enlace simbólico a /etc/ssl….

![x](https://miro.medium.com/max/430/0*3KcqQ7ny4Tpcn8Qq)

Vale , una vez estamos en el directorio procedemos a crear la CA propia (Auto-self , auto firmada)

como veis con ‘make nombre.key’ , vamos a crear la llave de la CA

![x](https://miro.medium.com/max/696/0*x6Gwbsbubb90a2q4)

Si no queremos que la key tenga ‘password’ , se puede quitar el password y si no OMITE este paso (step)

![x](https://miro.medium.com/max/693/0*kXF1oTKiGKCwekOn)

Aquí viene un poco lo gordo:

La idea es que vamos a crear nuestro ‘csr’ , para ello con el command comando(suena mejor en ingles) ‘make’ seguido de ‘nombre.csr’ en nombre pondremos lógicamente nuestro nombre , de todas formas todo lo dejo con capturas para que te fijes que no soy tan tonto de ponerlo con comillas , las comillas son modo ejemplo y esas cosas tan bonitas que tienen las guías para explicar cosas…

Faltaría comentar que vamos a tener una bonita sección donde añadir countryname..etc unos datos….

![x](https://miro.medium.com/max/700/0*17s2vVD9MRblUddf)

Cuando hayamos acabado , tendremos el fichero CSR

Para seguir y llegar a conseguir la CA , recuerdo que actualmente tenemos , CSR y KEY
Pues vamos a realizar la magia con openssl y firmamos nuestra CA que vamos a crear , con los días que queremos que sea valida nuestra CA… etc , yo os recomiendo que como todo esto es local y para no dar por saco renovando si la queréis para siempre , truco : 50años x 365 dias = X nº de días , calcularlo vosotros , y así tenéis una CA valida para 50 años… , os va a caducar algún día ? Puede sonar fuerte , pero a lo mejor en 50 años , ya no estamos ni por estos maravillosos mundos de los bits…

![x](https://miro.medium.com/max/700/0*J9DfkTBkTJ19xvEf)

Por ultimo queridos amigos , tenemos una CA creada y la podemos listar en el directorio donde estamos…

![x](https://miro.medium.com/max/700/0*nEdyB5SVHi5mCg46)

Acuérdate que por /etc/ssl… había un enlace simbólico o al revés y que vas a poder tener también allí la CA … la CA es el fichero que acaba en ‘crt’ y no ‘csr’

Si queréis utilizarla , utilizar por ejemplo la ruta absoluta donde se encuentra ubicada….

Bueno como estamos en verano y esto lo hago un 26 de Julio , os deseo feliz verano y que vuestra CA , os autorice para lo que narices autorice , perdonar por las palabras pero… realmente una CA local , que esta autorizando ¿? XDDD

Como os he dicho la utilizamos para lo que he explicado y no lo vuelvo a repetir… leete el post otra vez si no lo has entendido…. o a lo mejor explícamelo y así sabre quizás el por que no lo sabia?

Salu2

-----------------------------------------------------------------------------

ZipyintheNet¡ 2020!®