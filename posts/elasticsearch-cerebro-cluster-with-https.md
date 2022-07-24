---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## Elasticsearch - cerebro in cluster elasticsearch with HTTPS

Links de docker hub y github sobre cerebro

[Link-github](https://github.com/yannart/docker-cerebro)

[Link-docker-hub](https://hub.docker.com/r/yannart/cerebro/)

Fichero docker-compose

[Link-fichero-docker-compose](https://github.com/yannart/docker-cerebro/blob/master/docker-compose.yml)

Hay que tener en cuenta que...

Como configurar HTTPS en cerebro:

Habra que entrar al contenedor , visualizar el fichero applitacion.conf , editarlo manualmente en un editor de texto como sublime , por ejemplo.

Una vez editado , copiarlo al contenedor mediante copy , y reiniciar el contenedor para que se apliquen cambios.

Tener en cuenta que , los siguientes links ayudan a configurar el fichero de cerebro de configuracion applitacion.conf , y a parte , debemos apuntar al contenedor MASTER del cluster de elastic.

Tambien tener en cuenta que habra que convertir a PEM , el certificado CA.

```bash
# A list of known hosts
hosts = [
  {
    host = "https://es01:9200"
    name = "docker-cluster"
    auth = {
      username = "elastic"
      password = "alumno"  
    }    
  }
  # Example of host with authentication
  #{
  #  host = "http://some-authenticated-host:9200"
  #  name = "Secured Cluster"
  #  auth = {
  #    username = "username"
  #    password = "secret-password"
  #  }
]
play.ws.ssl {
  trustManager = {
    stores = [
      { type = "PEM", path = "/opt/cerebro/ca.pem" }
    ]
  }
}     
play.ws.ssl.loose.acceptAnyCertificate=true
```

[AYUDA1-github-issues](https://github.com/lmenezes/cerebro/issues/385)

[AYUDA2-github-issues](https://github.com/lmenezes/cerebro/issues/473)

[AYUDA-docker-cp-command](https://docs.docker.com/engine/reference/commandline/cp/)


-----------------------------------------------------------------------------

ZipyintheNet¡
