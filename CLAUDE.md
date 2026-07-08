# CarRenting_FE

Frontend del proyecto de alquiler de coches. Angular 19 con SSR. Repo Git independiente (ejecuta comandos `ng`/`npm`/`git` desde esta carpeta).

## Estado actual: scaffold recién generado

Este repo es, a día de hoy, el resultado casi sin tocar de `ng new` (Angular CLI 19.1.7, `--ssr`). **No hay todavía código de negocio**: sin servicios, sin `environments/`, sin gestión de estado, sin autenticación, sin rutas definidas (`app.routes.ts` exporta un array `Routes` vacío) y sin más componentes que el `AppComponent` por defecto (con el markup de bienvenida de Angular CLI todavía sin borrar). Antes de asumir que existe algún patrón ya establecido en el código, comprueba que no sea simplemente boilerplate del CLI.

Cuando se empiece a construir sobre esto, hará falta decidir/crear (no lo des por hecho, pregunta o decide explícitamente):
- `src/environments/environment.ts` con la URL base de la API del backend (ver `CarRenting_BE`, corre en `https://localhost:7127` / `http://localhost:5075` en desarrollo).
- `provideHttpClient(...)` en `src/app/app.config.ts` (todavía no está registrado).
- Rutas reales en `app.routes.ts` (listado de coches, reservas, login, admin...).
- Librería de UI, gestión de estado y herramienta de lint — ninguna está elegida todavía.

## Stack y configuración

- **Angular 19.1** standalone (sin `NgModule` raíz), con **SSR habilitado** (`src/main.server.ts`, `src/server.ts` con Express, `outputMode: server`).
- **TypeScript estricto**: `strict: true` + `noImplicitOverride`, `noPropertyAccessFromIndexSignature`, `noImplicitReturns`, `noFallthroughCasesInSwitch`; `strictTemplates`/`strictInjectionParameters`/`strictInputAccessModifiers` en `angularCompilerOptions`. Mantén ese nivel de rigor en código nuevo.
- Sin path aliases configurados en los `tsconfig.*.json`.
- Estilos en **CSS plano** (no SCSS/Sass), un fichero por componente.
- `.editorconfig`: indentación de 2 espacios, comillas simples en `.ts`.
- Testing: **Karma + Jasmine** (`ng test`). No hay E2E configurado (ni Cypress ni Playwright).
- Sin ESLint/Prettier configurado — no hay target `lint` en `angular.json`.

## Comandos

Ejecutar siempre desde `CarRenting_FE/`:

```
npm start        # ng serve, http://localhost:4200
npm run build    # ng build -> dist/car-renting-fe
npm test         # ng test (Karma/Jasmine)
```

## Backend

La API vive en el repo hermano `CarRenting_BE` (accesible vía `../CarRenting_BE`, ya permitido en `.claude/settings.json`). Sin autenticación implementada todavía en ningún lado del stack — no añadas guards/interceptors de auth en el FE sin que exista primero soporte real en el backend.
