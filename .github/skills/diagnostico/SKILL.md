---
name: diagnostico
description: Paso 0 para proyectos existentes - recorre el proyecto JUNTO al usuario, evalúa si está bien armado (estructura, tests, seguridad, explicabilidad) y recomienda la ruta de entrada al proceso spec-driven. Usar cuando el usuario quiera "ver el proyecto juntos", "analizar si está bien armado", "diagnóstico" o antes de adoptar.
---

# Paso 0 — Diagnóstico: ¿está bien armado este proyecto?

Este skill se usa **antes** de `adoptar`: es la mirada conjunta sobre un proyecto existente (un prototipo, un desarrollo heredado, algo vibecodeado) para decidir con datos si se gradúa, se adopta, se queda desechable o se reescribe. Acá **no se corrige nada**: se observa, se conversa y se escribe un informe.

## Parte 1 — Exploración (el agente, solo)

Recorré el proyecto y relevá, con evidencia concreta (`archivo:línea`, conteos reales):

1. **Mapa**: estructura de carpetas, puntos de entrada, qué hace la aplicación según el código (no según lo que el usuario recuerde).
2. **Stack y dependencias**: qué usa, versiones, dependencias que no se usan o que duplican función.
3. **Tests**: ¿hay runner configurado? ¿cuántos tests? ¿pasan? Corré la suite si existe y mostrá la salida real.
4. **Seguridad**: secretos hardcodeados, entrada sin validar, inyección posible, permisos amplios. Lo mismo que busca `revisar`, pero a vuelo de pájaro.
5. **Consistencia**: ¿el código parece de una sola mano o de muchas sesiones sin dirección? Nombres, patrones repetidos de forma distinta, código muerto, TODOs.

## Parte 2 — Análisis conjunto (con el usuario, área por área)

No tires un informe de una vez: recorré el proyecto **con** el usuario, un área por mensaje, y en cada una:

- Mostrá lo que encontraste (bueno y malo) con ejemplos concretos del código.
- Preguntá la intención: *"¿esto lo decidiste vos o salió así?"* — distingue diseño de accidente, que es la diferencia entre deuda asumida y deuda invisible.
- Preguntá qué quiere conservar: a veces una parte "fea" es la que valida la idea y se conserva; una parte "linda" no se usa y se borra.

El criterio de fondo son las preguntas del proceso: ¿qué pasa con un dato inesperado?, ¿hay algo inseguro?, ¿puede el usuario explicar cada parte a otra persona?

## Parte 3 — Informe y ruta

Escribí `docs/DIAGNOSTICO.md`:

```markdown
# Diagnóstico — <proyecto> · <fecha>

## Qué hace hoy (según el código)

## Lo que está bien armado
- <con evidencia>

## Deuda y riesgos
| Hallazgo | Gravedad | Dónde |
|----------|----------|-------|

## Tests
<runner, cantidad, resultado real de la suite>

## Veredicto
<una de las cuatro rutas, con el porqué>

## Plan de adopción propuesto
<pasos concretos y orden>
```

Las cuatro rutas posibles (recomendá una, decide el usuario):

1. **Adoptar directo** (skill `adoptar`): el proyecto está razonable; spec al revés, piezas heredadas, auditoría oportunista.
2. **Graduar** (sección Graduación del skill `prototipo`): era un prototipo y quiere producción; adopción + auditoría completa de TODO antes de usuarios o datos reales.
3. **Sigue desechable**: cumple su función de prototipo y no cruza la línea roja; se le agrega `DESECHABLE.md` y no se invierte más.
4. **Rescatar y reescribir**: la idea está validada pero el código no se salva; la spec al revés se escribe igual (eso se rescata: el aprendizaje) y se reconstruye por las fases 2-4.

El plan de adopción dice además cómo **adaptar el sistema a este proyecto**: dónde copiar `AGENTS.md` y `.github/skills/`, cuál sería la pieza 1 (casi siempre el runner de tests), qué piezas heredadas auditar primero y qué partes conviene dejar morir.

Commit del informe: `docs: diagnóstico inicial`. La decisión de ruta es del usuario; con su elección, el siguiente paso es el skill que corresponda.
