# test_distributed_systems

Proyecto de práctica del flujo **dev → qa → main**. Cada paso deja un cambio en este archivo y se integra mediante **Pull Request**.

## Ramas base

### `main`
Rama de producción: solo código estable listo para usuarios.

### `dev`
Rama de desarrollo / integración. Aquí aterrizan las features antes de pasar a pruebas.

### `qa`
Rama de quality assurance / staging. Aquí se valida lo que viene de `dev` antes de producción.

## Flujos

### Feature (`feature/*`)
- Se crea desde `dev`
- Se integra a `dev` mediante PR
- Ejemplo: PR #1 (`feature/documentar-feature-flow` → `dev`)

### Promoción a QA (`dev` → `qa`)
- Cuando el trabajo en `dev` está listo para pruebas, se abre PR de `dev` hacia `qa`
- En `qa` se valida funcionalidad, regresiones y criterios de aceptación

### Promoción a producción (`qa` → `main`)
- Cuando QA aprueba, se abre PR de `qa` hacia `main`
- `main` queda con la versión estable publicada

### Release (`release/*`) — adaptado a `dev` / `qa` / `main`
- Se crea desde `dev` cuando el conjunto de cambios está listo para versionar (ej. `release/1.0.0`)
- No se agregan features nuevas: solo fixes menores, versión y documentación final
- Flujo de cierre con las tres ramas:
  1. PR `release/*` → `qa` (validar el candidato a release en QA)
  2. PR `release/*` → `main` (publicar en producción + tag de versión, ej. `v1.0.0`)
  3. PR `release/*` → `dev` (devolver a desarrollo los ajustes hechos en la release)
- `qa` sigue siendo la rama permanente de ambiente; `release/*` es temporal y se elimina al terminar

### Hotfix (`hotfix/*`)
- Se crea desde `main` ante un incidente en producción
- Se integra a `main` mediante PR
- Luego se propaga el fix a `qa` y `dev` con PRs para no perder el cambio
- Ejemplo: rama `hotfix/documentar-hotfix` documenta este flujo en el README
  1. PR hotfix → `main`
  2. PR `main` → `qa` (o hotfix → `qa`)
  3. PR `main` → `dev` (o hotfix → `dev`)
