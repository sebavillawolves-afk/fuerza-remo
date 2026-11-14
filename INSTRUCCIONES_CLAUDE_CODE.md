# Instrucciones para Claude Code

Objetivo: subir esta carpeta a un repositorio nuevo de GitHub y publicarla con GitHub Pages, para instalarla en un iPhone como app web. La app ya está completa; no modifiques su contenido.

## Pasos
1. Comprueba que `git` y la CLI `gh` están instalados y que `gh auth status` muestra una sesión activa. Si falta algo, guía al usuario para instalarlo o iniciar sesión (`gh auth login`) antes de seguir.
2. Pregunta al usuario qué nombre quiere para el repositorio (sugerencia: `plan-fuerza-remo`). Adviértele que el repositorio será **público**, requisito para usar GitHub Pages gratis, y que cualquiera con el enlace podrá ver el contenido de la página (los registros que él ingrese en el teléfono no se suben). Espera su confirmación.
3. En esta carpeta: `git init`, rama `main`, commit inicial con todos los archivos.
4. Crea el repositorio y sube el código: `gh repo create <nombre> --public --source=. --remote=origin --push`.
5. Activa GitHub Pages desde la rama `main`, carpeta raíz:
   `gh api -X POST repos/{owner}/{repo}/pages -f "source[branch]=main" -f "source[path]=/"`
6. Espera a que el sitio esté publicado (`gh api repos/{owner}/{repo}/pages` hasta que `status` sea `built`) y verifica que `https://<usuario>.github.io/<nombre>/`, `…/manifest.webmanifest` y `…/sw.js` respondan 200.
7. Entrega al usuario el enlace final y estos pasos para el iPhone:
   - Abrir el enlace en **Safari** (no en la app de Claude ni en Chrome).
   - Tocar Compartir > Agregar a pantalla de inicio > Agregar.
   - Abrir la app una vez con internet; desde ahí funciona sin conexión.

## Después
Para cambios futuros sigue las reglas de `CLAUDE.md`, en especial subir `VERSION` en `sw.js` en cada publicación.
