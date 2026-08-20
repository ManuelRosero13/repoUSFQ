# Pista

No memorices comandos sueltos: piensa en **tres espacios distintos** que deben mantenerse sincronizados:

1. **Tu carpeta local** (lo que ves en tu editor).
2. **GitHub** (el remoto, llamado `origin` por convención).
3. **Otra copia local** (la carpeta "clonada" que simula a un compañero o a ti en otra máquina).

Preguntas guía para cada fase:

- **Fase 1-2:** ¿Ya existe el remoto vinculado a tu carpeta? Compruébalo con `git remote -v`. Si el remoto no existe todavía, `push` no tiene a dónde ir.
- **Fase 3:** Un Pull Request no es un comando de Git puro; es una función de GitHub. Antes de poder abrir uno, la rama debe existir **en GitHub**, no solo en tu computadora (`git push -u origin nombre-rama`).
- **Fase 4:** Si `git push` es rechazado, no es un error tuyo: significa que el remoto avanzó mientras tú no mirabas. `git status` después de un `git fetch` te dice si estás "atrás" o "adelante" del remoto. `git pull` es en realidad `git fetch` + `git merge` en un solo paso.
- Si aparece un conflicto en el README, ábrelo en tu editor: verás marcas `<<<<<<<`, `=======` y `>>>>>>>`. Decide qué líneas conservar de cada lado, elimina las marcas, guarda, y luego continúa con `git add` + `git commit`.

Si tienes GitHub CLI (`gh`) instalado, todo el flujo de crear el repo remoto y el Pull Request se puede hacer sin salir de la terminal. Si no, usa la web de GitHub para esos dos pasos puntuales, y la terminal para todo lo demás.
