# Contrato de trabajo — Spec-Driven Development

Este proyecto se desarrolla con un proceso en 4 fases. El agente de IA **ejecuta**; el humano **especifica, decide, aprueba y se responsabiliza**.

## El contrato

`docs/SPEC.md` es el contrato del proyecto. Toda tarea empieza releyéndolo. Si un pedido —del usuario o una idea del propio agente— cae fuera de la spec, se señala antes de ejecutar: *"esto no está en la spec: ¿la actualizamos o lo descartamos?"*. Si se actualiza, el cambio a `docs/SPEC.md` se escribe y commitea primero.

## Las 4 fases

Cada fase es un **skill** en `.github/skills/` — cargalo y seguilo cuando la tarea o el usuario lo pidan:

1. **Especificar** (skill `especificar`) — Entrevista de 10 min a 1 h que produce `docs/SPEC.md`: qué hace en una frase, qué funcionalidades tiene esta versión y cuáles NO, qué datos maneja y con qué tecnología.
2. **Diseñar** (skill `disenar`) — El agente propone exactamente 2 arquitecturas con ventajas e inconvenientes y se detiene. **El humano elige.** La decisión y su porqué quedan en `docs/ARCHITECTURE.md`; las piezas a construir, en `docs/PIECES.md` (el modelo de datos siempre primero).
   - **2.5 Historias** (skill `historias`) — Las funcionalidades de la spec se desglosan en características e historias de usuario con criterios de aceptación Dado/Cuando/Entonces, en `docs/BACKLOG.md`. El humano valida historia por historia. Los criterios de aceptación se convierten en tests en la fase 3.
3. **Dirigir** (skill `construir`) — Una unidad por vez: la historia del backlog (o la pieza técnica, si no hay backlog o falta la base). El humano la lee en serio, pregunta lo que no le convence, y solo con su OK explícito se hace **un commit por unidad** y se pasa a la siguiente.
4. **Revisar** (skill `revisar`, o el custom agent `auditor`) — Una **sesión limpia, sin contexto**, corre la suite de tests y audita la unidad como auditor externo: ¿qué pasa con un dato inesperado?, ¿hay algo que comprometa la seguridad?, ¿podría el humano explicar este código a otra persona?, ¿los tests prueban algo de verdad?, y para historias, ¿se cumplen sus criterios de aceptación? Si alguno falla: **NO SE INTEGRA**. El humano decide al final.

## Reglas permanentes para el agente

- **Al retomar**: si la sesión arranca sin un pedido concreto, o el usuario pregunta dónde estaban o qué sigue, usar el skill `estado` — el punto del proceso se reconstruye desde los docs y git, nunca desde la memoria de la conversación.
- Nunca decidir arquitectura ni stack: proponer opciones con pros y contras, y esperar la decisión humana.
- Una pieza por vez; nunca "generar todo el proyecto".
- Una pieza incluye sus tests (caso normal + bordes); sin tests, o con la suite en rojo, la pieza no está terminada y no se commitea.
- Un commit por pieza aprobada (código + tests juntos); nada se commitea sin OK explícito.
- No agregar funcionalidades "ya que estamos": lo que no está en la spec, no existe.
- El auditor no edita lo que audita: la revisión reporta; las correcciones vuelven a la fase de construcción.
- Estado de avance: historias en `docs/BACKLOG.md` y piezas técnicas en `docs/PIECES.md` (pendiente → construida (pendiente de revisión) → revisada ✓; en proyectos adoptados existe además `heredada (sin auditar)`).

## Trabajo en equipo

**Modo de trabajo de este repo: `solo`** ← cambiar a `equipo` cuando haya más de una persona.

En modo `equipo` rigen además estas reglas:

- **`main` protegida**: nada se commitea directo. Todo cambio — código, docs, mantenimiento — va por rama + pull request.
- **Una rama por unidad**: `historia/<id>-<slug>` o `fix/<slug>`, nacida de `main` actualizado; muere al mergear.
- **El dueño del proyecto revisa y mergea**: todos los PRs pasan por el dueño; nada del colaborador entra a `main` sin su OK. Los PRs del propio dueño entran con la auditoría IA (fase 4) aprobada, que en todos los casos es el filtro previo al PR, no su reemplazo.
- **Merge con squash**: un commit por unidad en `main`, aunque la rama tenga varios.
- **Dueño por historia**: al tomarla, su estado pasa a `en construcción — <nombre>` en `docs/BACKLOG.md`. Nunca dos personas en la misma historia ni tocando los mismos archivos; si dos historias chocan en archivos, se secuencian.
- Los docs (`SPEC.md`, `ARCHITECTURE.md`, `BACKLOG.md`) son el contrato de ambos: también cambian por PR.

## Versiones

- **Semver** con tags **anotados**, solo sobre `main`: PATCH = solo fixes; MINOR = historias nuevas; MAJOR = cambio incompatible del contrato (la spec rompió algo que existía).
- Se taggea con el skill `release`, nunca a mano suelta: historias de la versión `revisada ✓`, suite en verde, `CHANGELOG.md` actualizado.
- Un tag publicado es una promesa: no se mueve ni se borra; si salió mal, se corrige con un PATCH nuevo.

## Mantenimiento y adopción

- Con el proyecto andando, los bugs y ajustes menores van por el skill `mantener`: clasificar el pedido primero (bug / ajuste / funcionalidad nueva), bug se reproduce con un test que falla antes de corregir, y todo cambio de comportamiento pasa por actualizar `docs/SPEC.md` — no es mantenimiento.
- Para sumar este proceso a un proyecto ya empezado, primero el skill `diagnostico` (paso 0): recorrer el proyecto junto al usuario, evaluar si está bien armado y recomendar la ruta — adoptar directo, graduar un prototipo, dejarlo desechable, o rescatar la spec y reescribir. El informe queda en `docs/DIAGNOSTICO.md`.
- Después, el skill `adoptar`: reconstruye la spec desde el código, documenta la arquitectura as-is y marca lo existente como `heredada (sin auditar)` en `docs/PIECES.md`. Las piezas heredadas se auditan de forma oportunista: cuando el mantenimiento toca una, pasa entera por `revisar` (salvo graduación de prototipo: ahí se audita todo antes de usuarios o datos reales).

## La excepción

Si existe `DESECHABLE.md` en la raíz, este proceso no aplica: es un prototipo/script desechable y se trabaja rápido y sin ceremonia (skill `prototipo`). **Línea roja:** si va a tener usuarios, datos reales o mantenimiento de meses, se borra ese archivo y se empieza por la fase 1.
