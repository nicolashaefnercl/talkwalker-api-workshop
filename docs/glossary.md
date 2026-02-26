# Glosario

Términos usados en la documentación del workshop y en la API de Talkwalker.

| Término | Descripción |
|---------|-------------|
| **Access token** | Clave de autenticación para las llamadas a la API. Puede ser `read_only` o `read_write`. |
| **Collector** | Cola persistente donde se almacenan resultados (p. ej. de un stream o de un export task). Los datos permanecen 7 días. |
| **Credit** | Unidad de consumo de la API. Se consumen según el tipo de llamada y los resultados devueltos. |
| **Document** | Unidad de contenido indexada en Talkwalker (post, artículo, comentario, etc.). Tiene URL, título, contenido, metadatos y métricas. |
| **Export task** | Tarea asíncrona que copia un conjunto de datos históricos a un collector. |
| **Filter** | Filtro personalizado del proyecto; misma estructura que un topic pero usado para filtrar resultados bajo demanda. |
| **Histogram API** | API que devuelve métricas agregadas (resultados en el tiempo, sentimiento, temas, demografía, etc.) para reproducir widgets. |
| **Project** | Contenedor en Talkwalker con topics, filtros, canales y documentos. El `project_id` identifica el proyecto en la API. |
| **Query** | Expresión de búsqueda en la sintaxis Talkwalker (keywords, operadores, filtros por campo). |
| **Rehydration** | Proceso de recuperar el contenido completo de un tweet desde la Twitter API usando el tweet ID obtenido de Talkwalker. |
| **Resource** | Recurso configurado en un proyecto: topic, filter, channel, panel, event, etc. Se listan con la Resources API. |
| **Search API** | API para obtener documentos (resultados) de un proyecto con filtros y paginación. |
| **Source type** | Tipo de fuente del documento (p. ej. BLOG, SOCIALMEDIA_TWITTER, OTHER, ONLINENEWS). |
| **Stream** | Canal en tiempo real por el que Talkwalker envía documentos que coinciden con reglas (keywords) o con un proyecto. |
| **Topic** | Regla de búsqueda del proyecto cuyos resultados se indexan. Tiene líneas de inclusión y/o exclusión. |
| **Token demo** | Token de prueba (`access_token=demo`) con queries limitadas (cats, dogs, cats AND dogs) y sin redes sociales. |
