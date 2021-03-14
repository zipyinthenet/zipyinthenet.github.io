---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## ubuntu-bash-w10

Buenas !

En esta segunda parte vengo para traer 2 tipos de multiplexadores para linux , en este caso para nuestro Ubuntu Bash en W10 por WSL windows subsystem linux.

Actualmente los 2 multiplexadores que conozco y son los mas conocidos y los que mas utiles me han parecido despues de leer varios articulos son:

- TMUX
- Terminator linux multiplexador

Esta solucion de añadir los multiplexadores a nuestro Ubuntu Bash es una buenisima solucion para no tener que estar lidiando con mas ventanas , de tal forma que con abrir 1 solo terminal de Ubuntu Bash en w10 , podamos ejecutar por ejemplo tmux o terminator y con el terminal que se despliega poder abrir muchas sesiones y ventanas en diferentes hosts o el mismo hosts donde querramos trabajar , y con atajos de teclado muy rapidamente poder acceder a nuevas ventanas , estando todo el rato y tiempo en la misma ventana.

Es muy usado.

***
Terminator

Os dejo un  [articulo](https://medium.com/@bhupathy/install-terminator-on-windows-with-wsl-2826591d2156) , el cual habla sobre como INSTALAR Terminator en ubuntu BASH WSL en nuestro desktop de windows10.

Cabe destacar que terminador no funciona si no se instalan requisitos previos:
-Terminal ubuntu bash WSL instalar dbus-x11 y realizar sudo systemd-machine-id-setup
-Instalar en w10 X-server [link](https://sourceforge.net/projects/vcxsrv/)

Yo recomiendo probar terminator , pero para mi gusto tmux me ha gustado mas por los atajos de teclado y por que no hace falta instalar mas utilidades para el sistema de linux y tampoco tener que instalar utilidades en w10 como x-server. Tmux funciona una vez sea instalado en el terminal de ubuntu bash WSL en w10 sin ninguna utilidad simplemente instalamos tmux y corremos.

***
Tmux

[link-articulo-post-como-instalar-tmux](https://devblogs.microsoft.com/commandline/tmux-support-arrives-for-bash-on-ubuntu-on-windows/)

Instalar tmux , tan solo debemos llamar al programa desde herramienta apt-get 'apt-get install tmux' , no nos olvidemos de ejecutarlo con permisos de sudo o como root , mejor solo con permisos de sudo , por que root no es muy aconsejable hacer nada con este subsystem linux en windows.
![x](https://devblogs.microsoft.com/wp-content/uploads/sites/33/2019/02/1-install.png)


* * *
Y por ultimo , si os instalais esta utilidad en vuestro usuario con el que soleis trabajar en el terminal , vais a poder tener mas utilidades que se explican en el siguiente link

OH-MY-TMUX
[link-oh-my-tmux](https://github.com/gpakosz/.tmux)

![x](https://cloud.githubusercontent.com/assets/553208/19740585/85596a5a-9bbf-11e6-8aa1-7c8d9829c008.gif)

En el link referencial se explica todo , desde como instalar , hasta como usar algunos comandos.

De igual forma dejo un minitutorial:

OJO!!! , NO podemos usar esta utilidad si no tenemos antes INSTALADO TMUX , cuidado con esto , no es descargar la utilidad y probar como funcoine , esta utilidad esta hecha para cuando TENGAMOS INSTALADO TMUX , añadir nuevas FUNCIONALIDADES !!
```
$ cd
$ git clone https://github.com/gpakosz/.tmux.git
$ ln -s -f .tmux/.tmux.conf
$ cp .tmux/.tmux.conf.local .
```
Aqui dejo una pequeña chuleta:
```
CRTL +B  	
	prefix

CRTL +B   ,  
	RENAME VENTANA 	

CRTL +B  "(SHFT+2)
	VENTANA horizaontal

CRTL +B  %(SHFT+5)
	VENTANA vertical

CRTL +B  X
	Cerrar terminal

CRTL +B  espacio
	rotamos posiciones ventanas

CRTL +B  {(altgr+{)
	cambiar posicion ventana  en la que nos encontramos al lario contrario [ventana derecha pasa a la izquierda]

CRTL +B  }(altgr+})
	cambiar posicion ventana  en la que nos encontramos al lario contrario [ventana derecha pasa a la izquierda]

CRTL +B  O(crtl+o)
	rotar agujas

CRTL +B  c
	nueva sesion ventana

CRTL +B  1
	moverse sesion ventana anterior
CRTL +B  2
	moverse sesion ventana siguiente

CRTL +B M
	funcionalidad raton activar y desactivar

CTRL +B CTRL+derecha
	redimensionar estetica espacio paneles(ventanas de conexiones) manualmente
CTRL +B CTRL+izquierda
	redimensionar estetica espacio paneles(ventanas de conexiones) manualmente
CTRL +B CTRL+arriba
	redimensionar estetica espacio paneles(ventanas de conexiones) manualmente
CTRL +B CTRL+abajo
	redimensionar estetica espacio paneles(ventanas de conexiones) manualmente

CTRL +B shift+1
	lelvar panel ventana a nuueva sesion de ventana	

CTRL +B shift+:

CTRL +B altgr+[
	modo copia
CTRL +B altgr+]
	pegar lo seleccionado

CTRL +B S
	panel cosas abiertas
CTRL +B w
	panel cosas abiertas
```

Salu2

-----------------------------------------------------------------------------

ZipyintheNet¡ 2020!®
