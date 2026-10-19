---
name: adoptar
description: Adopción del proceso spec-driven en un proyecto YA empezado - reconstruye la spec desde el código existente, documenta la arquitectura real y marca las piezas heredadas. Usar cuando el usuario quiera sumar este flujo a un desarrollo existente, o diga "adoptar", "sumar el proceso", "onboarding".
---

# Adoptar — sumar el proceso a un proyecto existente

En un proyecto empezado no se especifica hacia adelante: se **reconstruye la spec desde el código** (de código a contrato), se documenta la arquitectura como ES (no como debería ser), y lo ya construido entra como herencia que se audita de a poco, no de golpe.

## Proceso

### 1. Spec al revés

1. Explorá el código en serio: estructura, entradas/salidas, modelos de datos, dependencias, configuración.
2. Redactá un **borrador** de `docs/SPEC.md` con lo que el código efectivamente hace hoy: qué hace en una frase, funcionalidades existentes, datos que maneja, stack real. Marcá con `(?)` todo lo que no estés seguro.
3. Revisalo con el usuario punto por punto — él valida, vos proponés. En particular: ¿hay funcionalidades a medio hacer? Van a "Fuera de alcance (todavía NO)". ¿Hay cosas que el código hace pero nadie quiere? Se anotan para eliminar.
4. Con su OK, el documento deja de ser borrador y pasa a ser **el contrato**.

### 2. Arquitectura como es (as-is)

1. Escribí `docs/ARCHITECTURE.md` describiendo la arquitectura ACTUAL, sin embellecerla. En "Por qué": "heredada — anterior a la adopción del proceso".
2. Agregá una sección `## Deuda detectada` con los problemas que viste al explorar (sin corregirlos ahora): acoplamiento, falta de tests, secretos en código, etc. Es un inventario, no un plan de refactor.

### 3. Piezas heredadas

1. Partí el código existente en piezas con la misma lógica que usaría la fase 2, y volcálas en `docs/PIECES.md` con el estado **`heredada (sin auditar)`**.
2. **No se audita todo de golpe**: la auditoría es oportunista. Cada vez que el mantenimiento (skill `mantener`) toque una pieza heredada, esa pieza pasa entera por `revisar` y cambia de estado. Las piezas calientes se auditan solas con el uso; las que nadie toca pueden esperar.
3. Si el proyecto no tiene runner de tests, configurarlo es la **primera pieza nueva** de `docs/PIECES.md` — sin eso, ni `mantener` ni `revisar` funcionan.

### 4. Cierre

1. Copiá a este proyecto el `AGENTS.md` y los `.github/skills/` de la plantilla (si no están ya).
2. Commit: `docs: adopción del proceso spec-driven` (los docs y skills juntos; nada de código en este commit).
3. A partir de acá rigen las reglas normales: funcionalidad nueva → `construir`/`revisar`; bugs y ajustes → `mantener`.

## Reglas de esta fase

- En esta fase **no se corrige código**, por tentador que sea: solo se observa, documenta y clasifica. Las correcciones salen después por `mantener`, con su test y su commit.
- La spec reconstruida documenta lo que HAY, no lo que te gustaría que haya. Los deseos van a "Fuera de alcance (todavía NO)".
