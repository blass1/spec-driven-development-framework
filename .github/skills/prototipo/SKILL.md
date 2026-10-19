---
name: prototipo
description: Excepción al proceso spec-driven - modo vibecode. Marca el proyecto como desechable (DESECHABLE.md) y lo libera de las 4 fases. Usar cuando el usuario diga "prototipo", "vibecode", "algo rápido desechable" o similar.
---

# Excepción — Prototipo desechable (vibecodear con permiso)

Hay casos donde el proceso completo no vale la pena. Este skill lo deja **registrado y acotado**.

## Proceso

1. Verificá que aplique alguna excepción legítima:
   - Un prototipo desechable para validar una idea en una tarde.
   - Un script desechable (convertir ficheros, migrar datos una vez).
   - Explorar una librería nueva para ver cómo se siente.
   - Código que no va a vivir más que unos días y donde no hay usuarios ni dinero en juego.
2. **La línea roja** — si cualquiera de estas es cierta, NO aplica la excepción:
   - Va a tener usuarios.
   - Va a manejar datos reales.
   - Va a haber que mantenerlo a lo largo de meses.

   En ese caso respondé que esto necesita el proceso completo y que el primer paso es la fase 1 (skill `especificar`).
3. Si aplica, creá `DESECHABLE.md` en la raíz del proyecto:

```markdown
# ⚠️ CÓDIGO DESECHABLE
- **Qué es:** <descripción>
- **Por qué es desechable:** <la excepción que aplica>
- **Fecha:** <hoy>

Este código NO pasó por el proceso spec-driven y no debe ir a producción.
Si sobrevive y va a tener usuarios, datos reales o mantenimiento:
graduarlo con el skill `adoptar` (spec al revés + auditoría de lo heredado).
```

4. Con ese archivo presente, construí rápido y sin ceremonia: sin spec, sin piezas, sin auditoría. Priorizá velocidad de aprendizaje.
5. Si durante el trabajo detectás que se cruzó la línea roja (aparecen usuarios, datos reales, o "esto lo dejamos andando"), avisá de inmediato y proponé graduarlo.

## Graduación: cuando el prototipo salió demasiado bien

Un prototipo que quiere sobrevivir no se bendice: se **gradúa**, y el camino es el skill `adoptar` (el prototipo es un caso particular de proyecto ya empezado):

1. Correr `adoptar`: spec reconstruida desde el código (validada por el usuario), arquitectura as-is con su deuda anotada, todo el código existente como `heredada (sin auditar)` en `docs/PIECES.md`.
2. **Diferencia con una adopción normal:** el código vibecodeado no tiene ninguna garantía, así que acá la auditoría NO es oportunista — antes de que entre un solo usuario o dato real, cada pieza heredada pasa por `revisar` en sesión limpia. Lo que no pasa, se reescribe por `construir`. El runner de tests es la primera pieza nueva.
3. Recién cuando todas las piezas quedaron `revisada ✓`, se borra `DESECHABLE.md`. Ese es el acto de graduación: de ahí en más rigen las reglas normales.

Graduar suele ser más barato que reescribir de cero — el prototipo ya validó la idea y el diseño — pero solo si la auditoría es honesta: un prototipo "muy bien armado" sin tests ni revisión es una sensación, no un hecho.
