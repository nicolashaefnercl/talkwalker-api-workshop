# Restricciones de la API

Resumen de limitaciones por fuente de datos y tipo de operación al usar la API de Talkwalker.

---

## Exportación (lectura de documentos)

### Facebook e Instagram

- **Contenido**: no se puede exportar contenido vía API ni por medios automatizados (políticas de la plataforma).
- **Métricas agregadas**: sí se pueden exportar mediante la **Histogram API**.

### X (Twitter)

- **Campos exportables**: solo sentimiento (calculado por Talkwalker), author ID y tweet ID.
- **Detalle completo**: hay que rehidratar los tweets con la **Twitter API v2** usando el tweet ID.
- **Límite**: X limita la exportación a **1,5M tweets/mes/cuenta**.
- **Add-on**: existe un add-on de Talkwalker que permite recibir contenido completo de tweets; consultar con CSM.

### Noticias online

- **Contenido completo**: no se exporta por políticas de copyright (TV Eyes, artículos de noticias).
- **Alternativa**: se devuelve contenido truncado; las palabras que coinciden con el topic aparecen resaltadas en el campo `content_snippet` (con etiquetas HTML `<b>`).

### Fuentes no exportables (raw)

- **TikTok**: no se exportan datos raw; solo métricas agregadas (Histogram).
- **Reddit**: igual, solo agregados.
- **LinkedIn**: no exportable.
- **WEIBO** y otras fuentes chinas.
- Artículos con restricción `WEB_NLA`.
- Algunos sitios de reviews según acuerdos con proveedores.
- `source_type`: `SOCIALMEDIA_DISQUS`, `MONITOREDSITE`.

---

## Importación (documentos)

- **No se pueden importar** documentos de redes sociales como si fueran de esa fuente.
- Sí se pueden importar documentos con `source_type: "OTHER"` (y luego actualizar a otro tipo si aplica, según el flujo de tu integración).

---

## Rate limits (resumen)

| API | Dentro de proyecto | Fuera de proyecto |
|-----|--------------------|-------------------|
| Search | 60 llamadas/min | 240 llamadas/min |
| Histogram | 30 llamadas/min | 60 llamadas/min |

Otros: Status credits 10/min; Docs 120/min; Resources 20/min; Tags 40/min.
