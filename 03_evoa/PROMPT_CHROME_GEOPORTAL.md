# Prompt para sesión con Claude en Chrome — geoportal SIMCI (EVOA municipal 2021+)

> Uso: abrir Chrome con la extensión de Claude conectada, iniciar una conversación
> y pegar TODO el bloque siguiente tal cual. Al terminar, copiar el reporte final
> que entregue Claude y traerlo a la sesión de la tesis para automatizar la descarga.

---

Misión: encontrar y extraer las capas EVOA (Evidencias de Explotación de Oro de
Aluvión) del geoportal SIMCI del convenio UNODC–Ministerio de Minas de Colombia.

Contexto: trabajo de grado sobre el efecto del precio del oro en Colombia. Ya
tengo el EVOA municipal 2018–2020 (datos.gov.co, ids g48d-yu62 y ub8r-2956) y la
tabla departamental 2020–2023 transcrita del informe 2023. Me falta el dato
MUNICIPAL (o los polígonos) de 2021, 2022 y 2023, que solo vive en el visor del
convenio. Necesito identificar el servicio de mapas que alimenta ese visor.

Pasos:

1. Abre https://www.biesimci.org/ y localiza su geoportal o visor de mapas
   (prueba también https://geoportal.biesimci.org/ directamente). Acepta cookies
   si las piden. Si exigen crear cuenta o iniciar sesión, DETENTE y repórtalo:
   no crees cuentas ni aceptes términos en mi nombre.

2. En el visor, busca en el catálogo/leyenda capas con los términos "EVOA",
   "oro", "aluvión" o "minería". Activa las que encuentres y anota su nombre
   exacto y los años disponibles.

3. Revisa las peticiones de red que hace el visor al activar cada capa y captura
   las URL de servicios geográficos. Patrones a buscar:
   - `/arcgis/rest/services/...` terminado en `MapServer` o `FeatureServer`
   - `/geoserver/...`, `service=WMS`, `service=WFS`, `GetCapabilities`
   - respuestas con `f=json`, `f=geojson` o `GetFeature`

4. Verificación ArcGIS REST: abre la URL base del servicio con `?f=json` para
   listar capas y campos. Luego prueba en una capa EVOA:
   `<URL_capa>/query?where=1%3D1&outFields=*&returnGeometry=false&f=json&resultRecordCount=5`
   y confirma que devuelve registros con campos tipo municipio / código DANE /
   año / hectáreas / figura de ley.

5. Verificación GeoServer/WFS: pide
   `.../ows?service=WFS&request=GetCapabilities`, anota los typeName de capas
   EVOA y prueba un GetFeature con `outputFormat=application/json&count=5`.

6. Si la interfaz ofrece descarga directa (GeoJSON, shapefile .zip, CSV,
   GeoPackage), descarga las capas EVOA de cada año disponible. Solo archivos de
   datos; ningún ejecutable.

7. Entrega un reporte final EXACTAMENTE con esta estructura:
   - Geoportal accesible: sí/no + URL final del visor
   - Capas EVOA halladas: nombre | años | grano (polígono/municipio/dpto) | campos clave
   - URLs de servicio VERIFICADAS (una por línea, con el resultado de la prueba del paso 4 o 5)
   - Archivos descargados y su ubicación
   - Obstáculos encontrados (login, token, CORS, bloqueos)

Ese reporte lo copiaré a otra sesión para automatizar la descarga completa:
sé literal con las URLs.

---

*Ficha creada el 26-ago-2026. Contexto completo de los informes EVOA y las demás
rutas de datos: `INFORMES_EVOA.md` en esta misma carpeta.*
