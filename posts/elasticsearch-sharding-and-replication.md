---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## Elasticsearch - Sharding && Replication

### Shards
Shards son indices en Lucene.

En Elasticsearch tenemos Indices.

Los Indices estan compuestos por Shards.

Dependiendo del numero de nodos que tengamos en el cluster de elasticsearch , de normal SIEMPRE tendremos 1 shard en cada nodo.

En caso de existir 1 solo nodo , 1 solo shard.

### Replication
Shards se pueden replicar , pero esto solo se puede realizar como minimo con mas de uno nodo (2 nodos minimo).

De forma que en un nodo tengamos 1 primary Shard , y en el secundario 1 replica shard.

NODO A
    - primary shard
NODO B
    - replica shard

La replica de Shards en elasticsearch , tambien sirve para aumentar el rendimiento del cluster en cuanto a busquedas. Ya que cada replica de shard , es una copia identica del shard primary , por tanto podriamos tener varios indices con varias consultas ejecutandose en cada uno de ellos.
Tambien hay que contar con varios factores mas , el hardware del nodo , y los recursos que tenga el nodo.

Para ver indices:

```bash
GET _cat/indices?v
```

Para ver estado cluster:

```bash
GET _cluster/health?pretty
```

Para ver shards y su estado:

```bash
GET _cat/shards?v
```

La columna 'prirep':
    - r = replica shard
    - p = primary shard

La columna 'node':
    - Podras ver en que nodo esta el shard.

La columna 'state':
    - STARTED = el shard ha comenzado
    - UNNASIGNED = el shard no esta asignado a ningun nodo
    - RELOCATING = el shard es relocalizado
    - INITIALIZING = el shard se esta recuperando de un compañero/nodo

[link-state-shards](https://www.elastic.co/guide/en/elasticsearch/reference/current/cat-shards.html)

-----------------------------------------------------------------------------

ZipyintheNet¡
