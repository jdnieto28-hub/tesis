# Informes EVOA — inventario, fuentes y rutas de replicación

> Ficha elaborada el 26-ago-2026. Complementa `README_DATOS.md` (§ 03_evoa) y
> `DICCIONARIO_CADENA.md` (eslabón extracción). Ningún dato de esta ficha es
> estimado: todo proviene de los documentos y páginas citados.

## 1. Qué es el sistema EVOA y quién lo produce

Sistema de monitoreo de **Evidencias de Explotación de Oro de Aluvión** con uso de
maquinaria (en tierra y en agua), operado desde 2016 por el convenio
**Ministerio de Minas y Energía – UNODC (proyecto SIMCI)**, con financiación de la
**Sección de Asuntos Antinarcóticos (INL) de la Embajada de EE. UU.** Metodología:
percepción remota — interpretación y procesamiento digital de imágenes satelitales
(Landsat 7 ETM / Landsat 8 documentados en las ediciones 2016–2018; la edición 2023
no especifica el sensor en el texto extraíble del PDF), índices espectrales para EVOA
en agua (12 ríos de Amazonía/Orinoquía), cruce con capas oficiales de legalidad
(títulos ANM, permisos ambientales ANLA/CAR, zonas excluibles, territorios étnicos,
RUNAP) y validación de campo/cartografía social.

**Lo que mide y lo que no:** superficie (ha) con huella de explotación aluvial a
cielo abierto en tierra; alertas en agua. **No** incluye minería de veta/subterránea
ni minería de subsistencia (barequeo). Es superficie detectada, no producción.

## 2. Serie de informes publicados (verificados)

| Datos de | Publicado | Cifra nacional (tierra) | Documento |
|---|---|---|---|
| 2014 | jun-2016 | (primera medición; cifra por verificar en el PDF) | unodc.org/documents/colombia/2016/junio/Explotacion_de_Oro_de_Aluvion.pdf |
| 2016 | 2018 | 83.620 ha | biesimci.org/fileadmin/2019/documentos/evoa/evoa-2016.pdf |
| 2018 (+prelim. 2019) | dic-2019 | 92.046 ha (2019 prelim.: 98.028) | comunicado unodc.org/colombia (05-dic-2019) |
| 2020 | jul-2021 | 100.752 ha | unodc.org/documents/colombia/2021/Agosto/Colombia_Explotacion_de_Oro_de_Aluvion_EVOA_Evidencias_a_partir_de_percepcion_remota_2020.pdf |
| 2021 | jun-2022 | 98.567 ha | unodc.org/documents/colombia/2022/Junio/Informe_Colombia_Explotacion_de_Oro_de_Aluvion_Evidencias_a_Partir_de_Percepcion_Remota_2021_SP_.pdf |
| 2022 | nov-2023 | 94.733 ha (73 % ilícita) | Resumen ejecutivo: unodc.org/documents/colombia/2023/noviembre-11/Resumen_Ejecutivo_EVOA_2022.pdf |
| **2023** | **abr-2026** | **105.060 ha (+11 %; 76 % ilícita)** | espejo ACM: acmineria.com.co/wp-content/uploads/2026/04/evidencias_de_explotacion_de_oro_de_aluvion_2023_compressed.pdf (+ infografía en la misma ruta) |
| 2024, 2025 | **no publicados** a abr-2026 | — | la propia ACM reclama el rezago |

Rezago editorial: ~2 años. El informe 2023 salió en abril de 2026.

## 3. Dónde están los DATOS (no los PDF) — rutas de replicación

1. **datos.gov.co** (ya descargado en este repo): `g48d-yu62` municipal y
   `ub8r-2956` departamental, **solo 2018–2020**, con el error de etiqueta
   BOYACA/Bolívar documentado en el README. Sin actualización desde entonces.
2. **Anexos tabulares de los PDF** (capturado 26-ago-2026): el informe 2023 trae
   la tabla departamental 2020–2023 y la tabla por figura de ley 2023 →
   transcritas verbatim a `evoa_departamental_2020_2023_informe2023.csv` y
   `evoa_2023_figura_ley_departamental.csv`. Sumas verificadas contra el total
   oficial (2020 y 2021 difieren ±1 ha por redondeo de la fuente).
   **Límite:** en lo municipal el PDF solo publica el top (Zaragoza 8.669 ha,
   Nechí 8.152, El Cantón del San Pablo 6.397, Nóvita 5.909, Cáceres 5.879 en
   2023; además 2022: El Bagre 4.398, Cáceres 4.936, Zaragoza 7.649). La tabla
   municipal completa 2021+ NO está en el PDF.
3. **Servicio ArcGIS del convenio — RESUELTO (26-ago-2026, sesión Chrome de Juan).**
   El visor real es el ArcGIS Experience «Acceso a Información EVOA»
   (experience.arcgis.com/experience/de5828f9f1a1471a9e91101874f32330), alimentado
   sin login por `https://arcgisenterprise.unodc.org.co/server/rest/services/SIMCI_EVOA`
   (ArcGIS Server 11.3; Query habilitado; maxRecordCount 2000). Capas clave:
   `VISOR_EVOA_EN_COLOMBIA/MapServer/1` (municipal, ha, 2014–2023, 1.388 filas),
   `/0` (departamental), `VISOR_EVOA_FIGURAS_DE_LEY/MapServer/2` (municipio ×
   figura de ley), `VISOR_EVOA_DINAMICA` (estable/nuevo/expansión/abandono) y
   `VISOR_EVOA_PRODUCCION_METALES_PRECIOSOS/MapServer/10` (**producción municipal
   TRIMESTRAL por tipo de explotador 2017–2025, oro y plata — aún sin descargar**).
   La extracción completa está en `arcgis_simci/` (8 CSV + XLSX + JSON crudos +
   reporte de URLs verificadas). Validación de instalación: 1.388 filas = count
   del servicio; totales nacionales exactos los 8 años (2014: 78.939 → 2023:
   105.060); los 298 registros 2018–2020 idénticos a datos.gov.co (0 diferencias);
   agregado departamental = tabla del PDF 2023; figura de ley 2023 exacta
   (20.672 / 4.757 / 79.631). Notas: geoportal.biesimci.org da 403; el SAI EVOA
   (accesoevoa.unodc.org.co) exige login — no se usó; el host viejo
   arcgisserver.unodc.org.co está caído.
4. **Réplica de terceros**: la ANT digitalizó los polígonos EVOA-2016 y los sirve
   en ArcGIS REST (exportable a GeoJSON/shapefile):
   `services9.arcgis.com/pZylgd2zhNey2qXF/ArcGIS/rest/services/PAZ_Y_CONFLICTO_/FeatureServer/1`.
   Útil como geometría histórica; citar como digitalización secundaria (no oficial SIMCI).
5. **Vía formal**: derecho de petición a MinMinas/UNODC-SIMCI solicitando la tabla
   municipal 2021–2023 (agregar al paquete de peticiones ya planeado: títulos ANM,
   Indumil, DIAN).
6. **Replicación desde cero** (Landsat/Sentinel + clasificación): viable
   técnicamente pero fuera del alcance del seminario; opción para el trabajo
   de grado completo (hasta abr-2027) solo si el asesor lo pide.

## 4. Hallazgos del informe 2023 relevantes para la tesis

- **Quiebre de tendencia:** 2021 (−2 %) y 2022 (−4 %) estables, 2023 **+11 %** —
  primera expansión fuerte del ciclo alcista reciente. Mayores incrementos:
  El Bagre (+26 %), Cáceres (+19 %), Zaragoza (+13 %) — Bajo Cauca antioqueño.
- **Composición de la producción formal:** hasta 2020 dominaban los títulos
  mineros; desde 2021 los barequeros superan a los títulos (2017-2022: barequeros
  45,2 % ≈ títulos 45,0 %). Conecta directamente con nuestra interpretación del
  canal formal como "estado documental".
- **Amparos administrativos (pista nueva de datos, eslabón extracción):** en
  Antioquia, del EVOA "con permisos" solo 9 % está libre de amparos; 87 % de los
  amparos se concentra en Zaragoza (37 %), Nechí (29 %) y El Bagre (22 %). La
  fuente advierte registro no estandarizado. Posible petición a ANM.
- **Subregistro reconocido oficialmente:** el informe declara que ANM ≠
  exportaciones de oro no monetario (DANE), que hay producción registrada en
  municipios distintos al de extracción, y que parte del oro ilegal se incorpora
  al circuito legal. Respaldo doctrinal directo del hallazgo de no-transmisión.
- Regalías de oro 2014→2023: COP $134 → $399 miles de millones (+198 %); precio
  promedio 81.246 → 269.278 COP/gr (Figura 8, fuente UPME 2023).
- Ecosistema de registro citado por el informe (eslabones superiores): Génesis
  (subsistencia), RUCOM, SIMCO/UPME, Cuentas Satélite DANE, visto bueno ANM +
  inspección DIAN en exportación.

## 5. Advertencias de uso (heredadas y nuevas)

1. EVOA = superficie acumulable/detectada, no producción; excluye veta y barequeo.
2. Serie municipal abierta termina en 2020; no mezclar con la departamental
   2021–2023 sin declarar el cambio de grano.
3. Redondeo de la fuente (verificado 26-ago-2026): en la tabla departamental, las
   sumas 2020 y 2021 exceden el total oficial en +1 ha (2022 y 2023 exactas); en la
   Tabla 1 (figura de ley), las sumas por columna difieren −1/−1/+2 ha de los
   totales oficiales, cuyo gran total sí es exacto (105.060 ha).
4. Guaviare, Vaupés y Vichada: solo alertas de EVOA en agua (0 ha en tierra).
5. El error BOYACA/Bolívar del dataset abierto NO aplica a los CSV nuevos
   (transcritos del PDF 2023).
