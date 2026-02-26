# Search API

La Search API permite obtener documentos (resultados) de un proyecto de Talkwalker, filtrados por topics, filtros personalizados y query syntax.

## Endpoint principal

```
GET https://api.talkwalker.com/api/v1/search/p/<project_id>/results?access_token=<access_token>
```

## Parámetros principales

| Parámetro | Descripción | Requerido | Por defecto |
|-----------|-------------|-----------|-------------|
| `access_token` | Token de API | Sí | — |
| `topic` | Uno o más IDs de topic del proyecto | No (múltiple) | — |
| `filter` | Uno o más IDs de filtro personalizado | No (múltiple) | — |
| `q` | Query de búsqueda (sintaxis Talkwalker) | No | — |
| `offset` | Resultados a saltar (paginación) | No | 0 |
| `hpp` | Resultados por página (máx. 500) | No | 10 |
| `sort_by` | Criterio de ordenación | No | engagement |
| `sort_order` | Orden: `asc` o `desc` | No | desc |
| `time_range` | Rango temporal (ej. `30d`, `7d`) | No | — |
| `timezone` | Zona horaria | No | UTC |
| `hl` | Resaltado en snippets | No | true |
| `summarize` | Activar AI Summaries (requiere hpp ≥ 100) | No | off |
| `channel` | IDs de canales | No (múltiple) | — |
| `panel` | IDs de panels | No (múltiple) | — |
| `dataset` | IDs de datasets (Customer Intelligence) | No (múltiple) | — |

Restricción: `hpp + offset` no puede superar **10.000**.

Unidades para `time_range`: `s`, `m`, `h`, `d`, `w`, `M` (meses).

## Listar proyectos

```
GET https://api.talkwalker.com/api/v1/search/info?access_token=<access_token>
```

No consume créditos. Devuelve la lista de proyectos accesibles con tu token.

## Ejemplo: búsqueda por topic

```bash
curl -L -X GET 'https://api.talkwalker.com/api/v1/search/p/<project_id>/results?topic=<topic_id>&access_token=<token>'
```

## Ejemplo: paginación y orden por fecha

```bash
curl -L -X GET 'https://api.talkwalker.com/api/v1/search/p/<project_id>/results?topic=<topic_id>&hpp=100&offset=0&sort_by=published&sort_order=desc&access_token=<token>'
```

## Ejemplo: filtrar por sentimiento negativo

```bash
curl -L -X GET 'https://api.talkwalker.com/api/v1/search/p/<project_id>/results?q=sentiment:NEGATIVE&topic=<topic_id>&access_token=<token>'
```

## Respuesta

Incluye `pagination` (p. ej. `next`, `total`) y `result_content.data` con los documentos. Cada documento tiene campos como `url`, `title`, `content`, `published`, `sentiment`, `engagement`, `matched_profile`, etc.

## Créditos y límites

- **Créditos**: 1 por resultado devuelto, mínimo 10 por llamada.
- **Rate limit**: 60 llamadas/minuto dentro de proyecto; 240/minuto en quicksearch (sin proyecto).

## AI Summaries

Con `summarize=on` y `hpp` ≥ 100 (máx. 500) se incluye un resumen por página. Coste: 20 créditos por resumen + 1 por resultado.

## Notebook

Abre **02_buscar_datos** en Colab para probar búsquedas, paginación y query syntax.
