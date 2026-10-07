# 10_exportaciones — Exportaciones de oro de Colombia (HS 7108)

> Ficha elaborada el 27-ago-2026. Fuente: **UN Comtrade**, endpoint público de vista
> previa (sin llave): `comtradeapi.un.org/public/v1/preview/C/A/HS` con
> `reporterCode=170&cmdCode=7108&flowCode=X&format=csv`, una llamada por año
> (el endpoint rechaza periodos múltiples separados por coma). El dato original
> lo reporta la DIAN/DANE a Naciones Unidas; Comtrade es la vía de acceso abierta
> sin registro en ANDA.

## Archivos

| Archivo | Contenido | Grano | Ventana |
|---|---|---|---|
| `comtrade_expo_oro_7108_anual_2010_2025.csv` | Exportaciones totales al mundo: kg netos y USD FOB | nacional × año | 2010–2025 |
| `comtrade_expo_oro_7108_destinos_2023.csv` | Desglose por país de destino (17 socios) | destino × año | 2023 |
| `comtrade_espejo_usa_importaciones_desde_colombia.csv` | Espejo: lo que EE. UU. reporta importar desde Colombia | nacional × año | 2023–2024 |

## Validaciones (27-ago-2026)

1. La suma de los 17 destinos de 2023 reproduce **exactamente** el total mundial:
   71.704,79 kg y US$ 3.403.928.661,75 (0 de diferencia).
2. Filtros aplicados a la respuesta cruda: `customsCode=C00` (todo régimen),
   `motCode=0` (todos los modos de transporte), `partner2Code=0`. La API duplica
   cada fila por modo de transporte (1000 aéreo, 3200 carretera) y por segundo
   socio (899): **nunca sumar filas sin filtrar**.
3. Espejo EE. UU. 2023: 25.587,3 kg (CIF US$ 1.565,0 M) contra 24.398,7 kg FOB
   declarados por Colombia hacia EE. UU. — diferencia +4,9 % en peso, consistente
   con margen CIF/FOB y rezagos de registro.

## Advertencias de uso

- 2010–2016 provienen de clasificaciones HS legacy (H3/H4) sin desglose modal y
  con `netWgt` entero; 2017+ (H5/H6) traen decimales y desglose por modo.
- 2025 figura como año completo en Comtrade a la fecha de descarga; verificar
  revisiones cuando DANE publique cierres definitivos.
- El socio **838 = «Free zones»** (categoría especial de Comtrade, no un país):
  en 2023 concentra 8.925 kg (12,4 %). Relevante para el eslabón de
  comercialización/zonas francas; no confundir con destino final.
- El valor es FOB en USD corrientes; para brechas con producción usar **kg**
  (advertencia de la identidad contable: volúmenes, no valores).
- Serie mensual y microdato por partida requieren ANDA (DANE) o DIAN (petición);
  este bloque cubre el agregado anual, suficiente para la brecha
  producción–exportación.

## Réplica

Una URL por año (2010–2025), p. ej.:
`https://comtradeapi.un.org/public/v1/preview/C/A/HS?reporterCode=170&period=2023&cmdCode=7108&flowCode=X&partnerCode=0&format=csv`
Destinos: misma URL sin `partnerCode`. Espejo: `reporterCode=842&flowCode=M&partnerCode=170`.
Pendiente menor: incorporar este bloque a `scripts/actualizar_bases.py`.

---

## Ampliación 28-ago-2026 — Subpartidas DIAN e importaciones

Solicitud: códigos DIAN 7108120000, 7108130000, 7108200000 y 2616901000 —
evolución, compradores e importaciones. Fuente: mismo endpoint público de
Comtrade (dato origen DIAN/DANE), una llamada por año; a 6 dígitos los códigos
nacionales equivalen a 710812, 710813, 710820 y 261690.

### Archivos nuevos

| Archivo | Contenido | Grano |
|---|---|---|
| `comtrade_oro_subpartidas_anual_2010_2025.csv` | Totales X y M por subpartida (kg; USD FOB expo / CIF impo) | subpartida × flujo × año |
| `comtrade_oro_subpartidas_socios_2010_2025.csv` | Desglose por país socio (comprador en X, vendedor en M) | socio × subpartida × flujo × año |

### Validaciones (28-ago-2026)

1. Interna: en los 87 grupos año×flujo×subpartida la suma de socios reproduce
   el total mundial (exacta 2017+; dif ≤2 kg en 2010–2016 por enteros legacy).
2. Cruzada: 710812 + 710813 reproduce EXACTAMENTE el total 7108 del archivo
   `comtrade_expo_oro_7108_anual_2010_2025.csv` en los 16 años ⇒ 710811 (polvo)
   y 710890 (demás) son cero en todo el periodo.

### Hallazgos de la capa

- **710820 (oro monetario): cero operaciones** en X y M 2010–2025. El oro sale
  íntegro como no monetario (712812/710813); BanRep no mueve oro por aduana.
- **Importaciones de oro ≈ cero** (máx. 37 kg/año, típicamente <10 kg): Colombia
  es exportador neto puro; toda H4 puede ignorar el flujo M de 7108.
- **710813 (semilabrado) se extingue**: ~5-6 t/año 2011–2018 (Suiza/EE. UU.) →
  0,14 t en 2025. La canasta se concentra en oro en bruto.
- **261690 (mineral/concentrados) explota tras 2017**: 0–133 t/año hasta 2016 →
  602 t (2017) → 38.383 t (2023) → 53.399 t (2025, US$451 M). Compradores:
  China 38 %, Perú 19 %, Alemania 11 %, Singapur, EAU, India. Vía marítima.
  OJO: a 6 dígitos incluye 2616.90.10.00 (oro) y 2616.90.90.00 (demás preciosos);
  el desglose exacto a 10 dígitos requiere la base DIAN.
- **Compradores de oro en bruto (710812), acumulado 2010–2025 (898 t)**:
  EE. UU. 49 %, Italia 12 %, Suiza 10 %, zonas francas 10 %, Hong Kong 4,8 %,
  India 4,5 %, EAU 3,7 %. Recomposición reciente: Suiza casi desaparece tras
  2014; Italia pico 2020–2022; en 2024–2025 suben Canadá (12,9 t en 2025),
  EAU (8,1 t) y Sudáfrica (4,5 t, nueva) mientras EE. UU. modera (15,1 t).

### Rutas DIAN directas identificadas (para microdato a 10 dígitos)

- **Bases Estadísticas de Comercio Exterior** (mensuales desde 2001):
  `dian.gov.co/dian/cifras/Paginas/Bases-Estadisticas-de-Comercio-Exterior-Importaciones-y-Exportaciones.aspx`
  — por fallo del Trib. Adm. de Cundinamarca (19-sep-2022, exp. 25000-23-41-000-2022-00994-00)
  se publican CON identificación de personas jurídicas ⇒ parte del derecho de
  petición DIAN ya es pública. La biblioteca de archivos exige navegador con JS
  (web_fetch rebota a login; sandbox bloquea el host).
- **Directorio de Importadores/Exportadores** (desde 2017): misma sección Cifras.
- **Microdato DANE EXPO por año SIN registro ANDA** (zips directos federados en
  datos.gov.co): `microdatos.dane.gov.co/index.php/catalog/472/download/{id}`
  (2011–2024; p. ej. 23641=2023, 24667=2024; catálogo 859 = 2025–2026, id 24665;
  catálogo 554 = 2005–2010). Sandbox bloqueado: descargar vía navegador.

### Réplica

`comtradeapi.un.org/public/v1/preview/C/A/HS?reporterCode=170&period={AÑO}&cmdCode={CODIGOS}&flowCode={X|M}&format=csv`
— 710812 solo (destinos numerosos superan el tope de ~500 filas si se combina),
trío 710813,710820,261690 junto, M con los cuatro juntos. Filtrar SIEMPRE
customsCode=C00, motCode=0, partner2Code=0 (2019 añade C03/C07; 2018–2017
mosCode «0 » con espacio). En M el kg está en netWgt o altQty y el valor es CIF.

---

## Ampliación 9-sep-2026 — Entregas DIAN (derecho de petición y registro de usuarios aduaneros)

Dos archivos llegados a la raíz del repositorio y reubicados aquí con nombre
descriptivo. Los derivados se regeneran con `scripts/13_dian_f600_usuarios_aduaneros.py`.

| Archivo | Origen | Contenido | Grano | Ventana |
|---|---|---|---|---|
| `dian_f600_exportaciones_oro_710812_710813_2010_2026.csv` | Respuesta DIAN al derecho de petición **2026DP000279747** (radicado 27-ago-2026; respuesta 04-sep-2026, formulario 1474 No. 1474953711814). Nombre original: `informacion_f600_subpartidas.csv` (contenido intacto) | Declaraciones de exportación (formulario 600), 118 columnas: exportador (NIT y razón social), destinatario, aduana de salida, país de destino, subpartida, kg netos, USD FOB, fechas | registro = serie de una declaración | 2009-12 – 2026-08 |
| `dian_usuarios_aduaneros_vigentes_2026-09-09.xlsx` | Portal DIAN, registro de usuarios aduaneros vigentes, descarga 09-09-2026. Nombre original: `Usuarios-aduaneros-09-09-2026.xlsx` | Hoja `UA_vigentes`: NIT, nombre, tipo de registro (44 tipos), seccional, códigos SYGA/MUISCA | registro (foto) | corte 09-09-2026 |

Derivados (todos en esta carpeta):

| Archivo | Qué es |
|---|---|
| `dian_usuarios_aduaneros_vigentes_2026-09-09.csv` | La hoja completa en CSV UTF-8 (2.313 filas, 1.910 NIT únicos; un NIT puede tener varios registros) |
| `dian_sci_vigentes_2026-09-09.csv` | Solo Sociedades de Comercialización Internacional (399) + C.I. MIPYMES (23) = 422 NIT. Responde al punto 3 del derecho de petición (listado de SCI, caso hijo 2026DP000279747-1) |
| `dian_f600_oro_anio_subpartida.csv` | F600 agregado: año × subpartida (registros, formularios, exportadores, kg netos, USD FOB) |
| `dian_f600_oro_exportador_anio.csv` | F600 agregado: exportador × año × subpartida, con destinos y aduanas. Las 10 declaraciones de personas naturales se agrupan como «PERSONA NATURAL» (sin nombres ni cédulas) |
| `dian_f600_exportadores_vs_usuarios_aduaneros.csv` | Cruce por NIT de los 131 exportadores del F600 con el registro vigente: 18 aparecen hoy como SCI vigentes; los demás no figuran en el registro 2026 (liquidados, sin registro o exportan bajo otra figura) |

### Validaciones (9-sep-2026)

1. F600: 300 registros = 239 formularios únicos (un formulario puede traer varias series);
   subpartidas 7108120000 (288) y 7108130000 (12); 131 NIT exportadores, 10 personas naturales.
   Totales: 14.397,8 kg netos y US$ 347,5 M FOB en todo el periodo. Los agregados derivados
   reproducen exactamente estas sumas.
2. Usuarios aduaneros: 2.313 filas, 1.910 NIT; los 399 SCI son NIT únicos.
3. Cruce: de los 18 exportadores vigentes como SCI, destacan C.I. J. Gutiérrez (en toma de
   posesión), C.I. Metales Preciosos de Colombia, C.I. Gold by Gold, CIIGSA.

### Advertencias de uso — leer antes de usar el F600

- **NO es el universo.** 300 registros para 17 años, con máximo 6,5 t en 2018 y 0,1 t en 2025,
  frente a 50–70 t/año en Comtrade: es un extracto o muestra (probablemente tope de 300 filas
  de la consulta DIAN). Sirve para **caracterizar** exportadores, destinos, aduanas y la
  estructura de la declaración; **no sirve para totales ni series**. Pendiente: pedir a la DIAN
  la entrega completa o confirmar el criterio de selección de los 300 registros.
- Error de unidades en el origen: fila 2018 de «Aprovechamientos Industriales de la Costa»
  declara 6.280 kg de «oro chatarra» con US$ 174 mil FOB; la descripción dice **6.280 gramos**.
  Excluir o corregir (÷1000) antes de cualquier suma en kg.
- Destino «COLOMBIA» (88 registros) no es un error: son exportaciones a **zonas francas**
  (destinatarios en Rionegro y Palmira → Zona Franca de Rionegro y Zona Franca del Pacífico).
  Coincide con el socio 838 «Free zones» de Comtrade.
- Contiene datos personales (nombres y cédulas de personas naturales y de quien suscribe la
  declaración, campos C7–C10, C89, C1001–C1003). El archivo crudo se conserva tal como lo
  entregó la DIAN; **en documentos y derivados solo se usan razones sociales de personas
  jurídicas**; las personas naturales van agregadas como «PERSONA NATURAL».
- Fechas en formato AAAAMMDD (`C83 FECHA ACEPTACIN`); `C1ANNIO` es el año del formulario
  y puede diferir del año de aceptación (p. ej. formularios de 2026 aceptados en 2025-12).
- El registro de usuarios aduaneros es una **fotografía** a 09-09-2026: no informa desde
  cuándo está vigente cada registro ni cuáles se cancelaron antes. El campo «Seccional de
  Aduanas» trae valores múltiples separados por «;» (a veces con espacio).


---

## Ampliación 14-sep-2026 — Legiscomex (microdato DIAN por declaración, 2017–jun-2026)

Nueva subcarpeta **`legiscomex/`** con 18 archivos xlsx (una subpartida × un año), 67
columnas por declaración: NIT y razón social del exportador, importador, destino,
departamento de origen, aduana, kg, FOB. Cubre 7108120000 (2017–jun-2026), 7108130000 y
2616901000 (2023–jun-2026). Los kg reproducen Comtrade con diferencia ≤ 0,05 % ⇒ **es el
universo** que el F600 no daba. Detalle, validación año a año y advertencias en
`legiscomex/README_LEGISCOMEX.md`. Crudo de 2023 (descripción completa de la mercancía con
RUCOM y visto bueno ANM) en `legiscomex/raw/`.
