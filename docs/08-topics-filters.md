# Topics, Filters y Custom Tags

## Topics API

En Talkwalker, un **topic** es una consulta de búsqueda cuyos resultados se indexan en el proyecto. Tiene consultas de inclusión y/o exclusión, con varias líneas (OR entre líneas). Los topics pueden agruparse en categorías.

### Limitaciones

- No se puede renombrar un topic; hay que eliminarlo y crear uno nuevo (nuevo ID).
- No se puede cambiar la categoría de un topic; hay que eliminarlo y crearlo en otra categoría.
- Cada línea de query no puede superar **4096 caracteres**.

### Custom filters

Los **filters** tienen la misma estructura que los topics pero se usan para filtrar resultados bajo demanda sobre varios topics. La misma API sirve para ambos; el parámetro `type` distingue: `search` (topic) o `filter`.

---

## Listar topics y filtros

Recursos del proyecto (topics y filters):

```
GET https://api.talkwalker.com/api/v2/talkwalker/p/<project_id>/resources?type=search,filter&access_token=<access_token>
```

Devuelve la estructura de categorías y nodos con `id` y `title` de cada topic/filter.

---

## Crear topic

```
POST https://api.talkwalker.com/api/v2/talkwalker/p/<project_id>/topics/import?access_token=<access_token>
Content-Type: application/json
```

Cuerpo para topic en categoría "ungrouped" (`category_id: "default"`):

```json
{
  "topic_type": "search",
  "topic_line_import": [
    {
      "topic_title": "Mi nuevo topic",
      "topic_description": "Descripción",
      "category_id": "default",
      "override": false,
      "query": "cats AND dogs AND lang:en",
      "included_query": true
    }
  ]
}
```

- `included_query: true` → línea de inclusión; `false` → exclusión.
- Para crear en un **grupo existente**, usa su `category_id`.
- Para crear en un **grupo nuevo**, quita `category_id` y añade `category_title`.

Puedes enviar varios elementos en `topic_line_import` en una sola llamada.

---

## Añadir línea a un topic existente

En el mismo endpoint de import, usa `override: false` y el `category_id` y topic existentes; equivale a "New Line" en la UI.

---

## Actualizar query de un topic

No se puede cambiar solo una línea; hay que enviar todas las líneas del topic en `topic_line_import` con `override: true` (o según documentación de import).

---

## Eliminar topic

Se requiere el par `categoryid` y `topicid` (endpoint de delete según documentación oficial).

---

## Custom Tags API

### Listar tags del proyecto

```
GET https://api.talkwalker.com/api/v2/talkwalker/p/<project_id>/tags?access_token=<access_token>
```

### Gestionar tags en documentos

Para añadir o quitar tags en un documento se usan los campos correspondientes en la **Docs API** (update/upsert), por ejemplo `tags_marking`, `tags_customer` o los IDs de tag del proyecto. La referencia exacta de campos está en la documentación de [Talkwalker Documents](https://developer.talkwalker.com/docs/talkwalker-documents/fields).

## Notebooks

- **07_gestionar_topics**: crear, actualizar y eliminar topics (y filters).
- **08_custom_tags**: listar tags y gestionar tags en documentos.
