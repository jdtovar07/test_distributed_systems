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

### Hotfix (`hotfix/*`)
- Se crea desde `main` ante un incidente en producción
- Se integra a `main` mediante PR
- Luego se propaga el fix a `qa` y `dev` con PRs para no perder el cambio
