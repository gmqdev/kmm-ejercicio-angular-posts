# Objetivo del Proyecto

Construir una SPA (Single Page Application) moderna con Angular para la gestión de `posts` y `comments` conectada a un backend mock de `json-server`.

## Estado Actual

- **Workspace:** Proyecto migrado exitosamente a **Nx Monorepo**.
- **Angular:** Versión moderna configurada dentro del monorepo.
- **Plugins:** Instalados `@nx/angular`, `@nx/eslint`, `@nx/vitest` y `@nx/playwright`.
- **Estilos:** TailwindCSS y daisyUI listos.
- **Backend:** Archivo `db.json` preparado para `json-server`.

## Requisitos Funcionales Críticos

- Sistema de autenticación con Login y protección de rutas (Guards).
- CRUD completo de Posts y Comentarios.
- Listado de posts con filtros reactivos (autor, etiquetas, búsqueda) y paginación.
- Solo los autores pueden editar o borrar su propio contenido (ownership).
- Internacionalización (i18n) en español e inglés.

## Flujo de Navegación

- `/login` -> Pantalla de acceso.
- `/posts` -> Listado principal con filtros.
- `/posts/new` -> Creación de contenido.
- `/posts/:id` -> Detalle con carga diferida (@defer) de comentarios.
- `/posts/:id/edit` -> Edición de contenido propio.
