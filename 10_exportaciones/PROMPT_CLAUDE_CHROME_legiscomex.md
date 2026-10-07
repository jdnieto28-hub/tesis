# Prompt para Claude en Chrome — descarga de exportaciones de oro en Legiscomex (demo Javeriana)

> Copia TODO lo que sigue a la línea y pégalo en Claude en Chrome.
> El acceso es un DEMO de la Biblioteca Javeriana vigente hasta el 3 de noviembre de 2026.

---

Necesito descargar de **Legiscomex** (módulo de estadísticas de comercio exterior de Colombia, fuente DIAN/DANE) las exportaciones de oro de Colombia con detalle por exportador, para mi trabajo de grado en Ciencia de Datos (P. U. Javeriana). Tengo acceso por la Biblioteca Javeriana.

## Acceso

1. Abre https://javeriana.libguides.com/legiscomex y sigue el enlace de acceso al recurso.
2. Cuando aparezca el login institucional (EZproxy de la Javeriana) o cualquier captcha, **detente y déjame escribir yo el usuario y la clave**. Nunca guardes ni repitas mis credenciales.
3. Si Legiscomex pide crear un usuario propio o aceptar términos, muéstrame la pantalla y espera mi confirmación.
4. No hagas clic en nada que implique comprar, cotizar o contratar módulos.

## Qué buscar

Dentro de Legiscomex ubica el módulo de **estadísticas de exportaciones de Colombia** (puede llamarse «Estadísticas», «Inteligencia comercial» o «Consulta por subpartida»; los nombres varían, explora el menú y dime qué encontraste antes de seguir).

Consulta de EXPORTACIONES por subpartida arancelaria, **una subpartida y un año a la vez**:

- Subpartidas: **7108120000** (oro en bruto, la principal), **7108130000** (semilabrado) y **2616900000** (concentrados de minerales preciosos).
- Años obligatorios: **2023, 2024 y 2025** (enero a diciembre; para 2025 y 2026 hasta el último mes disponible).
- Si el tiempo alcanza: 2017 a 2022, solo 7108120000.

Pide el **máximo nivel de detalle** que permita la plataforma. Columnas que necesito (todas las que existan):
fecha o mes · subpartida · NIT y razón social del exportador · país de destino · departamento de origen de la mercancía · aduana o lugar de salida · modalidad o régimen (incluida zona franca) · vía de transporte · peso neto (kg) · peso bruto (kg) · valor FOB (USD) · cantidad y unidad.

## Descarga

1. Exporta cada consulta a **Excel o CSV** con el detalle (no el resumen).
2. Nombra los archivos así: `legiscomex_expo_7108120000_2023.xlsx`, `legiscomex_expo_7108130000_2023.xlsx`, `legiscomex_expo_2616900000_2023.xlsx`, y lo mismo para 2024 y 2025.
3. Si la plataforma limita el número de filas por descarga, parte la consulta por trimestre o por mes y numera los archivos (`..._2023_T1.xlsx`).
4. Si no permite descargar, copia la tabla completa a un archivo y dímelo.
5. Deja todo en la carpeta Descargas; yo lo muevo después.

## Verificación (hazla antes de terminar)

Suma el peso neto (kg) de 7108120000 + 7108130000 por año y compáralo con estos totales de UN Comtrade (partida 7108):

- 2023: 71.705 kg
- 2024: 69.886 kg
- 2025: 57.158 kg

Si la diferencia supera el 5 %, no lo «corrijas»: repórtamelo con las dos cifras. También registra:

- hasta qué **mes y año** están actualizadas las estadísticas (fecha del último dato disponible) y, si aparece, la fecha de la última actualización de la plataforma;
- si alguna razón social sale oculta, anonimizada o como «persona natural»;
- cuántas filas trae cada archivo.

## Reglas

- No inventes valores ni completes celdas vacías.
- Si una consulta falla dos veces o la sesión se cierra, avísame y espera.
- Al final entrégame una tabla: subpartida · año · archivo · filas · kg totales · diferencia frente a Comtrade · último mes disponible.
