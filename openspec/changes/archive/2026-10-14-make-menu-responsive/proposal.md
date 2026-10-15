## Why

El menú de navegación del sitio (`.navbar` / `.nav-menu`) es una barra horizontal fija que no se adapta a pantallas pequeñas: en móviles los enlaces se comprimen, desbordan o resultan difíciles de pulsar. El CSS ya contiene los selectores `#nav-toggle` y `.menu-icon` (ocultos con `display: none`), lo que indica que se planificó un menú tipo hamburguesa que nunca se implementó.

## What Changes

- Añadir un botón de menú hamburguesa visible solo en pantallas pequeñas (por debajo de un breakpoint, p. ej. 768px) en las 4 páginas: `index.html`, `publications.html`, `teaching.html`, `research.html`.
- En pantallas pequeñas, el `.nav-menu` se oculta por defecto y se despliega en vertical al activar el botón hamburguesa; al desactivarlo vuelve a ocultarse.
- En pantallas grandes el menú conserva su comportamiento horizontal actual y el botón permanece oculto.
- Implementación sin dependencias de JavaScript: se usará la técnica del checkbox oculto (`#nav-toggle`) + label (`.menu-icon`), aprovechando los selectores ya presentes en `styles.css`.
- Mejoras de accesibilidad del toggle: label asociado al checkbox, área táctil adecuada y foco visible.

## Capabilities

### New Capabilities

- `responsive-navigation`: comportamiento del menú de navegación del sitio en pantallas grandes y pequeñas, incluyendo el toggle hamburguesa, el despliegue/colapso del menú y los breakpoints aplicados.

### Modified Capabilities

(ninguna — no existen specs previas en `openspec/specs/`)

## Impact

- **Código afectado**: `index.html`, `publications.html`, `teaching.html`, `research.html` (marcado del header/nav) y `styles.css` (media queries y reglas del toggle).
- **Sin dependencias nuevas**: solo HTML + CSS, sin JavaScript ni librerías externas.
- **Sin cambios de contenido**: los enlaces del menú y su destino no cambian.
