# Query Syntax (cheatsheet)

La API de Talkwalker usa una sintaxis de consulta para filtrar documentos. Una query puede tener hasta **50 operandos** y **4096 caracteres**. Las búsquedas son **insensibles a acentos y mayúsculas** (p. ej. `éléVE` coincide con "eleve"). No hay stemming (p. ej. "children" no coincide con "child"). Se pueden usar caracteres no latinos y emojis.

---

## Operadores booleanos

| Operador | Descripción | Ejemplo |
|----------|-------------|---------|
| `AND` | Ambos términos deben aparecer | `BMW AND bike` |
| `OR` | Al menos uno de los términos | `BMW OR bike` |
| `AND NOT` | Excluir un término | `BMW AND NOT bike` |
| `NOT` | Filtro negativo | `NOT coupons` |
| `""` | Frase exacta (orden respetado) | `"BMW series"` |
| `()` | Agrupar términos | `BMW AND (motorcycle OR car)` |
| `*` | Comodín (0 o más caracteres, solo al final) | `Luxemb*` |
| `?` | Un carácter | `reali?ation` |
| `~` (proximidad) | Frase entre comillas + distancia en palabras | `"obama merkel"~5` |
| `~X` (fuzzy) | Palabra similar (X = 0, 1 o 2 caracteres cambiados) | `roam~1` |
| `"..."~` (fuzzy frase) | Variantes con guión/espacio | `"car sharing"~` |
| `+` | Cadena exacta (case insensitive) | `+"l'oréal"` |
| `++` | Cadena exacta (case sensitive) | `++"L'Oréal"` |
| `NEAR/x` | Términos cerca (x = distancia, default 15) | `(BMW OR Audi) NEAR/3 (motorcycle OR car)` |
| `ONEAR/x` | Como NEAR pero respetando orden | `(BMW OR Audi) ONEAR/3 (motorcycle OR car)` |
| `SENTENCE` | Misma oración | `(BMW OR Audi) SENTENCE (motorcycle OR car)` |
| `OSENTENCE` | Misma oración, orden respetado | `(BMW OR Audi) OSENTENCE (motorcycle OR car)` |

---

## Opciones de búsqueda avanzada

| Opción | Descripción | Ejemplo |
|--------|-------------|---------|
| Búsqueda simple | Palabra o frase | `Apple` |
| `title:` | Solo en el título | `title:sixt` |
| `content:` | Solo en el contenido | `content:sixt` |
| `author:` | Por autor | `author:Franz` |
| `authorshort:` | Nombre corto del autor (case sensitive) | `authorshort:franz_1975` |
| `mention:` | Mención de usuario (case sensitive) | `mention:@franz_1975` |
| `hashtag:` | Hashtag (case sensitive) | `hashtag:#bmw` |
| `lang:` | Idioma (código ISO 2 letras) | `lang:de` |
| `gender:` | Género del autor | `gender:male` |
| `author_id:` | ID del autor | `author_id:"ig:4024202702"` |
| `source_id:` | ID de la fuente | `source_id:"ig:4024202702"` |
| `authordescription:` | En la biografía del autor | `authordescription:"car enthusiast"` |
| `sourcecountry:` | País de la fuente | `sourcecountry:de` |
| `authorcountry:` | País del autor | `authorcountry:fr` |
| `sourcetype:` | Tipo de medio | `sourcetype:BLOG` |
| `is:comment` | Solo comentarios | `is:comment` |
| `-is:comment` | Sin comentarios | `-is:comment` |
| `is:retweet` | Solo retweets | `is:retweet` |
| `-is:retweet` | Solo posts originales | `-is:retweet` |
| `is:twitter_reply` | Solo respuestas de Twitter | `is:twitter_reply` |
| `is:author_verified` | Autor verificado | `is:author_verified` |
| `is:source_verified` | Fuente verificada | `is:source_verified` |
| `is:question` | Preguntas | `is:question` |
| `contains:image` | Con imagen | `contains:image` |
| `contains:audio` | Con audio | `contains:audio` |
| `contains:video` | Con video | `contains:video` |
| `is:important` | Marcado importante en Talkwalker | `is:important` |
| `is:read` | Marcado como leído | `is:read` |
| `is:checked` | Sentimiento revisado manualmente | `is:checked` |
| `score:n` | Puntuación manual (0–10) | `score:4` |
| `posttype:` | Tipo de post | `posttype:IMAGE`, `posttype:LINK`, `TEXT`, `VIDEO`, `AUDIO` |
| `device:` | Dispositivo | `device:BOT`, `device:MOBILE_IOS`, etc. |
| `image:` | Logo/objeto/escena en imagen | `image:apple`, `image:scene-amusement_park` |
| `demographic:` | Demografía | `demographic:occupation-accountant` |
| `customerentity:` | Entidad personalizada (documentos importados) | `customerentity:"Brand:Auto/Ferrari"` |
| `custom.<campo>:` | Campo personalizado | `custom.example:"Texto"` |

---

## Búsqueda por URL

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| `domainurl:` | Dominio de la URL | `domainurl:reddit.com` |
| `root_url`, `host_url` | Otros filtros por URL según documentación | Ver referencia API |

---

## Sentimiento y métricas

En queries puedes filtrar por sentimiento y métricas (sintaxis exacta según documentación):

| Concepto | Ejemplo típico |
|----------|----------------|
| Sentimiento negativo | `sentiment:NEGATIVE` o por rango |
| Sentimiento positivo | `sentiment:POSITIVE` |
| Restricciones por métrica | Mín/máx para engagement, reach, etc. (ver documentación) |

---

## Tips

- En frases (`""`) y búsqueda raw (`+""`) los espacios múltiples se normalizan.
- Los espacios incluyen tabulaciones y saltos de línea.
- Para tipos de fuente (`sourcetype`), `posttype`, `lang`, etc., consulta la lista de valores en el portal de desarrollador o en el editor de queries de Talkwalker.

---

## Próximo paso

- Usar estas queries en el [Search API](03-search-api.md) con el parámetro `q`.
- Practicar en el notebook **02_buscar_datos**.
