# Changelog — Mis Gastos (PWA)

## v1 — 2026-08-06
Primera conversión a PWA instalable, sobre la base del `index (15).html` original.

- Agregado `manifest.json` (íconos, `display: standalone`, color de marca).
- Agregado `sw.js` (cache del shell, network-first, deja pasar Firebase/Firestore sin interceptar).
- Meta tags PWA en `index.html` (theme-color, apple-mobile-web-app-*, viewport-fit=cover).
- Inputs móviles a 16px (evita zoom automático al enfocar en iOS/Android).
- Botones de ícono con tap target mínimo de 34px.
- `padding` con `env(safe-area-inset-*)` en body y toast.
- Eliminado el comentario de instrucciones de setup de Firebase (quedaba público en el repo).
- Verificado en producción: manifest, sw registration y íconos responden 200 en `juanimm14.github.io/Gastos/`.

Snapshot completo de esta versión en `versions/v1/`.

## v2 — 2026-08-06
Mejoras visuales: consistencia entre plataformas y alineación de datos.

- Reemplazados todos los emojis de íconos (✏️ 🗑 💰 📋 🔒 🔓) por SVG inline propios — antes se veían distinto en cada SO (Windows/Android/iOS render diferente los emoji de color).
- Badges "Pagado/Pendiente" ahora usan un check/x en SVG en vez de los caracteres ✓/✗.
- Arreglado el alineado de columnas: los montos no quedaban en una columna prolija porque cada fila calculaba su propio ancho de columna ("auto") de forma independiente. Ahora las columnas monto/estado/acciones tienen ancho fijo.
- Arreglado que las filas de tarjetas (sin badge de estado) y las de "Cobrado" (con una columna extra vacía) tenían distinta cantidad de columnas que las filas normales, lo que corría todo el contenido. Ahora todas las filas usan siempre las mismas 4 columnas.
- Limpiado el texto de los toasts ("Guardado", "Monto manual guardado") sin símbolos sueltos.
- Verificado: sintaxis del script validada con `node --check`.

Snapshot completo de esta versión en `versions/v2/`.

## v3 — 2026-08-06
Fix de un bug de overflow reportado (algunos botones de eliminar se salían de la tarjeta) + mejoras de visibilidad.

- **Bug fix**: la columna de nombre usaba `1fr` puro, que en CSS Grid no se achica por debajo del contenido — con nombres largos empujaba el resto de la fila (botón eliminar incluido) fuera de la tarjeta. Cambiado a `minmax(0,1fr)` para que el nombre ahora se ajuste (haga wrap) en vez de desbordar.
- El botón de editar (lápiz) no tenía fondo y era casi invisible al lado del de eliminar (que sí tiene chip rosado). Ahora los botones de ícono `btn-ghost` tienen un fondo gris suave, igual de visibles que el de eliminar.
- Números grandes del resumen final (`rf-val`) ahora usan la tipografía serif de marca (`DM Serif Display`) en vez de la sans en negrita — más identidad visual.

Snapshot completo de esta versión en `versions/v3/`.

## v4 — 2026-08-06
Indicador de versión + Dashboard separado.

- Agregado un badge chiquito abajo a la izquierda (`v4`) para confirmar de un vistazo qué versión está viendo el navegador — útil porque el service worker cachea contenido.
- Nueva pestaña **Dashboard**, separada de la carga de gastos: selector "Gastos / Dashboard" en la tira del mes.
  - **Gastos**: solo secciones, extras y cobrado — la pantalla de carga quedó más liviana.
  - **Dashboard**: resumen final + los 3 gráficos (por sección, cobrado vs gastos, pagado vs pendiente), con título grande en serif.
- La vista elegida se guarda en `localStorage` y se mantiene al cambiar de mes.

Snapshot completo de esta versión en `versions/v4/`.

## v5 — 2026-08-06
Investigación de un corte horizontal reportado por captura de pantalla.

- El screenshot mostrado era de la **v3 en producción** (sin badge ni Dashboard todavía — esos son de v4, aún no subida).
- Probé reproducir el corte inyectando el HTML/CSS real de la app en la página en vivo a 700px, 960px y 1265px de ancho, con datos representativos (montos grandes, badges, etc.) — no logré reproducir overflow en ningún caso; la hipótesis más probable es un glitch transitorio del reflow al cargar las tipografías.
- Agregado `overflow-x: hidden` + `max-width: 100%` en `html, body` como red de seguridad: nada en el diseño necesita scroll horizontal de página completa (la barra de resumen ya tiene su propio scroll interno), así que esto elimina la categoría de bug sin costo visual, se haya encontrado la causa exacta o no.

Snapshot completo de esta versión en `versions/v5/`.

## v6 — 2026-08-06
El badge de versión estaba escondido (esquina inferior izquierda, letra chica, semi-transparente) — pasó desapercibido.

- Movido el badge de versión al lado del título "Mis Gastos" en el header, como una píldora azul bien visible (`v6`), en vez de una marca de agua tenue en una esquina.

Snapshot completo de esta versión en `versions/v6/`.

## v7 — 2026-08-06
Bug real confirmado con captura del celular (APK) y de la web: el botón de eliminar se salía de la tarjeta.

- **Causa**: la columna de acciones (editar+eliminar) quedó fijada en 66px (desktop) / 60px (mobile) en el fix de v3, pero los dos botones con su padding necesitan ~68-70px — no entraban, y al no poder achicarse (los botones tienen `min-width`), se salían de la columna y de la tarjeta. Pasaba en escritorio y en mobile, por eso se veía tanto en la web como en la APK.
- **Fix**: columna de acciones ampliada a 86px (desktop) / 84px (mobile).
- Verificado con medición real (no estimada) inyectando el HTML/CSS actualizado en la página en vivo: 0px de desborde en 1280px y en 375px (ancho de celular típico).

Snapshot completo de esta versión en `versions/v7/`.
