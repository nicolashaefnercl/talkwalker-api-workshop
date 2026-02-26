# Upload Documents (Docs API)

La API de documentos permite crear, actualizar, eliminar y recuperar documentos en un proyecto de Talkwalker. Es útil para importar contenido propio (blogs, foros, reseñas, etc.). **No se pueden importar documentos de redes sociales**.

## Requisitos

- Proyecto con tipo de fuente **OTHER** habilitado (media type "unclassified" en ajustes del proyecto).
- El documento debe coincidir con al menos una regla/topic del proyecto.
- Token con permisos **read_write**.

## Endpoints principales

Base: `https://api.talkwalker.com/api/v2/docs/p/<project_id>`

| Operación | Método | Endpoint |
|-----------|--------|----------|
| Crear | POST | `.../create?access_token=<token>` |
| Actualizar | POST | `.../update?access_token=<token>` |
| Upsert | POST | `.../upsert?access_token=<token>` |
| Eliminar | POST | `.../delete?access_token=<token>` |
| Restaurar | POST | `.../undelete?access_token=<token>` |
| Batch (varias operaciones) | POST | `...?access_token=<token>` (body: array de objetos create/update/delete) |

## Campos obligatorios para crear

| Campo | Descripción |
|-------|-------------|
| `url` | Identificador único del documento. Debe coincidir con un canal/dominio del proyecto. No se puede cambiar después. |
| `published` | Fecha de publicación (epoch en milisegundos). |
| `title` | Título (opcional pero recomendado). |
| `content` | Contenido del documento. |

## Ejemplo: crear un documento

```bash
curl -X POST 'https://api.talkwalker.com/api/v2/docs/p/<project_id>/create?access_token=<token>' \
  -H 'Content-Type: application/json' \
  -d '{
    "url": "https://www.ejemplo.com/articulo-1",
    "title": "Título del artículo",
    "content": "Contenido del artículo.",
    "published": "1625398761000",
    "extra_author_attributes": { "name": "Autor", "gender": "MALE" }
  }'
```

## Ejemplo: actualizar (p. ej. añadir métricas)

En `update` envías la misma `url` y los campos a modificar. Para arrays puedes usar `+tags_marking` / `-tags_marking` para añadir o quitar elementos.

## Ejemplo: batch (varios documentos)

```json
[
  { "create": { "url": "...", "title": "...", "content": "...", "published": "..." } },
  { "update": { "url": "...", "title": "Nuevo título" } },
  { "delete": { "url": "..." } }
]
```

## Custom fields

Si el proyecto tiene campos personalizados (Project Settings → Custom Metrics), puedes enviarlos en el objeto `custom`:

```json
"custom": { "text_1": "Valor texto", "double_1": 0.75 }
```

## Créditos y límites

- **Créditos**: No se consumen por crear/actualizar/eliminar documentos.
- **Rate limit**: 120 llamadas por minuto.

## Flujo CREATE + UPDATE para source_type

Un patrón habitual es: crear el documento con `source_type: "OTHER"` y luego actualizarlo a `source_type: "SOCIALMEDIA_TIKTOK"` (u otro) para que aparezca en la categoría correcta en la UI. Ver notebook **04_importar_documentos**.

## Notebook

Abre **04_importar_documentos** en Colab para CRUD, batch y custom fields.
