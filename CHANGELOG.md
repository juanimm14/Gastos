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
