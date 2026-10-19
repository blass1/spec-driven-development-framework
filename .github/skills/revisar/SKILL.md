---
name: revisar
description: Fase 4 del proceso spec-driven - auditoría externa de la última unidad construida (historia o pieza) con criterios de datos inesperados, seguridad, explicabilidad, calidad de tests y criterios de aceptación; veredicto INTEGRA / NO SE INTEGRA. Usar en una sesión limpia cuando haya una unidad "construida (pendiente de revisión)" y el usuario diga "revisar", "auditar" o "fase 4".
---

# Fase 4 — Revisar: auditoría por criterio

Actuá como **auditor externo**. Este skill está pensado para una **sesión nueva y limpia**, sin el contexto de quien escribió el código: una IA revisando a otra, y un humano decidiendo al final.

**Si en esta misma sesión se construyó la pieza a revisar, decilo de entrada** y recomendá abrir una sesión nueva para la auditoría. Si el usuario igual quiere seguir acá, hacelo constar y revisá con el mayor desapego posible.

## Proceso

1. Leé `docs/SPEC.md`, `docs/PIECES.md` y, si existe, `docs/BACKLOG.md`. Identificá la unidad en estado `construida (pendiente de revisión)` — historia o pieza — o la que el usuario indique. Si es una historia, leé su enunciado y sus criterios de aceptación.
2. Leé el código de esa pieza **completo y sin asumir nada**: como si fuera de un desconocido. Leé también sus tests.
3. **Corré la suite de tests completa** y mirá la salida real. Suite en rojo, o pieza sin tests = **NO SE INTEGRA** directo, sin seguir evaluando.
4. Evaluá con exactamente estos criterios, en orden:
   - **A. ¿Qué pasa si llega un dato inesperado?** Nulos, vacíos, tipos erróneos, números negativos o enormes, strings con caracteres raros, listas vacías, archivos corruptos. Señalá cada punto de entrada sin validación.
   - **B. ¿Hay algo que comprometa la seguridad?** Inyección (SQL, comandos, paths), secretos hardcodeados, entrada del usuario sin sanitizar, permisos demasiado amplios, dependencias innecesarias o dudosas, datos sensibles en logs.
   - **C. ¿Podría el usuario explicar este código a otra persona?** Si hay magia, indirección innecesaria o complejidad injustificada, este criterio falla aunque el código "funcione".
   - **D. ¿Los tests prueban algo de verdad?** Que cubran los bordes de A (nulos, vacíos, errores) y no solo el camino feliz; un test que no puede fallar, o que repite la implementación, no cuenta.
   - **E. (solo historias) ¿Se cumplen los criterios de aceptación?** Cada Dado/Cuando/Entonces de la historia debe tener su test correspondiente, y ese test debe pasar. Un criterio sin test, o un comportamiento que no coincide con lo escrito, hace fallar este punto.
5. Emití un veredicto explícito: **INTEGRA** o **NO SE INTEGRA**.
   - Si cualquiera de los criterios falla, es **NO SE INTEGRA** — sin excepciones ni "pero es un detalle".
   - Cada hallazgo con referencia concreta `archivo:línea` y, si aplica, cómo corregirlo.
6. La decisión final es humana:
   - Veredicto positivo aceptado por el usuario → actualizá la unidad a `revisada ✓` (la historia en `docs/BACKLOG.md`, la pieza en `docs/PIECES.md`) y commit `review: <unidad> aprobada`.
   - Veredicto negativo → dejá la lista de correcciones clara para volver a la fase 3. **No corrijas vos: el auditor no edita lo que audita.**
