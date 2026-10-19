---
name: especificar
description: Fase 1 del proceso spec-driven - entrevista corta que produce docs/SPEC.md, el contrato del proyecto. Usar al arrancar un proyecto o una nueva versión, o cuando el usuario diga "especificar", "hagamos la spec" o "fase 1".
---

# Fase 1 — Especificar

Actuá como entrevistador. NO escribas código, NO propongas arquitectura, NO elijas tecnología por tu cuenta. Esta fase dura de 10 minutos a 1 hora, nunca más.

La especificación es el **contrato** entre el usuario y el agente: si en cualquier fase posterior el trabajo se desvía, se vuelve a este documento.

## Proceso

1. Si ya existe `docs/SPEC.md`, leelo primero y preguntá si esto es una revisión de la spec actual o una nueva versión.
2. Entrevistá al usuario, **una pregunta a la vez**, en este orden:
   - **A. ¿Qué hace la aplicación, en UNA frase?** Si la respuesta necesita dos frases, ayudá a recortar hasta que entre en una.
   - **B. ¿Qué funcionalidades tiene ESTA versión?** Y con igual importancia: **¿cuáles NO tiene todavía?** La lista de "fuera de alcance" es obligatoria y explícita.
   - **C. ¿Qué datos maneja y qué tecnología quiere usar?** Entidades principales, de dónde vienen los datos, y el stack. Si el usuario no tiene stack decidido, anotalo como pregunta abierta para la fase de diseño — no lo decidas vos.
3. Repreguntá todo lo ambiguo. Si el usuario amplía el alcance mientras habla, ayudalo a **cerrar** alcance, no a crecerlo: lo que no entre en esta versión va a "todavía no".
4. Escribí `docs/SPEC.md` con exactamente esta estructura:

```markdown
# SPEC — <nombre del proyecto> · v<N>
> Este documento es el contrato. Si el trabajo se desvía de lo escrito acá, se vuelve acá.

## Qué hace (una frase)

## Funcionalidades de esta versión
- [ ] ...

## Fuera de alcance (todavía NO)
- ...

## Datos

## Tecnología

## Preguntas abiertas
```

5. Mostráselo al usuario y pedí confirmación explícita. Solo con su OK: commit `spec: v<N>` (si no es repo git, ofrecé `git init` primero).
6. Cerrá indicando el siguiente paso: la fase 2 (skill `disenar`).
