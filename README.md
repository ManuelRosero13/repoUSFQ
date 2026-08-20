# Semana 1 — Clase 2: Git/GitHub para trabajo iterativo y colaborativo

## Ubicación en el temario

**Objetivos de aprendizaje de la semana (contexto):**
- Configurar el flujo de trabajo base del semestre con Git/GitHub, ramas, commits, pull requests y colaboración.
- Reconocer el nuevo rol del desarrollador en el ciclo intención → ejecución → auditoría.

**Contenido específico de la clase 2 (ampliado):**
Repaso práctico de comandos **locales** (`init`, `status`, `add`, `commit`, `branch`, `checkout/switch`, `merge`, resolución de conflictos) **y de comandos remotos de GitHub** (`remote add`, `push`, `pull`, `fetch`, `clone`), aplicando el flujo completo **GitHub Flow**: issue/tarea → rama → commit → push → pull request → revisión → merge en el repositorio remoto.

## Enunciado
Practica GitHub Flow creando una sección “Bitácora creativa” en un README. Debes crear rama, commit, simular un cambio paralelo en `main`, provocar un conflicto, resolverlo y dejar el historial listo para pull request.

- Crear un repositorio en GitHub y conectarlo a su carpeta local (`git remote add origin ...`).
- Subir su historial por primera vez (`git push -u origin main`).
- Trabajar con ramas remotas (`git push origin <rama>`, `git branch -vv`, `git push -u origin <rama>`).
- Traer cambios remotos (`git fetch`, `git pull`).
- Clonar un repositorio existente (`git clone`) para simular el trabajo de un segundo colaborador.
- Abrir y fusionar un **pull request** desde la línea de comandos usando GitHub CLI (`gh pr create`, `gh pr merge`) o, como alternativa, desde la interfaz web de GitHub.

## Estructura de esta carpeta

```
clase-2-git-github/
├── README.md                       # Este archivo: contexto y guía general
├── docs/
│   ├── descripcion.md              # Enunciado del reto para los estudiantes
│   ├── pista.md                    # Pista para orientar sin resolver el reto
│   └── instrucciones.md            # Cómo probar y ejecutar el ejercicio
```

## Repositorio

1. **Cuenta de GitHub:** los estudiantes crean un repositorio vacío en su cuenta de GitHub (por la web o con `gh repo create`) y siguen los comandos conectando contra esa URL real. Esto es lo que deben usar para su entrega del semestre.

## Requisitos previos

- Git instalado (`git --version`).
- Cuenta de GitHub activa.
- (Opcional pero recomendado) [GitHub CLI](https://cli.github.com/) instalado y autenticado con `gh auth login`, para crear repos y pull requests desde la terminal.
- Editor de código (VS Code) y terminal (bash/zsh/Git Bash en Windows).
