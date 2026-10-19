---
name: historias
description: Fase 2.5 del proceso spec-driven - desglosa las funcionalidades de docs/SPEC.md en características (features) e historias de usuario con criterios de aceptación Dado/Cuando/Entonces, en docs/BACKLOG.md. Usar después de disenar y antes de construir, o cuando el usuario diga "historias", "backlog", "características" o "desglosar".
---

# Fase 2.5 — Historias: de la spec al backlog

Actuá como analista que propone; el usuario valida. El backlog traduce el contrato a unidades de trabajo: **características** (features) que agrupan **historias de usuario**, cada una con criterios de aceptación que después se vuelven tests.

## Proceso

1. Leé `docs/SPEC.md` y `docs/ARCHITECTURE.md`. Si faltan, detenete y pedí las fases previas.
2. Proponé una **característica** por cada funcionalidad de la spec (id `F1`, `F2`, …). Nada que no esté en la spec: si al desglosar aparece algo nuevo, frená y preguntá si se actualiza la spec primero.
3. Desglosá cada característica en **historias** con este formato:
   - *"Como \<rol\>, quiero \<acción\>, para \<beneficio\>"* — el rol es un usuario real de la app, no "el sistema".
   - **Criterios de aceptación** en Dado/Cuando/Entonces: entre 2 y 5 por historia, describiendo **comportamiento observable**, nunca implementación. Incluí al menos un criterio de borde o error (qué pasa cuando sale mal), no solo el camino feliz.
   - Tamaño: una historia se construye en una sesión. Si no entra, partila.
4. Validá el desglose con el usuario **historia por historia**: él corrige roles, prioridades y criterios. Nada queda sin su OK.
5. Escribí `docs/BACKLOG.md`:

```markdown
# Backlog — <proyecto>
> Generado desde SPEC v<N>. Estados por historia: pendiente → en construcción → construida (pendiente de revisión) → revisada ✓

## F1 — <característica>

### F1-H1 — <título corto> · `pendiente`
Como <rol>, quiero <acción>, para <beneficio>.

**Criterios de aceptación:**
- [ ] Dado <contexto>, cuando <acción>, entonces <resultado>.
- [ ] Dado <caso de error>, cuando <acción>, entonces <resultado seguro>.
```

6. Orden del backlog = orden de construcción, decidido por el usuario (valor primero, dependencias después).
7. Commit: `docs: backlog v<N>`.
8. Cerrá indicando el siguiente paso: `construir`, que desde ahora toma historias como unidad de trabajo (las piezas técnicas de base de `docs/PIECES.md` — modelo de datos, runner de tests — van antes de la primera historia).

## Mantenimiento del backlog

Cuando la spec cambie (vía `especificar` o un desvío aceptado), el backlog se actualiza en el mismo commit de docs: historias nuevas entran `pendiente`, las que quedaron fuera del contrato se marcan `descartada` con una línea de porqué — no se borran.
