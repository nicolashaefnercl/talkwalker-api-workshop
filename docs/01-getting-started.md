# Getting Started

Esta guía cubre los conceptos básicos para usar la API de Talkwalker: tokens, créditos y restricciones.

## Access Token

### Token demo

Para probar la API sin credenciales propias puedes usar el token de demostración:

```
access_token=demo
```

Con este token puedes usar:

- **Search API** (resultados e histograma)
- **Streaming API**

Limitaciones del token demo:

- Solo acepta estas queries predefinidas: `cats`, `dogs`, `cats AND dogs`.
- No devuelve resultados de redes sociales; solo de blogs, foros y noticias.
- Es solo para pruebas.

### Token propio

Para usar la API con los topics de tu proyecto de Talkwalker o para obtener resultados de redes sociales necesitas un **token propio**.

| Tipo de token | Uso |
|---------------|-----|
| `read_only` | Búsquedas (Search API, Histogram, Streaming en solo lectura). |
| `read_write` | Búsquedas + actualizar/eliminar documentos, crear/eliminar streams, configurar panels y reglas. |

Para obtener un token propio debes contactar a Talkwalker.

---

## Créditos y precios

Los créditos se consumen según el tipo de llamada y los resultados exportados.

| API | Coste en créditos |
|-----|-------------------|
| Histogram API | 10 créditos por llamada |
| Stream API | 1 crédito por resultado |
| Search API | 1 crédito por resultado + mínimo 10 créditos por llamada |

La **importación de documentos** no consume créditos.

### Reinicio mensual

Los créditos se reinician cada mes el día de la suscripción a las **03:00 UTC**.

### Consultar créditos restantes

Endpoint:

```
GET https://api.talkwalker.com/api/v1/status/credits?access_token=<access_token>
```

Respuesta (ejemplo):

```json
{
  "status_code": "0",
  "status_message": "OK",
  "result_creditinfo": {
    "used_credits_monthly": 0,
    "remaining_credits_monthly": 5000,
    "next_billing_period": 1748556000000,
    "monthly_total": 5000
  }
}
```

Este endpoint está limitado a **10 llamadas por minuto**; conviene cachear el resultado.

---

## Rate limits

| Endpoint / API | Límite |
|----------------|--------|
| Search API (dentro de proyecto) | 60 llamadas/minuto |
| Search API (fuera de proyecto, quicksearch) | 240 llamadas/minuto |
| Histogram API (dentro de proyecto) | 30 llamadas/minuto |
| Histogram API (fuera de proyecto) | 60 llamadas/minuto |
| Status credits | 10 llamadas/minuto |
| Docs API (create/update/delete) | 120 llamadas/minuto |
| Resources API | 20 llamadas/minuto |
| Tags API | 40 llamadas/minuto |

---

## Listar proyectos accesibles

Para obtener los proyectos vinculados a tu token:

```
GET https://api.talkwalker.com/api/v1/search/info?access_token=<access_token>
```

No consume créditos. Límite: 10 llamadas/minuto.

---

## Próximos pasos

- Revisar [Query Syntax](02-query-syntax.md) para construir búsquedas.
- Consultar [Restricciones API](api-restrictions.md) por fuente de datos.
- Abrir el notebook **00_setup_y_credenciales** en Colab para verificar token, créditos y proyectos.
