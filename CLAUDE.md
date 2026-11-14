# Plan de fuerza y remo (app web instalable)

App personal de entrenamiento: rutinas de fuerza A/B/C en casa, días de remo, registro de series, temporizador de descanso, mediciones corporales y recomendaciones generales de alimentación. Se publica con GitHub Pages y se instala en el iPhone desde Safari (Compartir > Agregar a pantalla de inicio).

## Estructura
- `index.html`: toda la app en un solo archivo (estilos, datos de ejercicios, figuras animadas y lógica). No hay paso de compilación.
- `sw.js`: service worker que guarda la app para usarla sin conexión.
- `manifest.webmanifest` e `icons/`: nombre, colores e íconos de la app instalada.

## Reglas al modificar
1. Edita `index.html` directamente. Mantén todo en ese archivo; no agregues dependencias externas ni frameworks.
2. **Cada vez que cambies cualquier archivo, sube el número en `VERSION` dentro de `sw.js`** (por ejemplo `fuerza-remo-v1` a `fuerza-remo-v2`). Sin eso, los teléfonos pueden seguir mostrando la versión anterior.
3. Si agregas un archivo nuevo que la app necesita sin conexión, inclúyelo en la lista `FILES` de `sw.js`.
4. Usa siempre rutas relativas (`icons/…`, `sw.js`), nunca rutas que partan con `/`: el sitio vive en una subcarpeta de GitHub Pages.
5. Los registros del usuario se guardan en `localStorage` con la clave `plan-fuerza-remo-v1`. No cambies esa clave ni la forma del objeto guardado sin migrar los datos existentes (función `merge`).
6. No incluyas datos personales nuevos en el código: el repositorio y el sitio son públicos.
7. Idioma de la interfaz: español de Chile.

## Dónde está cada cosa en `index.html`
- `ANIMS` y `figure()`: poses y dibujo de las figuras animadas.
- `EX`: ejercicios (nombre, músculos, claves técnicas, error común).
- `RUT`: rutinas A, B y C. Cada puesto tiene listas por equipamiento (base, mancuernas, banco) que rotan en cada ciclo.
- `presc()`: series, repeticiones y pausas según la semana del ciclo de 8 semanas.
- `target()`: objetivo del día y peso sugerido (doble progresión).

## Publicar cambios
`git add -A && git commit -m "…" && git push`. GitHub Pages se actualiza en uno o dos minutos; la app se actualiza sola en el teléfono la próxima vez que se abra con internet.
