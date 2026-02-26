# Workshop Talkwalker API

Documentación práctica y notebooks ejecutables para la **API de Talkwalker**. Pensado para desarrolladores que quieran integrar o automatizar flujos con Talkwalker de forma auto-guiada.

## Contenido

- **Documentación**: en la carpeta `docs/` (Markdown). Puedes leerla en GitHub o generar un sitio con [MkDocs Material](#desplegar-documentación-con-mkdocs).
- **Notebooks**: en `notebooks/`. Ejecuta cada uno en **Google Colab** con un clic (usa los enlaces "Open in Colab" más abajo).

## Cómo usar

1. **Token demo**: para probar Search API y Streaming API sin credenciales, usa `access_token=demo` con las queries `cats`, `dogs` o `cats AND dogs` (solo blogs/foros/noticias).
2. **Token propio**: para tus proyectos, importar documentos, topics o tags necesitas un token **read_write**. Contacta a Talkwalker para obtenerlo.
3. Abre cualquier notebook en Colab, rellena las celdas de configuración (token, project_id, etc.) y ejecuta las celdas en orden.

## Notebooks (Open in Colab)

Sustituye `nicolashaefnercl/talkwalker-api-workshop` por la ruta real de tu repositorio en GitHub para que los enlaces a Colab funcionen.

| Módulo | Descripción | Abrir en Colab |
|--------|-------------|----------------|
| 00 - Setup y credenciales | Verificar token, créditos, listar proyectos | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/00_setup_y_credenciales.ipynb) |
| 01 - Explorar proyecto | Resources API: topics, filtros, channels, tags | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/01_explorar_proyecto.ipynb) |
| 02 - Buscar datos | Search API, query syntax, paginación | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/02_buscar_datos.ipynb) |
| 03 - Métricas agregadas | Histogram API (widgets) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/03_metricas_agregadas.ipynb) |
| 04 - Importar documentos | Docs API: create, update, batch | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/04_importar_documentos.ipynb) |
| 05 - Streaming | Streams por keywords y por proyecto | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/05_streaming.ipynb) |
| 06 - Export tasks | Export Task API asíncrono | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/06_export_tasks.ipynb) |
| 07 - Gestionar topics | Topics API: crear/actualizar topics | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/07_gestionar_topics.ipynb) |
| 08 - Custom tags | Gestionar tags en documentos | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/08_custom_tags.ipynb) |
| 09 - Image API | Detección de logos, objetos y escenas | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nicolashaefnercl/talkwalker-api-workshop/blob/main/notebooks/09_image_api.ipynb) |

## Estructura del repositorio

```
talkwalker-api-workshop/
├── README.md
├── mkdocs.yml
├── docs/
│   ├── index.md
│   ├── 01-getting-started.md
│   ├── 02-query-syntax.md
│   ├── 03-search-api.md … 09-image-api.md
│   ├── api-restrictions.md
│   └── glossary.md
└── notebooks/
    ├── 00_setup_y_credenciales.ipynb
    ├── 01_explorar_proyecto.ipynb
    └── … 09_image_api.ipynb
```

## Desplegar documentación con MkDocs

Para generar un sitio web a partir de `docs/`:

```bash
pip install mkdocs-material
mkdocs serve
```

Abre `http://127.0.0.1:8000`. Para publicar en **GitHub Pages**:

```bash
mkdocs gh-deploy
```

(Configura `mkdocs.yml` con tu `repo_url` antes.)

## Pasos recomendados para publicar

¿Primera vez publicando este workshop? Sigue la guía paso a paso en **[PASOS_RECOMENDADOS.md](PASOS_RECOMENDADOS.md)** para:

1. Reemplazar la URL del repo en README y `mkdocs.yml`
2. Subir el contenido a GitHub
3. Comprobar los enlaces "Open in Colab"
4. (Opcional) Publicar la documentación con MkDocs en GitHub Pages

## Referencias

- [Talkwalker Developer Portal](https://developer.talkwalker.com/)
- Documentación local: carpeta `docs/` o el sitio generado con MkDocs.
