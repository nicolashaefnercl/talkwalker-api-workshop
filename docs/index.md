# Workshop Talkwalker API

Bienvenido al workshop de la **API de Talkwalker**. Este material está pensado para desarrolladores que quieran integrar o automatizar flujos con Talkwalker de forma práctica y auto-guiada.

## ¿Qué incluye este workshop?

1. **Documentación en Markdown** (esta web): teoría simplificada, referencias rápidas y ejemplos por endpoint.
2. **Notebooks ejecutables en Google Colab**: código listo para probar cada funcionalidad; solo hace falta configurar credenciales y ejecutar celdas.

## Cómo usarlo

- **Si prefieres leer primero**: navega por los apartados *Empezar* y *Referencia API* en el menú.
- **Si prefieres probar en vivo**: abre los notebooks desde el [README del repositorio](https://github.com/your-org/talkwalker-api-workshop) con los enlaces *Open in Colab*.
- **Token demo**: para Search API y Streaming API puedes usar `access_token=demo` con las queries `cats`, `dogs` o `cats AND dogs` (solo blogs, foros y noticias; sin redes sociales).
- **Token propio**: para usar tus proyectos, importar documentos, gestionar topics o tags necesitas un token con permisos `read_write`. Contacta a Talkwalker para obtenerlo.

## Estructura del workshop

| Módulo | Documentación | Notebook Colab |
|--------|---------------|-----------------|
| Setup y credenciales | [Getting Started](01-getting-started.md) | 00_setup_y_credenciales |
| Explorar proyecto | — | 01_explorar_proyecto |
| Buscar datos | [Search API](03-search-api.md) | 02_buscar_datos |
| Métricas agregadas | [Histogram API](04-histogram-api.md) | 03_metricas_agregadas |
| Importar documentos | [Upload Documents](05-upload-documents.md) | 04_importar_documentos |
| Streaming | [Streaming API](06-streaming-api.md) | 05_streaming |
| Export tasks | [Export Task API](07-export-task-api.md) | 06_export_tasks |
| Topics y filters | [Topics, Filters y Tags](08-topics-filters.md) | 07_gestionar_topics, 08_custom_tags |
| Image API | [Image API](09-image-api.md) | 09_image_api |

## Enlaces útiles

- [Portal oficial Talkwalker Developer](https://developer.talkwalker.com/)
- [Restricciones por fuente de datos](api-restrictions.md)
- [Glosario de términos](glossary.md)
