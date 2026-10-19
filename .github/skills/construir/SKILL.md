---
name: construir
description: Fase 3 del proceso spec-driven - construye la siguiente unidad de trabajo (historia de docs/BACKLOG.md o pieza de docs/PIECES.md), espera el OK del usuario, un commit por unidad. Usar cuando existan docs/SPEC.md y docs/ARCHITECTURE.md y el usuario diga "construir", "siguiente historia", "siguiente pieza" o "fase 3".
---

# Fase 3 — Dirigir: generar por unidades con contexto

Se construye **una unidad por invocación**, nunca el proyecto entero. El usuario dirige; vos ejecutás.

## Proceso

1. Leé `docs/SPEC.md`, `docs/ARCHITECTURE.md` y `docs/PIECES.md`. Si falta alguno, detenete y pedí la fase previa. Si existe `docs/BACKLOG.md`, leelo también.
2. Elegí la unidad de trabajo y anunciala antes de tocar código:
   - Si hay **piezas técnicas de base** pendientes en `docs/PIECES.md` (modelo de datos, runner de tests), van primero, una por vez.
   - Con la base lista y `docs/BACKLOG.md` presente, la unidad es la **primera historia `pendiente`** del backlog (o la que el usuario indique): marcala `en construcción` y leé sus criterios de aceptación.
   - Sin backlog, la unidad sigue siendo la primera pieza pendiente de `docs/PIECES.md`.
   - **En modo `equipo`** (ver AGENTS.md): el estado lleva dueño (`en construcción — <nombre>`), y antes de tocar código se crea la rama de la unidad desde `main` actualizado: `git checkout main && git pull && git checkout -b historia/<id>-<slug>` (o `fix/<slug>`).
3. Generala con el contexto de lo ya construido, respetando la arquitectura elegida. No agregues funcionalidades que no estén en la spec "ya que estamos".
4. **La unidad incluye sus tests.** Sin tests no está terminada. Para una historia, **cada criterio de aceptación (Dado/Cuando/Entonces) se convierte en al menos un test** — nombralo de forma que se reconozca el criterio. Sumá además los bordes técnicos: nulos, vacíos, tipos erróneos, errores esperables. Si el proyecto aún no tiene runner de tests configurado, configurarlo es parte de la pieza 1.
5. Corré la suite completa (los tests de esta pieza y los de las anteriores) y **mostrá la salida real** al usuario. Con tests en rojo no se avanza: se corrige primero.
6. Explicá qué hiciste y qué decisiones tomaste, e **invitá al usuario a leer el código y los tests en serio**: que pregunte todo lo que no le convenza. Ajustá hasta que diga explícitamente que está bien. Su lectura no es opcional — es la fase.
7. Solo con el OK explícito del usuario y la suite en verde:
   - Commit de la unidad (código + tests juntos): `feat: <historia o pieza>` (o `fix:`/`refactor:` según corresponda; para una historia, incluí su id: `feat: F1-H2 ...`). En modo `equipo`, el commit va a la rama de la unidad, **nunca a `main`**.
   - Actualizá su estado a `construida (pendiente de revisión)`: la historia en `docs/BACKLOG.md`, la pieza en `docs/PIECES.md`.
8. Recordale al usuario que la unidad **no se integra de verdad** hasta pasar la auditoría (skill `revisar`) en una sesión limpia, y cuál es la siguiente. En modo `equipo`, el cierre tras la auditoría es el **pull request**: lo revisa y mergea el dueño del proyecto (merge con squash: un commit por unidad en `main`), y la rama se borra al mergear.

## Desvíos

Si el usuario (o vos mismo, al construir) detecta algo fuera de `docs/SPEC.md`, frená antes de implementarlo: *"esto no está en la spec — ¿la actualizamos o lo descartamos?"*. Si se actualiza la spec, el cambio se escribe en `docs/SPEC.md` primero y se commitea aparte.
