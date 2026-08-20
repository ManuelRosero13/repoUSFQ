# Solución completa comentada

> Ejecuta estos bloques en orden. Los bloques marcados como "MÁQUINA A" corresponden a tu carpeta de trabajo original; los marcados como "MÁQUINA B" corresponden a la carpeta clonada que simula a un colaborador.

## Fase 1 — Repositorio local (MÁQUINA A)

```bash
# Crear la carpeta del proyecto y entrar en ella
mkdir bitacora-web3 && cd bitacora-web3

# Inicializar el repositorio Git en esta carpeta
git init

# Crear el README inicial con la sección Descripción
printf "# Bitácora Web 3\n\n## Descripción\nRepositorio del semestre para Desarrollo Web 3.\n" > README.md

# Agregar el archivo al área de staging
git add README.md

# Crear el primer commit local
git commit -m "chore: crear README inicial"
```

## Fase 2 — Conexión con GitHub (MÁQUINA A)

```bash
# Opción A: crear el repositorio remoto vacío con GitHub CLI (recomendado)
gh repo create bitacora-web3 --public --source=. --remote=origin

# Opción B (si no usas gh): crea el repo vacío desde github.com/new
# y luego conecta el remoto manualmente:
git remote add origin https://github.com/TU-USUARIO/bitacora-web3.git

# Verificar que el remoto quedó registrado correctamente
git remote -v

# Renombrar la rama principal a "main" si aún se llama "master"
git branch -M main

# Subir la rama main por primera vez y establecer el tracking remoto
# -u (--set-upstream) hace que a partir de ahora "git push" y "git pull"
# sepan automáticamente a qué rama remota apuntar.
git push -u origin main
```

## Fase 3 — Rama, commit y Pull Request (MÁQUINA A)

```bash
# Crear y cambiar a una nueva rama de trabajo (no se toca main directamente)
git switch -c feature/bitacora-creativa

# Agregar la sección de bitácora creativa al README
printf "\n## Bitácora creativa\n- Idea 1: catálogo interactivo de arte.\n- Idea 2: generador de mundos narrativos.\n" >> README.md

# Confirmar el cambio en un commit descriptivo
git add README.md
git commit -m "docs: agregar bitacora creativa"

# Subir ESTA RAMA (no main) a GitHub, creando el tracking remoto
git push -u origin feature/bitacora-creativa

# Crear el Pull Request desde la terminal con GitHub CLI
gh pr create --base main --head feature/bitacora-creativa \
  --title "Agregar bitácora creativa" \
  --body "Agrega la sección de bitácora creativa al README del semestre."

# Alternativa sin gh: abre la URL que GitHub sugiere en la terminal
# tras el push, o entra a la pestaña "Pull requests" del repositorio en la web.

# Revisar el diff del PR antes de fusionar (opcional, muy recomendable)
gh pr diff

# Fusionar el Pull Request (borra la rama remota automáticamente con --delete-branch)
gh pr merge --merge --delete-branch
```

## Fase 4 — Sincronización y conflicto remoto

### Volver a main local y traer los cambios fusionados (MÁQUINA A)

```bash
git switch main

# git pull = git fetch (traer referencias remotas) + git merge (integrarlas)
git pull origin main
```

### Simular un segundo colaborador (MÁQUINA B)

```bash
# Salimos de la carpeta actual y clonamos el mismo repo en otra ubicación
cd ..
git clone https://github.com/TU-USUARIO/bitacora-web3.git bitacora-web3-colaborador
cd bitacora-web3-colaborador

# Este "colaborador" edita directamente la sección Descripción
sed -i 's/Repositorio del semestre para Desarrollo Web 3./Repositorio oficial del semestre - version colaborador./' README.md

git add README.md
git commit -m "docs: actualizar descripcion desde maquina B"

# Sube el cambio directo a main remoto
git push origin main
```

### De vuelta en la MÁQUINA A: provocar y resolver el conflicto

```bash
cd ../bitacora-web3

# Editamos la misma línea, pero con un texto distinto, SIN haber hecho pull antes
sed -i 's/Repositorio del semestre para Desarrollo Web 3./Repositorio oficial del semestre - version maquina A./' README.md

git add README.md
git commit -m "docs: actualizar descripcion desde maquina A"

# Intentamos subir: esto será RECHAZADO porque origin/main avanzó
# (el error dice "Updates were rejected because the remote contains work...")
git push origin main

# Traemos los cambios remotos y los integramos
git pull origin main
# Si git pull genera un conflicto en README.md, ábrelo: verás algo como
#
# <<<<<<< HEAD
# Repositorio oficial del semestre - version maquina A.
# =======
# Repositorio oficial del semestre - version colaborador.
# >>>>>>> <hash-del-commit-remoto>
#
# Edita el archivo a mano y deja una sola versión que combine la intención de ambos, por ejemplo:
cat > README.md <<'EOF_INNER'
# Bitácora Web 3

## Descripción
Repositorio oficial del semestre, actualizado por múltiples colaboradores.

## Bitácora creativa
- Idea 1: catálogo interactivo de arte.
- Idea 2: generador de mundos narrativos.
EOF_INNER

# Marcar el conflicto como resuelto y cerrar el commit de merge
git add README.md
git commit -m "merge: resolver conflicto de descripcion entre maquina A y B"

# Ahora sí, subir el resultado final
git push origin main

# Revisar el historial completo con ramas, merges y commits
git log --oneline --graph --all
```

## Comandos clave usados en este ejercicio (resumen)

| Comando | Qué hace |
|---|---|
| `git init` | Inicializa un repositorio Git en la carpeta actual |
| `git remote add origin <url>` | Vincula la carpeta local con un repositorio remoto en GitHub |
| `git remote -v` | Muestra los remotos configurados y sus URLs |
| `git push -u origin <rama>` | Sube una rama y establece el seguimiento (tracking) remoto |
| `git push` | Sube commits locales a la rama remota vinculada |
| `git fetch` | Descarga referencias remotas sin fusionarlas |
| `git pull` | Descarga y fusiona automáticamente (`fetch` + `merge`) |
| `git clone <url>` | Crea una copia local completa de un repositorio remoto |
| `gh repo create` | Crea un repositorio en GitHub desde la terminal (requiere GitHub CLI) |
| `gh pr create` | Crea un Pull Request desde la terminal |
| `gh pr diff` | Muestra el diff de un Pull Request |
| `gh pr merge` | Fusiona un Pull Request desde la terminal |
