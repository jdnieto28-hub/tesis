# Reporte — capas EVOA (UNODC–MinMinas / SIMCI). Extracción 2026-08-26

## Geoportal accesible
Sí (vía ArcGIS Enterprise público de UNODC Colombia, sin login ni token).
- Visor final: https://experience.arcgis.com/experience/de5828f9f1a1471a9e91101874f32330 ("Acceso a Información EVOA", ArcGIS Experience Builder; el web map subyacente es el ítem https://unodc-online.maps.arcgis.com/sharing/rest/content/items/a0e0b4945c0849c59089a35d63b8dade/data?f=json, que hoy apunta al host viejo caído; los servicios vivos están en el host nuevo).
- Servicio que alimenta los visores (raíz): https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA?f=json
- biesimci.org solo tiene mapas PNG estáticos (https://www.biesimci.org/index.php?id=110) y el enlace al SAI EVOA (https://accesoevoa.unodc.org.co/ → login WordPress, credenciales se piden a menergia@minenergia.gov.co). geoportal.biesimci.org devuelve 403.

## Capas EVOA halladas (nombre | años | grano | campos clave)
Carpeta SIMCI_EVOA (20 servicios). Los relevantes para el panel municipal:
- VISOR_EVOA_EN_COLOMBIA/MapServer/1 "Municipio (ha)" | 2014, 2016, 2018–2023 (1.388 registros; 2021=173, 2022=177, 2023=178 filas, 101 con EVOA>0 cada año) | municipio (polígono DANE) | OID, Año, Cod_depto, Cod_mpio, EVOA (ha), DEPTO, MUNICIPIO
- VISOR_EVOA_EN_COLOMBIA/MapServer/0 "Departamento (ha)" | 2014–2023 (140 reg.) | departamento | Año, Cod_depto, DEPARTAMEN, EVOA
- VISOR_EVOA_EN_COLOMBIA/MapServer/4 "dbo.VISOR_EVOA_EN_COLOMBIA_MUNICIPIO_PORC_VIEW" | 2014–2023 (883 reg., solo EVOA>0) | municipio | Anio, Codmpio, MUNICIPIO, TotalEvoa, EvoaAnio (total nacional), PorcMpio
- VISOR_EVOA_EN_COLOMBIA/MapServer/2 "Municipio" y /3 "Departamento" | sin año | polígonos límite DANE | Codmpio, Codepto
- VISOR_EVOA_FIGURAS_DE_LEY/MapServer/2 "Figuras de ley" (tabla) | 2014–2023 (3.050 reg.; 2021=352, 2022=365, 2023=376) | municipio × figura territorial (SZH, RI, PNN, TCN, ZPDRNR, RFPN, RAMSAR, Ley 2ª) | ANIO, Cod_Depto, Cod_Mpio, Municipio, FigLey_Lic_Amb, FigLey_Amp_Titulo, FigLey_RPP, FigLey_Ares_Decl, FigLey_SL_D0933, FigLey_SL_L0685, FigLey_Ares_Tram, FigLey_Propuesta_Cont, FigLey_ZMC_Etnica, FigLey_Sin_FL, ClaseFL_PermisosTecnicos, ClaseFL_En_Transito, ClaseFL_Exp_Ilicita, EVOA
- VISOR_EVOA_FIGURAS_DE_LEY/MapServer/1 "Mpio (ha)" y /0 "Depto (ha)" | 2014–2023 | municipio / depto | mismos campos que EN_COLOMBIA/1
- VISOR_EVOA_DINAMICA/MapServer/2 "Dinámica general" (tabla) | 2014–2023 (883 reg.) | municipio | ANIO, Cod_Mpio, Dinamica_Abandono, Dinamica_Estable, Dinamica_Nuevo, Dinamica_Expansion, EVOA
- VISOR_EVOA_DINAMICA/MapServer/3 "Dinámica histórico" (tabla) | 2014–2023 (~5.500 reg.; 2021=692, 2022=708, 2023=712) | municipio × dinámica (formato largo) | ANIO, Cod_Mpio, DINAMICA, Area_ha
- VISOR_EVOA_DENSIDAD/MapServer/0 "Densidad" | por Anio (24 polígonos) | polígonos de densidad (gridcode) | gridcode, Densidad, Anio
- VISOR_EVOA_PRODUCCION_METALES_PRECIOSOS/MapServer/10 "dbo.VISOR_EVOA_PRODUCCION_METALES_TABLE" (tabla) | 2017–2025, trimestral + consolidado anual (10.174 reg.) | municipio × metal × tipo de explotador | ANIO, TRIMESTRE, CODMPIO, MPIO, METAL, EXPLOTADOR (ARE, BAREQUEROS, CHATARREROS, SOLICITUDES DE LEGALIZACIÓN, SUBCONTRATOS DE FORMALIZACIÓN, TÍTULOS MINEROS), GRAMO_ORO, GRAMO_PLATA, GRAMO_PLATINO, GRAMOSTOTAL — (producción declarada; útil para su variable dependiente, NO descargada)
- Otros servicios EVOA disponibles (no descargados): VISOR_EVOA_TME (TCN, RI, PNN, TME MPIO/DPTO, MUNICIPIO (ha)), VISOR_EVOA_AGUA (Alertas, Ríos, SZH, tabla Tabla_EVOA_AGUA), VISOR_EVOA_EVOA_AGUA_MAP, VISOR_EVOA_COCA_Y_EVOA (Municipio, Dinámica EVOA y Coca por Municipio, tablas G1K/G5K), VISOR_EVOA_COBERTURAS_ALTO_VALOR_AMBIENTAL, VISOR_EVOA_MODELO_DE_RESTRICCION_AMBIENTAL, VISOR_EVOA_Y_ECOSISTEMAS, VISOR_EVOA_ZONAS_Y_SUBZONAS_HIDROGRAFICAS, VISOR_EVOA_BIESIMCI (MPIOS + tabla BIESIMCI), VISOR_EVOA_CONSULTA_PERSONALIZADA, VISOR_EVOA_DM_COMP_MINERO, VISOR_EVOA_PUEBLOS_INDIGENAS_AMAZONIA, VISOR_EVOA_EVOAYCOCA, VISOR_EVOA_EN_COLOMBIA_202407041650.

## URLs de servicio VERIFICADAS (una por línea, resultado de la prueba del paso 4)
https://arcgisenterprise.unodc.org.co/server/rest/services?f=json → 200, lista carpetas (SIMCI_EVOA, SIMCI_COCA, Modulo_EVOA_y_Coca, …)
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA?f=json → 200, 20 servicios MapServer listados
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_EN_COLOMBIA/MapServer?f=json → 200, ArcGIS Server 11.3, capabilities Map,Query,Data, supportedQueryFormats JSON/geoJSON/PBF, maxRecordCount 2000, 6 capas
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_EN_COLOMBIA/MapServer/1/query?where=1%3D1&outFields=*&returnGeometry=false&f=json&resultRecordCount=5 → 200, 5 registros con Año, Cod_depto, Cod_mpio, EVOA, DEPTO, MUNICIPIO (ej. 2014 | 94884 Puerto Colombia | 12,465 ha)
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_EN_COLOMBIA/MapServer/1/query?where=1%3D1&outFields=A%C3%B1o&returnDistinctValues=true&returnGeometry=false&f=json → 200, años 2014,2016,2018,2019,2020,2021,2022,2023
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_EN_COLOMBIA/MapServer/1/query?where=A%C3%B1o%3D%272023%27&returnCountOnly=true&f=json → 200, count 178 (2021: 173, 2022: 177)
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_EN_COLOMBIA/MapServer/1/query?where=A%C3%B1o%3D%272023%27&outFields=*&returnGeometry=false&orderByFields=Cod_mpio&f=json → 200, 178 registros (descargado; igual para cada año)
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_EN_COLOMBIA/MapServer/0/query?where=1%3D1&outFields=*&returnGeometry=false&f=json → 200, 140 registros departamentales
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_EN_COLOMBIA/MapServer/4/query?where=1%3D1&outFields=*&returnGeometry=false&orderByFields=OID&resultOffset=0&resultRecordCount=220&f=json → 200 (paginado 5×220 = 883 registros)
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_FIGURAS_DE_LEY/MapServer?f=json → 200, capas 0 Depto (ha), 1 Mpio (ha); tabla 2 Figuras de ley
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_FIGURAS_DE_LEY/MapServer/2/query?where=ANIO%3D%272023%27&outFields=*&returnGeometry=false&orderByFields=OID&resultOffset=0&resultRecordCount=50&f=json → 200 (paginado de 50 por ~44 KB/página; 376 registros 2023, 365 en 2022, 352 en 2021)
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_DINAMICA/MapServer?f=json → 200, capas 0 Mpio (ha), 1 Depto (ha); tablas 2 Dinámica general, 3 Dinámica histórico
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_DINAMICA/MapServer/2/query?where=1%3D1&outFields=*&returnGeometry=false&orderByFields=OID&resultOffset=0&resultRecordCount=160&f=json → 200 (6 páginas = 883 registros)
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_DINAMICA/MapServer/3/query?where=ANIO%3D%272023%27&outFields=*&returnGeometry=false&orderByFields=OID&resultOffset=0&resultRecordCount=240&f=json → 200 (3 páginas/año)
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_DENSIDAD/MapServer/0?f=json → 200, 24 polígonos, campos gridcode, Densidad, Anio
https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_PRODUCCION_METALES_PRECIOSOS/MapServer/10/query?where=1%3D1&outFields=*&f=json&resultRecordCount=2 → 200, registros de producción (2017 | 05002 ABEJORRAL | BAREQUEROS | GRAMO_ORO 232,9)
Geometrías (polígonos municipales con EVOA, por año): https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA/VISOR_EVOA_EN_COLOMBIA/MapServer/1/query?where=A%C3%B1o%3D%272023%27&outFields=*&returnGeometry=true&outSR=4326&f=geojson (no descargado; el mismo polígono DANE se repite por año, basta unir por codigo_municipio)
FALLIDAS: https://arcgisserver.unodc.org.co/arcgis/rest/services/SIMCI/Visor_EVOA_en_Colombia/MapServer?f=json → HTTP 500/503 (host viejo caído: todo /arcgis/rest/* devuelve "Error interno en el servidor"); https://geoportal.biesimci.org/ → 403; https://geoportal.biesimci.org/arcgis/rest/services → 404; https://arcgisenterprise.unodc.org.co/server/rest/services/Modulo_EVOA_y_Coca?f=json → "Token Required".
Nota WFS/GeoServer: no aplica; la plataforma es ArcGIS Server (no hay endpoint WMS/WFS expuesto en el host nuevo; no probado GetCapabilities OGC).

## Archivos descargados y su ubicación
Entregados en la conversación (ZIP EVOA_SIMCI_UNODC_2026-08-26.zip) y en el workspace de la sesión (carpeta evoa/entrega):
- 01_evoa_municipio_ha_2014_2023.csv (1.388 filas) — panel municipal completo (base para el modelo)
- 02_evoa_departamento_ha_2014_2023.csv (140)
- 03_evoa_municipio_participacion_2014_2023.csv (883)
- 04_evoa_figuras_de_ley_detalle_2021_2023.csv (1.093 × 36 columnas)
- 05_evoa_municipio_clases_figura_ley_2021_2023.csv (303) — permisos / en tránsito / ilícita por municipio, formato datos.gov.co
- 06_evoa_dinamica_general_2014_2023.csv (883)
- 07_evoa_dinamica_historico_2021_2023.csv (2.112)
- 08_panel_municipal_formato_datosgov_2018_2023.csv (601) — 2018–2020 de g48d-yu62 + 2021–2023 del servicio, mismas columnas
- EVOA_SIMCI_UNODC_extraccion_2026-08-26.xlsx — todo lo anterior + hoja LEEME con diccionario
Validación: totales nacionales 2018=92.046 / 2019=98.028 / 2020=100.752 / 2021=98.567 / 2022=94.733 / 2023=105.060 ha (coinciden con las cifras publicadas por UNODC); los 298 registros municipales 2018–2020 del servicio son idénticos a datos.gov.co g48d-yu62 (0 diferencias >0,01 ha); la tabla de figuras de ley agregada por municipio cuadra con la capa municipal en 2021–2023 (0 diferencias >0,5 ha).

## Obstáculos encontrados
- SAI EVOA (https://accesoevoa.unodc.org.co/) exige usuario y contraseña (WordPress); no se creó cuenta ni se intentó ingresar. No es necesario: los mismos datos están en el ArcGIS Server público.
- Host antiguo arcgisserver.unodc.org.co caído (HTTP 500/503); por eso el Experience público muestra "La fuente de datos no existe o no es accesible". El host nuevo arcgisenterprise.unodc.org.co responde sin token.
- Carpeta Modulo_EVOA_y_Coca requiere token; CO_OCCP también.
- No hay descarga directa (shapefile/CSV) en la interfaz; la extracción se hizo por REST query. Límite maxRecordCount 2000 → paginar con resultOffset/resultRecordCount (o `exceededTransferLimit`).
- El sandbox de esta sesión no tiene salida de red hacia *.unodc.org.co ni datos.gov.co (403 del proxy); la extracción se hizo desde el navegador (fetch/get_page_text), no con curl. Para automatizar desde otro entorno basta `requests` o `arcgis`/`esridump` contra las URLs anteriores.
- Efecto colateral: al navegar a una URL CSV de datos.gov.co el navegador descargó un archivo (g48d-yu62.csv) a la carpeta de Descargas; es solo un CSV de datos abiertos, puede borrarse.
- CORS: los servicios responden con CORS abierto desde arcgis.com; no hubo bloqueos.
