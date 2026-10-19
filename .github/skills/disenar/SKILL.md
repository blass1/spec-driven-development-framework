---
name: disenar
description: Fase 2 del proceso spec-driven - propone exactamente 2 arquitecturas con pros y contras, el usuario decide, y produce docs/ARCHITECTURE.md y docs/PIECES.md. Usar cuando exista docs/SPEC.md y el usuario diga "diseñar", "arquitectura" o "fase 2".
---

# Fase 2 — Diseñar

Actuá como **consultor, no decisor**. Elegir la arquitectura es criterio y trabajo del usuario.

## Proceso

1. Leé `docs/SPEC.md` completo. Si no existe, **detenete** y pedí hacer la fase 1 (skill `especificar`) primero.
2. Proponé **exactamente 2** formas de estructurar el proyecto. Por cada opción:
   - Estructura: carpetas, módulos, y la lista tentativa de piezas a construir.
   - Ventajas concretas para ESTE proyecto (no genéricas).
   - Inconvenientes concretos.
   - En qué escenario conviene.
3. **DETENETE.** No elijas, no escribas código, no recomiendes salvo que el usuario te lo pida explícitamente. Esperá su decisión y su porqué.
4. Con la elección hecha, escribí `docs/ARCHITECTURE.md`:

```markdown
# Arquitectura — <proyecto>
> Decidida por <usuario> el <fecha>, sobre SPEC v<N>.

## Opción elegida: <nombre>

## Por qué (criterio del usuario)

## Opción descartada: <nombre>
```

5. Volcá la lista ordenada de piezas en `docs/PIECES.md`, todas en estado `pendiente`. **El modelo de datos es siempre la pieza 1.**

```markdown
| # | Pieza | Estado | Commit |
|---|-------|--------|--------|
| 1 | Modelo de datos | pendiente | |
```

6. Commit: `design: arquitectura elegida — <nombre>`.
7. Cerrá indicando el siguiente paso: la fase 2.5 (skill `historias`, para desglosar el backlog) o directamente la fase 3 (skill `construir`) si el proyecto es tan chico que no lo amerita — decisión del usuario.
