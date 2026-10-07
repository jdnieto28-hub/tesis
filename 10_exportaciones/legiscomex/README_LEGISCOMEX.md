# legiscomex/ — Declaraciones de exportación de oro (DIAN vía Legiscomex)

> Ficha elaborada el 14-sep-2026 al reubicar los archivos que Juan dejó en la raíz de
> `BDATOS-ORO/` (descargados el 14-sep-2026 entre las 04:21 y las 05:09 desde el demo de
> Legiscomex de la Biblioteca Javeriana, **vigente hasta el 3-nov-2026**). Contenido intacto:
> solo se movieron y, en el caso del crudo, se renombró. Prompt de descarga:
> `../PROMPT_CLAUDE_CHROME_legiscomex.md`.

## Qué es

Registro **declaración por declaración** (una fila = una serie de una DEX) de las
exportaciones colombianas, fuente DIAN, con 67 columnas: fecha (año/mes/día), número de
declaración, tipo (INICIAL/MODIFICACIÓN), aduana y aduana de embarque, agente aduanero,
**NIT y razón social del exportador**, municipio (domicilio del exportador), razón social y
dirección del importador, subpartida a 10 dígitos, descripción de la mercancía, cantidad,
**kg netos y brutos**, país de destino, **departamento de origen de la mercancía**,
departamento de procedencia, lugar de salida, vía de transporte, régimen y modalidad,
moneda, forma de pago, **valor FOB (USD y COP)**, flete, seguro, precios unitarios y
continente de destino.

Es el **universo** de declaraciones (no un extracto como el F600 de la DIAN, que trae
300 filas): la suma de kg reproduce UN Comtrade con diferencia ≤ 0,05 % en 7108 (ver
validación).

## Archivos (hoja única `detalle`, sin fila de encabezado extra)

| Archivo | Subpartida | Ventana | Filas | kg netos | NIT exportadores |
|---|---|---|---|---|---|
| `legiscomex_expo_7108120000_2017.xlsx` | 7108120000 oro en bruto | 2017 | 2.259 | 48.732,3 | 117 |
| `legiscomex_expo_7108120000_2018.xlsx` | 7108120000 | 2018 | 1.724 | 40.794,5 | 108 |
| `legiscomex_expo_7108120000_2019.xlsx` | 7108120000 | 2019 | 2.976 | 48.700,7 | 169 |
| `legiscomex_expo_7108120000_2020.xlsx` | 7108120000 | 2020 | 4.139 | 65.673,3 | 238 |
| `legiscomex_expo_7108120000_2021.xlsx` | 7108120000 | 2021 | 4.542 | 76.843,6 | 312 |
| `legiscomex_expo_7108120000_2022.xlsx` | 7108120000 | 2022 | 3.881 | 67.494,5 | 294 |
| `legiscomex_expo_7108120000_2023.xlsx` | 7108120000 | 2023 | 4.348 | 68.524,8 | 199 |
| `legiscomex_expo_7108120000_2024.xlsx` | 7108120000 | 2024 | 4.051 | 67.023,7 | 161 |
| `legiscomex_expo_7108120000_2025.xlsx` | 7108120000 | 2025 | 2.912 | 57.014,3 | 129 |
| `legiscomex_expo_7108120000_2026_ene-jun.xlsx` | 7108120000 | ene–jun 2026 (último dato 30-jun-2026) | 1.724 | 34.776,3 | 102 |
| `legiscomex_expo_7108130000_2023.xlsx` | 7108130000 semilabrado | 2023 | 27 | 3.217,6 | 2 |
| `legiscomex_expo_7108130000_2024.xlsx` | 7108130000 | 2024 | 25 | 2.865,0 | 2 |
| `legiscomex_expo_7108130000_2025.xlsx` | 7108130000 | 2025 | 7 | 143,8 | 2 |
| `legiscomex_expo_7108130000_2026_ene-jun.xlsx` | 7108130000 | ene–jun 2026 | 3 | 1,9 | 1 |
| `legiscomex_expo_2616901000_2023.xlsx` | 2616901000 minerales de oro y concentrados | 2023 | 274 | 38.383.361,9 | 29 |
| `legiscomex_expo_2616901000_2024.xlsx` | 2616901000 | 2024 | 401 | 32.027.155,4 | 35 |
| `legiscomex_expo_2616901000_2025.xlsx` | 2616901000 | 2025 | 749 | 53.314.763,5 | 43 |
| `legiscomex_expo_2616901000_2026_ene-jun.xlsx` | 2616901000 | ene–jun 2026 | 622 | 32.322.954,8 | 41 |

Faltan (no se descargaron): 7108130000 y 2616901000 para 2017–2022. El demo permite bajarlos
hasta el 3-nov-2026.

### `raw/legiscomex_raw_expo_7108120000_2023.xlsx`

Descarga **cruda** de la plataforma (nombre original `16003d31e84e4c53a0d67ce32d3d8c78.xlsx`,
md5 `c22f19814ec294d3978d0d2e68ab8ea7`): dos hojas, `Resumen` (parámetros de la consulta:
rango 2023/01/01–2023/12/01, filtro 7108120000, columnas pedidas) y `Detalle` (encabezado en
la fila 3, columna extra `fila`, aviso «máximo 80.000 registros»; 4.348 filas de datos, las
mismas de la versión limpia). Se conserva porque la versión limpia **pierde información**:

- `Descripción de la Mercancía` está **truncada a 255 caracteres** en los archivos limpios;
  el crudo trae el texto completo (hasta >300 caracteres), que en oro incluye ley/fineza,
  gramos brutos y finos, número de RUCOM, visto bueno ANM, número de autorización y pagos de
  regalías. Es la única traza documental mina→exportación que existe en la base.
- Los precios unitarios FOB vienen redondeados a 2 decimales en los limpios; el crudo trae
  el valor completo.
- Los limpios normalizan espacios dobles («ZONA FRANCA  DE  RIONEGRO» → «ZONA FRANCA DE RIONEGRO»).

Juan bajó tres copias crudas idénticas de 2023 (mismo conjunto de 4.348 filas, solo cambia
el orden dentro del día); las otras dos quedaron en `BDATOS-ORO/_para_borrar/legiscomex_raw_duplicados/`.
**Recomendación:** si los crudos de 2024, 2025, 2026 y de 2616901000 siguen en Descargas,
guardarlos aquí en `raw/` con el mismo patrón de nombre antes de perderlos.

## Validación (14-sep-2026) — kg netos Legiscomex vs UN Comtrade (`../comtrade_oro_subpartidas_anual_2010_2025.csv`)

| Año | 710812 Legiscomex | Comtrade | dif. | 710813 Legiscomex | Comtrade | 261690 Legiscomex (2616901000) | Comtrade (261690, 6 dígitos) |
|---|---|---|---|---|---|---|---|
| 2017 | 48.732,3 | 48.712,1 | +0,04 % | — | 5.579,3 | — | 602.862,6 |
| 2018 | 40.794,5 | 40.794,5 | 0,00 % | — | 4.597,0 | — | 2.399.784,0 |
| 2019 | 48.700,7 | 48.700,7 | 0,00 % | — | 3.498,8 | — | 4.207.841,5 |
| 2020 | 65.673,3 | 65.673,3 | 0,00 % | — | 3.203,1 | — | 6.680.184,4 |
| 2021 | 76.843,6 | 76.843,6 | 0,00 % | — | 2.604,4 | — | 13.662.621,1 |
| 2022 | 67.494,5 | 67.510,4 | −0,02 % | — | 3.168,5 | — | 23.485.792,1 |
| 2023 | 68.524,8 | 68.487,2 | +0,05 % | 3.217,6 | 3.217,6 | 38.383.361,9 | 38.383.402,1 (0,00 %) |
| 2024 | 67.023,7 | 67.020,8 | 0,00 % | 2.865,0 | 2.865,0 | 32.027.155,4 | 32.269.763,7 (−0,75 %) |
| 2025 | 57.014,3 | 57.014,3 | 0,00 % | 143,8 | 143,8 | 53.314.763,5 | 53.398.650,7 (−0,16 %) |

Conclusión: Legiscomex ES el microdato detrás de Comtrade. 7108120000 + 7108130000 en 2023 =
71.742 kg frente a 71.705 kg del prompt (dif. 0,05 %). En 261690 la pequeña diferencia
negativa es esperable: Comtrade a 6 dígitos incluye 2616909000 (demás minerales preciosos),
que no se descargó.

## Advertencias de uso

- **Grano empresa, no mina.** `Municipio` es el domicilio del exportador (2023: Bogotá 78 %,
  Buenaventura 20 %). El origen de la mercancía está en `Departamento Origen` (2023 oro en
  bruto: Antioquia 92 % de las filas) — **no hay municipio de origen**. No sustituye la
  producción municipal ANM/SIMCI; sirve para la compuerta exportadora (H4, brecha).
- **Personas naturales anonimizadas**: la razón social sale como «PERSONA NATURAL» (2023: 572
  filas de 4.348 = 13 %; 2026 ene–jun: 69). Su NIT/cédula sí figura: **no propagar** a documentos.
- **«Considerado confidencial por parte de la fuente oficial»** aparece en `País de Destino`
  (2019: 95, 2020: 94, 2021: 186, 2022: 87, 2023: 20, 2024: 13 filas; ninguna en 2025–2026 ni
  en razón social). Tratar como destino desconocido, no como país.
- Las **zonas francas** figuran como país de destino («ZONA FRANCA DE RIONEGRO-MEDELLÍN»,
  «ZONA FRANCA DE PALMASECA CALI», «ZONA FRANCA DE PACÍFICO CALI»): en 2017–2021 son el primer
  «destino» de 7108120000. Equivalen al socio 838 «Free zones» de Comtrade y al destino
  «COLOMBIA» del F600. Para destino final hay que encadenar la reexportación desde zona franca
  (no está en esta base).
- `Descripción de la Mercancía` está vacía en TODO 2017–2022 (la plataforma no la trae para
  esos años) y truncada a 255 caracteres en 2023–2026 (ver crudo).
- Toda celda es texto en los limpios (`Año`, `Mes`, kg, USD): convertir con `pd.to_numeric`.
  El crudo trae `Año`/`Mes`/`Dia` numéricos.
- 261690 se mide en **toneladas de mineral/concentrado**, no de oro fino: nunca sumar con 7108.
- 2026 cubre enero–junio (último dato 30-jun-2026); la plataforma publica con ~2 meses de rezago.
- Cada año es una descarga separada; una misma declaración puede tener varias filas (series).
  2023: 4.348 filas = 4.168 declaraciones únicas.

## Réplica

Legiscomex → Estadísticas → Exportaciones → Colombia → filtro «Código Partida» a 10 dígitos,
rango anual, exportar Detalle a Excel (tope 80.000 filas por descarga; ningún año lo alcanza).
Comparar siempre los kg contra Comtrade antes de usar.
