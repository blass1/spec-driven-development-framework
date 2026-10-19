# Plantilla — Spec-Driven Development (GitHub Copilot)

Plantilla de proyecto para desarrollar con GitHub Copilot (CLI, coding agent, VS Code) siguiendo un proceso en 4 fases: **Especificar → Diseñar → Dirigir → Revisar**, con el humano decidiendo en cada punto de control.

## Cómo empezar un proyecto

**Proyecto nuevo:**
1. Copiá esta carpeta (o cloná el repo plantilla) con el nombre del proyecto nuevo.
2. `git init` si hace falta.
3. En Copilot CLI, pedí la fase 1: *"arranquemos la spec"* (skill `especificar`) y seguí en orden.

**Proyecto ya empezado (o prototipo que salió bien):**
1. Copiá `AGENTS.md` y `.github/` al repo existente.
2. Pedí el diagnóstico: *"veamos juntos si este proyecto está bien armado"* (skill `diagnostico`): lo recorren área por área y sale un informe con la ruta recomendada (adoptar / graduar / sigue desechable / reescribir).
3. Según la ruta: `adoptar` reconstruye la spec desde el código y marca lo existente como heredado.
4. De ahí en más: features nuevas por las fases 2-4, bugs y ajustes por `mantener`.

## Cómo funciona

- **`AGENTS.md`** es el contrato: Copilot lo carga siempre y le dice al agente las reglas permanentes (la spec manda, una pieza por vez, un commit por pieza, el humano decide).
- **`.github/skills/`** tiene un skill por fase (formato estándar `SKILL.md`): Copilot los activa cuando la tarea coincide con su descripción, o cuando los nombrás.
- **`.github/agents/auditor.md`** es un custom agent para la fase 4: un perfil de auditor externo que no edita lo que audita.

| Fase | Skill | Produce |
|------|-------|---------|
| 1. Especificar | `especificar` | `docs/SPEC.md` (el contrato) |
| 2. Diseñar | `disenar` | `docs/ARCHITECTURE.md` + `docs/PIECES.md` |
| 2.5 Historias | `historias` | `docs/BACKLOG.md`: características e historias con criterios de aceptación |
| 3. Dirigir | `construir` | una historia (o pieza) + un commit, por vez |
| 4. Revisar | `revisar` / agente `auditor` | veredicto INTEGRA / NO SE INTEGRA |
| Excepción | `prototipo` | `DESECHABLE.md` (modo vibecode) |
| Mantenimiento | `mantener` | bugs con test de regresión; ajustes menores |
| Paso 0 existente | `diagnostico` | `docs/DIAGNOSTICO.md`: análisis conjunto + ruta recomendada |
| Proyecto existente | `adoptar` | spec reconstruida + piezas `heredada (sin auditar)` |
| Cierre de versión | `release` | bump semver propuesto + `CHANGELOG.md` + tag anotado |
| Retomar | `estado` | dónde está el proyecto y el siguiente paso, leído de docs + git |

**Importante:** la fase 4 se corre en una **sesión nueva de Copilot** — la IA que escribió el código no se audita a sí misma. El custom agent `auditor` refuerza el rol, pero la sesión limpia la abrís vos.

## Trabajo en equipo y versiones

`AGENTS.md` tiene un **modo de trabajo** (`solo` / `equipo`). En `equipo`: `main` protegida, una rama por historia, PRs que revisa y mergea el dueño del proyecto (merge con squash), y dueño por historia en el backlog. Las versiones se cierran con el skill `release`: semver con tag anotado, bump propuesto desde los commits, `CHANGELOG.md` por versión.

## Skills personales (opcional)

Para tener las fases disponibles en TODOS tus repos del trabajo sin copiar la plantilla, copiá las carpetas de `.github/skills/` a `~/.copilot/skills/`.

## Estructura

```
proyecto/
├── AGENTS.md                  ← el contrato (Copilot lo carga siempre)
├── .github/
│   ├── skills/
│   │   ├── especificar/SKILL.md
│   │   ├── disenar/SKILL.md
│   │   ├── construir/SKILL.md
│   │   ├── revisar/SKILL.md
│   │   ├── prototipo/SKILL.md
│   │   ├── mantener/SKILL.md
│   │   ├── adoptar/SKILL.md
│   │   ├── historias/SKILL.md
│   │   ├── diagnostico/SKILL.md
│   │   ├── release/SKILL.md
│   │   └── estado/SKILL.md
│   └── agents/
│       └── auditor.md         ← custom agent para la fase 4
├── docs/
│   ├── SPEC.md                ← fase 1: el contrato funcional
│   ├── ARCHITECTURE.md        ← fase 2: decisión de arquitectura y su porqué
│   ├── BACKLOG.md             ← fase 2.5: características e historias con criterios de aceptación
│   └── PIECES.md              ← piezas técnicas de base y estado
└── DESECHABLE.md              ← solo si es un prototipo (excepción al proceso)
```

## La filosofía

> Lo que importa es la capacidad de dirigir el proceso: especificar bien, diseñar bien,
> revisar bien y responsabilizarte del resultado. La IA ejecuta; vos decidís.
