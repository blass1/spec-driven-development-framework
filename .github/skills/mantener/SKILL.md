---
name: mantener
description: Mantenimiento del proyecto bajo proceso spec-driven - bugs y cambios chicos sin pasar por las 4 fases completas. Usar cuando el proyecto ya tiene docs/SPEC.md y el usuario reporte un bug, pida un ajuste menor o diga "mantener", "arreglar", "fix".
---

# Mantenimiento — el atajo con reglas

Las 4 fases completas son para construir. Para mantener, el proceso es proporcional al cambio — pero la spec sigue siendo el contrato y los tests siguen siendo obligatorios.

## Paso 0 — Clasificar el pedido

Antes de tocar código, decidí (y decilo en voz alta) qué es:

- **Bug**: el código no hace lo que la spec dice. → Seguí el flujo de bug de abajo.
- **Ajuste menor**: cambia el CÓMO, no el QUÉ (refactor, texto, estilo, rendimiento). La spec no se toca. → Flujo de ajuste.
- **Funcionalidad nueva o cambio de comportamiento**: cambia el QUÉ. → **No es mantenimiento.** Se actualiza `docs/SPEC.md` primero (fase 1 corta), se agrega la pieza a `docs/PIECES.md`, y va por el flujo completo: `construir` → `revisar`. Si toca la arquitectura, pasa antes por `disenar`.

Si no está claro cuál es, preguntá — no adivines.

## Flujo de bug

1. **Reproducilo con un test que falle, ANTES de tocar el código.** Si no podés escribir un test que falle, no entendiste el bug todavía: investigá más o preguntá.
2. Corregí lo **mínimo** que hace pasar ese test. Nada de "ya que estamos" — lo que encuentres de paso se anota, no se arregla en el mismo commit.
3. Corré la suite completa. En verde, explicale al usuario la **causa raíz** (no solo el parche) y mostrá la salida de los tests.
4. Con su OK: un commit `fix: <bug>` que incluye el test de regresión.

## Flujo de ajuste menor

1. Anunciá qué vas a cambiar y qué NO va a cambiar de comportamiento.
2. Hacé el cambio. Los tests existentes son la red: la suite completa tiene que seguir en verde sin modificar los tests (si un ajuste "necesita" cambiar tests, es un cambio de comportamiento — reclasificá).
3. Con el OK del usuario: commit `refactor:`/`perf:`/`chore:` según corresponda.

## Revisión proporcional

- Cambio trivial (texto, estilo, un ajuste local con tests en verde): alcanza con la lectura del usuario.
- El cambio toca **seguridad, datos, dinero o una pieza marcada `heredada (sin auditar)`**: va a auditoría en sesión limpia (skill `revisar`) como cualquier pieza. Si la pieza tocada era heredada, esta es la oportunidad de auditarla: se revisa la pieza entera y se actualiza su estado en `docs/PIECES.md`.

## Regla permanente

Si durante el mantenimiento detectás que el código y `docs/SPEC.md` ya no coinciden (la spec quedó vieja), avisá: la spec se actualiza en su propio commit. Una spec desactualizada es peor que no tener spec.
