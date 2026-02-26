# Image API

La Image API permite detectar **logos**, **objetos** y **escenas** en imágenes, útil para análisis de contenido visual.

## Requisitos

- **URLs de imagen**: si pasas URLs, el dominio debe estar autorizado (whitelist) en tu cuenta Talkwalker. Si no, la API devuelve error 50 (URL no aprobada).
- **Subida de archivo**: como alternativa, se puede enviar la imagen por otro método si no usas URL.
- **Logo detection**: solo se pueden detectar logos que estén en tu lista predefinida. Si usas un ID no configurado, error 45.
- **Créditos**: se consumen créditos de procesamiento según tu suscripción.

## Endpoints típicos

- **Logo**: detección de logos en la imagen (IDs de logo configurados en la cuenta).
- **Objeto**: detección por códigos de objeto Talkwalker (lista de object codes en la documentación).
- **Escena**: detección por códigos de escena (scene codes).

La base URL es `https://api.talkwalker.com`; los paths exactos (p. ej. `/api/v2/detect/images/logo`, `.../object`, `.../scene`) y parámetros (p. ej. `image_url`, `detect`) figuran en la [documentación oficial](https://developer.talkwalker.com/guides/use-image-api).

## Errores frecuentes

- **Código 50**: URL de imagen no autorizada. Hay que dar de alta el dominio en Talkwalker.
- **Código 45**: ID de logo (o modelo) no conocido o no autorizado en tu cuenta.

## Notebook

Abre **09_image_api** en Colab para probar detección de logos, objetos y escenas con ejemplos.
