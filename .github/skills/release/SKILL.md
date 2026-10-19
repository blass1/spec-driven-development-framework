---
name: release
description: Cierre de versión del proceso spec-driven - verifica que las historias de la versión estén revisadas y la suite en verde, propone el bump semver leyendo los conventional commits, actualiza CHANGELOG.md y crea el tag anotado. Usar cuando el usuario diga "release", "cerrar versión", "taggear" o "publicar versión".
---

# Release — cerrar y taggear una versión

Un tag es una promesa: "esto se puede instalar". Este skill es el checklist que impide taggear promesas rotas. Solo se taggea `main`, solo en verde.

## Proceso

1. **Precondiciones** — verificá y, si alguna falla, listá lo que falta y detenete:
   - Estás en `main`, actualizado (`git pull`), con el working tree limpio.
   - En modo `equipo`: no quedan PRs de la versión sin mergear.
   - En `docs/BACKLOG.md` no hay historias de esta versión en `en construcción` ni `construida (pendiente de revisión)`: todas `revisada ✓` (las que no llegaron se mueven explícitamente a la próxima versión, con OK del usuario).
   - `docs/PIECES.md` sin piezas `construida (pendiente de revisión)`.
2. **Suite completa en verde.** Mostrá la salida real. En rojo no hay release, sin excepciones.
3. **Proponé el bump** leyendo los commits desde el último tag (`git describe --tags --abbrev=0` y `git log <último-tag>..HEAD --oneline`):
   - Solo `fix:`/`chore:`/`docs:` → **PATCH** (vX.Y.Z+1).
   - Algún `feat:` → **MINOR** (vX.Y+1.0).
   - Algo rompe comportamiento que ya existía (la SPEC cambió de forma incompatible) → **MAJOR** (vX+1.0.0).
   - Si no hay ningún tag todavía, proponé `v0.1.0` (o `v1.0.0` si la spec v1 está completa y revisada). **El usuario aprueba o corrige el número — la decisión es suya.**
4. **Actualizá `CHANGELOG.md`** (crealo si no existe) agregando arriba:

```markdown
## v<X.Y.Z> — <fecha>
### Agregado
- <historias feat, en lenguaje de usuario, no de commit>
### Corregido
- <fixes>
### Cambiado
- <refactors/perf visibles>
```

5. **Cerrá**, solo con el OK explícito del usuario:
   - Commit: `chore: release v<X.Y.Z>` (el changelog y cualquier bump de versión en manifiestos del proyecto).
   - Tag anotado: `git tag -a v<X.Y.Z> -m "<una línea resumiendo la versión>"` — anotado siempre, lightweight nunca.
   - `git push && git push --tags`.
6. Anotá en `docs/BACKLOG.md` la versión junto a las historias que salieron (p. ej. `revisada ✓ · v1.1.0`), así el backlog cuenta qué salió cuándo.

## Reglas duras

- Un tag publicado no se mueve ni se borra: si la versión salió mal, se arregla con un PATCH nuevo.
- No se taggea con historias a medias, suite en rojo o working tree sucio — el checklist no se negocia.
