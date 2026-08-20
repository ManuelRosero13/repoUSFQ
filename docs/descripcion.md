# Reto práctico — Clase 2: "De mi carpeta local a GitHub"

## Contexto

Cada estudiante está armando el repositorio principal que usará durante todo el semestre para el curso de Desarrollo Web 3 (Stack MERN). Antes de escribir una sola línea de backend, necesitas dominar el flujo con el que vas a trabajar de aquí en adelante: **crear, versionar, subir y sincronizar tu proyecto entre tu computadora y GitHub**, incluyendo el ciclo completo de una Pull Request.

## Enunciado del reto

Vas a simular el ciclo de vida completo de una "Bitácora creativa del semestre", pero esta vez el trabajo no puede quedarse solo en tu computadora: debe llegar a GitHub y pasar por un Pull Request real, como lo harás en tus próximos proyectos.

Debes completar las siguientes fases, en orden:

### Fase 1 — Repositorio local
1. Crea una carpeta de proyecto e inicializa un repositorio Git.
2. Crea un archivo `README.md` con una sección `## Descripción` para tu bitácora del semestre.
3. Haz tu primer commit.

### Fase 2 — Conexión con GitHub
4. Crea un repositorio **vacío** en tu cuenta de GitHub (desde la web, o con `gh repo create` si tienes GitHub CLI).
5. Conecta tu repositorio local con el repositorio remoto (`git remote add origin ...`).
6. Sube tu rama principal por primera vez usando el flag de tracking (`git push -u origin main`).
7. Verifica en la web de GitHub que tu README apareció correctamente.

### Fase 3 — Trabajo en rama y Pull Request
8. Crea una nueva rama llamada `feature/bitacora-creativa`.
9. En esa rama, agrega una sección `## Bitácora creativa` a tu README con al menos 2 ideas.
10. Haz commit de ese cambio y **sube la rama a GitHub** (no a `main`).
11. Abre un Pull Request de `feature/bitacora-creativa` hacia `main` (usando `gh pr create` o la interfaz web).
12. Revisa el "diff" del Pull Request antes de fusionarlo.
13. Fusiona (merge) el Pull Request.

### Fase 4 — Sincronización y conflicto remoto
14. De vuelta en tu terminal, cambia a `main` local y trae los cambios fusionados con `git pull`.
15. Simula que trabajas desde "otra máquina": clona tu propio repositorio en una carpeta distinta con `git clone` (esto simula un segundo colaborador).
16. Desde esa copia clonada, haz un pequeño cambio directo en `main` remoto (por ejemplo agregar una línea a `## Descripción`) y súbelo con `push`.
17. Vuelve a tu carpeta original (la "primera máquina") y, **sin haber hecho pull todavía**, agrega una línea distinta en la misma sección `## Descripción` y trata de hacer `push`. Deberías recibir un rechazo porque el remoto tiene cambios que no tienes localmente.
18. Resuelve la situación: haz `git pull`, resuelve el conflicto si aparece, conserva la intención de ambos cambios, haz commit del merge y vuelve a subir con `push`.

## Criterios de aceptación

- El repositorio existe tanto localmente como en GitHub, con historial de commits visible en la web.
- El README final en `main` remoto contiene tanto la sección `## Descripción` (editada en dos "máquinas" distintas) como `## Bitácora creativa`.
- Existe al menos un Pull Request cerrado/fusionado en el historial del repositorio en GitHub.
- El estudiante puede explicar, en sus propias palabras, la diferencia entre `git fetch`, `git pull` y `git push`, y por qué ocurrió el rechazo en el paso 17.
- El historial de commits (`git log --oneline --graph --all`) refleja las ramas, el merge del PR y el merge del conflicto remoto.

## Entregable

Captura de pantalla del Pull Request fusionado en GitHub + el archivo `README.md` final + el comando `git log --oneline --graph --all` ejecutado en tu terminal, pegados en tu documento de bitácora del curso.
