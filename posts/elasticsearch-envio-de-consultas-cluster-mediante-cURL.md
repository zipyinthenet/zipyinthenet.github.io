---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## Elasticsearch - Envio de consultas cluster mediante cURL

```bash
curl -k -X GET -u usuario:password https://localhost:9200 

curl -k -X GET -u elastic:password https://localhost:9200 
```

```bash
curl -k -X GET -u elastic:password https://localhost:9200/_cluster/health?pretty

curl -k -X GET -u elastic:password https://localhost:9200/_cat/nodes?v

curl -k -X GET -u elastic:password https://localhost:9200/_cat/indices?v

curl -k -X GET -u elastic:password https://localhost:9200/_cat/indices?v\&expand_wildcards=all
```

[Link-rest-API](https://www.elastic.co/guide/en/elasticsearch/reference/current/rest-apis.html)

-----------------------------------------------------------------------------

ZipyintheNet¡
