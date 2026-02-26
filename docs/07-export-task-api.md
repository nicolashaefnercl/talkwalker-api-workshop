# Export Task API

La Export Task API permite crear tareas **asíncronas** que copian un conjunto de datos históricos a un **collector**, desde el cual luego puedes leer los resultados.

## Conceptos

- **Export task**: trabajo en segundo plano que filtra datos por proyecto, stream o query y los escribe en un collector.
- **Collector**: cola persistente donde se vuelcan los resultados. Los datos permanecen **7 días**.

## Parámetros comunes (cuerpo de la petición)

| Parámetro | Descripción | Requerido |
|-----------|-------------|-----------|
| `start` | Inicio del rango (timestamp ms o fecha `YYYY-MM-DD`) | Sí |
| `stop` | Fin del rango (día excluido) | No |
| `target` | ID del collector de destino | Sí |
| `query` | Query adicional (AND con el contexto) | No |
| `limit` | Máximo de resultados a exportar | No (default 1.000.000) |

Cada resultado exportado consume **1 crédito**. Máximo **1.000.000** resultados por tarea.

---

## Crear collector vacío

Para recibir los resultados del export necesitas un collector sin reglas:

```
PUT https://api.talkwalker.com/api/v3/stream/c/<collector_id>?access_token=<access_token>
Content-Type: application/json

{}
```

---

## Los tres tipos de export

### 1. Export desde proyecto

```
POST https://api.talkwalker.com/api/v3/stream/p/<project_id>/export?access_token=<access_token>
```

Cuerpo ejemplo:

```json
{
  "start": "2022-04-01",
  "stop": "2022-05-01",
  "target": "<collector_id>",
  "query": "domainurl:reddit.com OR sourcetype:SOCIALMEDIA_TWITTER",
  "topics": ["<topic_id>"]
}
```

### 2. Export desde stream existente

```
POST https://api.talkwalker.com/api/v3/stream/s/<stream_id>/export?access_token=<access_token>
```

### 3. Export solo por query

```
POST https://api.talkwalker.com/api/v3/stream/export?access_token=<access_token>
```

---

## Consultar estado de la tarea

```
GET https://api.talkwalker.com/api/v3/tasks/export/<task_id>?access_token=<access_token>
```

Estados posibles: `UNKNOWN`, `QUEUED`, `RUNNING`, `FINISHED`, `FAILED`, `DELETED`, `ABORTED`, `RESULT_LIMIT_REACHED`. El campo `processed` indica cuántos documentos se han exportado; `progress` el avance (1 = 100%).

---

## Leer resultados del collector

Cuando la tarea esté `FINISHED` (o mientras escribe), lee el collector:

```
GET https://api.talkwalker.com/api/v3/stream/c/<collector_id>/results?access_token=<access_token>&resume_offset=earliest&end_behaviour=stop
```

`end_behaviour=stop` cierra la conexión al llegar al final. `resume_offset=earliest` empieza desde el principio.

---

## Listar y abortar tareas

Listar tareas recientes:

```
GET https://api.talkwalker.com/api/v3/tasks/export?access_token=<access_token>
```

Abortar una tarea en curso:

```
DELETE https://api.talkwalker.com/api/v3/tasks/export/<task_id>?access_token=<access_token>
```

## Buenas prácticas

Para rangos largos, conviene dividir en varias tareas (p. ej. un mes por tarea) para controlar créditos y volumen.

## Notebook

Abre **06_export_tasks** en Colab para crear collector, lanzar export, consultar estado y leer resultados.
