# Sitio Web Académico - Javiera Araya-Moreno

Sitio web estático personal y académico para Javiera Araya-Moreno (investigadora postdoctoral). Desarrollado con HTML5 semántico y CSS3 puro con diseño responsive (soporte desktop y mobile mediante toggle CSS sin dependencias de frameworks externos ni JavaScript).

## Arquitectura y Componentes

El proyecto es un sitio web multi-página estático compuesto por las siguientes páginas y recursos principales:

*   [`index.html`](./index.html): Página principal (Home / Sobre Mí). Presenta la biografía profesional, filiación académica y contacto.
*   [`research.html`](./research.html): Sección de líneas de investigación organizadas con acordeón nativo HTML5 (`<details>` / `<summary>`).
*   [`teaching.html`](./teaching.html): Catálogo de docencia y cursos impartidos organizados en tarjetas (`.teaching-card`).
*   [`publications.html`](./publications.html): Listado exhaustivo de producción académica categorizada (artículos revisados por pares, capítulos de libros, traducciones, etc.).
*   [`styles.css`](./styles.css): Hoja de estilos global con variables CSS (`:root`), tipografías de Google Fonts (`Lato`, `Playfair Display`), diseño de grid/flexbox y navegación colapsable responsive por checkbox-hack.
*   [`img/`](./img/): Directorio de recursos estáticos multimedia (fotografías, íconos y logotipos SVG/PNG/JPEG).

### Especificaciones OpenSpec

*   [`openspec/specs/responsive-navigation/spec.md`](./openspec/specs/responsive-navigation/spec.md): Especificación de diseño y comportamiento del menú de navegación responsive accesible.

## Interface

### Páginas y Rutas Locales
*   `index.html`: Entrypoint raíz del sitio.
*   `research.html`: Vista de proyectos y líneas de investigación.
*   `teaching.html`: Vista de experiencia docente y cursos.
*   `publications.html`: Vista de publicaciones académicas indexadas y enlaces DOI.

### Elementos de Interfaz Compartidos
*   `.navbar`: Barra de navegación fija (`header` sticky con `z-index: 1000`).
*   `#nav-toggle` + `.menu-icon`: Checkbox-hack para menú responsive hamburguesa en pantallas `<= 768px`.
*   `.nav-menu`, `.nav-item`, `.nav-link`: Enlaces de navegación compartidos en todos los documentos HTML.
*   `#main-content`: Contenedor semántico principal de cada vista.
*   `footer`: Pie de página estático consistente.

## Invariants

*   **HTML puro**: No se requiere ni se incluye JavaScript para la interactividad del menú responsive ni para los desplegables; se utiliza el patrón CSS checkbox-hack (`#nav-toggle:checked ~ .nav-menu`) y `<details>/<summary>`.
*   **Consistencia de navegación**: Cada una de las 4 páginas HTML contiene la misma barra de navegación (`.navbar`) con los mismos enlaces cruzados relativos hacia las demás páginas y el enlace externo al CV en Google Drive.
*   **Mobile-first / Responsive**: Los breakpoints definidos en `styles.css` (`@media (max-width: 768px)` y `@media (max-width: 480px)`) garantizan la legibilidad y disposición fluida de tarjetas, menús y fuentes.

## Side Effects

*   El formulario interactivo del menú móvil modifica el estado visual en el DOM mediante el pseudo-selector `:checked` del input `#nav-toggle`.
*   Los enlaces de publicaciones y CV abren pestañas externas (`target="_blank"`).

## Verification

El proyecto es estático y no contiene un ejecutor de pruebas automatizado empaquetado. Para verificar visualmente y validar:

*   **Inspección en navegador**: Abrir cualquier archivo `.html` (p. ej. `index.html`) en un navegador web o servir mediante un servidor HTTP local (ej. `npx serve .` o Live Server).
*   **Validación de sintaxis**:
    ```bash
    # Validación W3C HTML / CSS (opcional vía herramientas locales o linter si estuviese instalado)
    ```
