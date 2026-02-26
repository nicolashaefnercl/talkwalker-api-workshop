# Histogram API

La Histogram API permite reproducir en tus propios dashboards los widgets de Talkwalker: resultados en el tiempo, métricas de rendimiento, sentimiento, temas, demografía y mapa mundial.

## Coste y límites

- **Créditos**: 10 por llamada.
- **Rate limit**: 30 llamadas/minuto dentro de proyecto; 60/minuto fuera.

## Uso típico

Los histogramas se solicitan con parámetros que dependen del tipo de widget que quieras reproducir. La base es un proyecto y, opcionalmente, topics/filtros y rango temporal.

## Mapeo widget → API

| Sección en Talkwalker | Tipo de histograma | Uso |
|------------------------|---------------------|-----|
| Resultados | Resultados en el tiempo | Métricas a lo largo del tiempo |
| Performance | Mentions, engagement, reach | Métricas agregadas |
| Influencers | Unique authors | Autores únicos |
| Sentimientos | Share of sentiments | Distribución de sentimiento |
| Temas | Top themes | Temas principales |
| Demografía | Gender, etc. | Desglose demográfico |
| Mapa mundial | Distribución geográfica | Resultados por ubicación |
| Visual insights | Indoor/Outdoor | Detección en imágenes |

La documentación oficial detalla el endpoint exacto y los parámetros por tipo (resultados, performance, influencers, sentiment, themes, demographics, world map, visual insights). Algunos widgets no son reproducibles vía API.

## Restricciones por fuente

- **Facebook/Instagram**: no se exportan documentos; solo métricas agregadas vía Histogram.
- **TikTok/Reddit**: solo datos agregados (Histogram), no raw.
- **Twitter**: campos limitados; rehidratación vía Twitter API si necesitas detalle.

## Notebook

Abre **03_metricas_agregadas** en Colab para ejemplos de llamadas a la Histogram API según el tipo de widget.
