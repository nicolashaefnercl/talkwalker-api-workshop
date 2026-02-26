# Streaming API

La Streaming API permite recibir en tiempo real menciones y artículos que coinciden con reglas (keywords) o con un proyecto de Talkwalker.

## Dos modos de uso

1. **Por keywords**: streams definidos solo por reglas de búsqueda. Solo incluye contenido de la base global de Talkwalker (blogs, foros, noticias), **no redes sociales**.
2. **Por proyecto**: escuchas un proyecto (y opcionalmente topics/filtros). **Sí incluye redes sociales** indexadas en ese proyecto.

---

## Stream por keywords

### Crear o actualizar stream

```
PUT https://api.talkwalker.com/api/v3/stream/s/<stream_id>?access_token=<access_token>
Content-Type: application/json

{
  "rules": [
    { "rule_id": "rule_1", "query": "cats AND dogs" },
    { "rule_id": "rule_2", "query": "electric AND lang:en AND sentiment:negative" }
  ]
}
```

Si el `stream_id` ya existe, la petición sobrescribe las reglas. Los documentos que coincidan con **rule_1 OR rule_2** se envían al stream.

### Escuchar el stream

```
GET https://api.talkwalker.com/api/v3/stream/s/<stream_id>/results?access_token=<access_token>
```

La conexión permanece abierta; los resultados llegan en chunks (JSON lines o chunks con `chunk_type`: `CT_CONTROL`, `CT_RESULT`). Para limitar resultados o créditos usa `max_hits=<n>`.

Opcional: filtrar más con `q=<rule_extra>` para añadir una condición AND a las reglas del stream.

---

## Stream por proyecto

### Escuchar proyecto (tiempo real)

```
GET https://api.talkwalker.com/api/v3/stream/p/<project_id>/results?access_token=<access_token>
```

Opcional: limitar a topics/filtros con `topic=<topic_id>&topic=<topic_id2>&topic=<filter_id>`. Opcional: `q=<regla_extra>`, `max_hits=<n>`.

### Colector (persistencia)

Para no perder datos si no estás escuchando, puedes enviar el flujo a un **collector** (cola persistente, datos disponibles 7 días).

Crear/actualizar collector sobre un proyecto:

```
PUT https://api.talkwalker.com/api/v3/stream/c/<collector_id>?access_token=<access_token>
Content-Type: application/json

{
  "collector_query": {
    "queries": [ { "id": "rule_1", "query": "cats AND dogs" } ],
    "project_topics": { "project": "<project_id>", "topics": ["<topic_id>"] },
    "filters": ["<filter_id>"]
  }
}
```

Leer el collector como cola:

```
GET https://api.talkwalker.com/api/v3/stream/c/<collector_id>/results?access_token=<access_token>&resume_offset=earliest&end_behaviour=stop
```

---

## Créditos

- **Stream API**: 1 crédito por resultado entregado.

## Notebook

Abre **05_streaming** en Colab para crear streams por keywords, escuchar por proyecto y usar collectors.
