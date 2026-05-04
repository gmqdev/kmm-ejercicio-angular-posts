# Guía de Estilo y Desarrollo

## 1. Stack Tecnológico Obligatorio

- **Orquestador:** Nx Monorepo para la gestión de proyectos y caché de tareas.
- **Framework:** Angular Moderno (versión estable más reciente).
- **Detección de Cambios:** Modo Zoneless experimental activado.
- **Reactividad:** Uso estricto de Signals, Signal Forms y httpResource.
- **Rendimiento:** Implementación de @defer para carga diferida y lazy loading por ruta.
- **CSS:** TailwindCSS + daisyUI con enfoque Mobile First.
- **i18n:** Internacionalización obligatoria (es/en) mediante ngx-translate o Transloco.

## 2. Arquitectura: Screaming Architecture via Nx

Toda la funcionalidad debe estar encapsulada en librerías dentro de `libs/`. No desarrollar lógica de negocio en la carpeta `apps/`.

### Tipos de Librerías (Estructura de Dominios)

- **`libs/[dominio]/feature-[nombre]`**: Componentes inteligentes (contenedores), gestión de estado y rutas.
- **`libs/[dominio]/ui-[nombre]`**: Componentes presentacionales puros (dumb components).
- **`libs/[dominio]/data-access`**: Servicios, httpResource, signals de estado y modelos.
- **`libs/[dominio]/utils`**: Funciones puras, helpers o guards específicos del dominio.
- **`libs/shared/[tipo]`**: Recursos transversales (UI global, interceptores, utilidades genéricas).

## 3. Identidad Visual y UI

### Paleta de Colores

- **Primary Blue (#0053DC)**: Color para botones principales, estados activos y paginación.
- **Background (#F7F9FB)**: Color de fondo general de la aplicación.
- **Surface / Card (#FFFFFF)**: Fondo de tarjetas de posts y contenedores principales.
- **Heading Text (#2A3439)**: Títulos principales (H1, H2) y texto de alto contraste.
- **Secondary Text (#566166)**: Texto de párrafos, etiquetas y placeholders.
- **Input / Muted (#F0F4F7)**: Fondo de campos de texto, selectores y tarjetas secundarias.

### Tipografía y UX

- **Fuente Principal:** 'Inter' (800 para títulos, 400-600 para cuerpo).
- **Heading 1**: 36px, Semi-bold/Bold, Letter-spacing -0.9px.
- **Post Cards**: Padding de 32px, Border-radius de 8px, sin bordes (solo sombras sutiles o cambios de tono).
- **UX**: Estados visuales explícitos para `loading`, `empty`, `error` y `forbidden`.

## 4. Calidad y Flujo de Trabajo

- **Linter**: ESLint con reglas de Angular y Nx.
- **Formateo**: Prettier (2 espacios, comillas simples).
- **Git**: Mensajes siguiendo la convención de Conventional Commits.
- **Testing**:
  - Unitarios: Vitest + Testing Library.
  - E2E: Playwright para flujos críticos (Login, CRUD).
- **Automatización**: Uso de Husky y lint-staged para validación pre-commit.

## 5. Flujo de Validación de Cambios (Protocolo Nx Affected)

Para asegurar la calidad antes de cada commit, se debe seguir este proceso automatizado:

1. **Escanear Cambios**: Identificar solo los proyectos afectados por las modificaciones actuales.

    ```bash
   npx nx affected --target=test --base=main
   ```

2. **Ejecutar Validación**:
    - **Formateo y Reglas**: `npx nx format:write` y `npx nx affected --target=lint`.
    - **Pruebas Unitarias**: `npx nx affected --target=test --watch=false`.

3. **Confirmación**: Si todos los pasos devuelven éxito, el código es apto para commit.

## 6. Comandos Preferidos

- **Generar lib**: `npx nx g @nx/angular:library [nombre] --directory=libs/[dominio] --standalone`.
- **Ejecución**: `npx nx serve`.
- **Validación**: `npx nx affected --target=test` o `lint`.
