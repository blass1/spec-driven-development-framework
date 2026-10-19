---
name: estado
description: Retomar el trabajo - reconstruye en qué punto del proceso spec-driven está el proyecto leyendo los docs y git, y propone el siguiente paso. Usar al arrancar una sesión, o cuando el usuario pregunte "¿dónde estábamos?", "¿qué sigue?", "estado" o "retomemos".
---

# Estado — ¿dónde estábamos?

El estado del proyecto no vive en la memoria de nadie: vive en los docs y en git. Este skill lo reconstruye y lo dice en menos de un minuto. **No cambia nada**: solo lee y reporta.

## Proceso

1. Leé, de lo que exista: `DESECHABLE.md`, `docs/DIAGNOSTICO.md`, `docs/SPEC.md`, `docs/ARCHITECTURE.md`, `docs/BACKLOG.md`, `docs/PIECES.md`, `CHANGELOG.md`. Mirá también `git log --oneline -10`, `git status`, la rama actual y el último tag (`git describe --tags --abbrev=0`).
2. Determiná la situación con esta tabla (primera fila que aplique):

| Si… | El proyecto está en… |
|-----|----------------------|
| Existe `DESECHABLE.md` | Modo prototipo: se vibecodea; ofrecer `diagnostico` si quiere graduarlo |
| No hay `docs/SPEC.md` y hay código | Sin proceso: proponer `diagnostico` (paso 0) |
| No hay `docs/SPEC.md` y no hay código | Proyecto nuevo: proponer `especificar` (fase 1) |
| Hay SPEC pero no `docs/ARCHITECTURE.md` | Fase 2 pendiente: `disenar` |
| Hay arquitectura pero no `docs/BACKLOG.md` | Fase 2.5 pendiente: `historias` (o directo a `construir` si es chico) |
| Hay historia/pieza `en construcción` | Fase 3 a medias: retomarla (ver quién es el dueño en modo equipo) |
| Hay historia/pieza `construida (pendiente de revisión)` | Fase 4 pendiente: `revisar` en sesión limpia |
| Hay piezas `heredada (sin auditar)` y el trabajo las toca | Auditoría oportunista pendiente |
| Todo `revisada ✓` y hay commits sin taggear | Cierre pendiente: ofrecer `release` |
| Todo `revisada ✓` y taggeado | Versión cerrada: siguiente historia del backlog, o `especificar` v+1 |

3. Reportá en pocas líneas: **dónde está el proyecto** (fase y unidad concreta, con su id), **qué quedó a medias** (rama sin mergear, working tree sucio, PRs abiertos, suite sin correr), y **el siguiente paso propuesto** con el skill que corresponde.
4. Señalá inconsistencias si las ves (estados del backlog que no coinciden con git, spec desactualizada) — se corrigen por el skill que corresponda, no desde acá.
5. Esperá la confirmación del usuario antes de arrancar el siguiente paso.
