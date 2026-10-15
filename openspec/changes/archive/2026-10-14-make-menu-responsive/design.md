## Context

Sitio web personal estático (HTML + CSS, sin JavaScript ni build) con 4 páginas (`index.html`, `publications.html`, `teaching.html`, `research.html`) que comparten un header con `.navbar` y `.nav-menu` horizontal. El menú no se adapta a pantallas pequeñas. `styles.css` ya contiene la regla `#nav-toggle, .menu-icon { display: none; }`, resto de una intención previa de implementar un menú hamburguesa con la técnica del checkbox.

## Goals / Non-Goals

**Goals:**

- Menú usable en móviles: botón hamburguesa que despliega/colapsa el `.nav-menu` en vertical bajo 768px.
- Mantener intacto el comportamiento actual en escritorio (≥768px).
- Sin JavaScript: toggle 100% HTML + CSS (checkbox hack), coherente con la naturaleza estática del sitio.
- Marcado del header idéntico en las 4 páginas.
- Accesibilidad básica del toggle: label asociado, foco visible, operable con teclado.

**Non-Goals:**

- No se rediseña el resto del layout responsive (hero, columnas, tablas, etc.); solo el menú.
- No se añade JavaScript, framework ni animaciones complejas.
- No se cambian los enlaces ni el contenido del menú.
- No se reestructura el footer ni el contenido de las páginas.

## Decisions

### 1. Checkbox hack en lugar de JavaScript

Se usa un `<input type="checkbox" id="nav-toggle">` oculto + `<label class="menu-icon" for="nav-toggle">`, y CSS con el selector `#nav-toggle:checked ~ .nav-menu` para desplegar el menú.

- **Por qué**: el sitio no tiene JavaScript; añadirlo solo para el menú sería una dependencia innecesaria. Los selectores `#nav-toggle`/`.menu-icon` ya existen en el CSS, lo que confirma esta dirección.
- **Alternativa considerada**: botón `<button>` + JS con `classList.toggle`. Se descarta por introducir JS y por requerir gestión de `aria-expanded` manual.
- **Coste aceptado**: accesibilidad menos rica que un botón con ARIA (el checkbox no comunica "expandido/colapsado" a lectores de pantalla). Se mitiga manteniendo el checkbox focusable (oculto visualmente pero no con `display: none` en móvil... ver Decisión 3) y el label asociado.

### 2. Breakpoint en 768px con mobile-first opcional

Media query `@media (max-width: 767px)` que colapsa el menú; el CSS actual de escritorio queda como caso base.

- **Por qué**: 768px es el punto estándar tablet/móvil y minimiza cambios al CSS existente (solo se añade un bloque de media query, no se reescribe el caso base).
- **Alternativa considerada**: enfoque mobile-first reescribiendo el caso base. Se descarta por tocar más reglas existentes y aumentar el riesgo de regresiones en escritorio.

### 3. Ocultar el checkbox sin `display: none` en móvil

En el breakpoint móvil, `#nav-toggle` se oculta visualmente (p. ej. `position: absolute; opacity: 0; width/height` solapando el icono o técnica de "visually hidden") en vez de `display: none`, para que siga siendo focusable por teclado y el menú sea operable sin ratón.

- **Por qué**: `display: none` elimina el checkbox del orden de tabulación y rompe la operación por teclado.
- **Alternativa considerada**: mantener `display: none` y confiar solo en el label. Se descarta porque el label no es focusable por defecto y la navegación por teclado quedaría rota.

### 4. Menú desplegable en flujo, no overlay

Al desplegarse, el `.nav-menu` se muestra como lista vertical dentro del header (el header crece), en `position: static`/flujo normal dentro del sticky header.

- **Por qué**: el header ya es `position: sticky`; un menú en flujo evita problemas de superposición, `z-index` y scroll que tendría un overlay `position: absolute/fixed`.
- **Alternativa considerada**: overlay absoluto bajo el header. Descartado por complejidad innecesaria para 5 enlaces.

### 5. Marcado compartido replicado en las 4 páginas

El nuevo bloque de header (checkbox + label + estructura del nav) se copia idéntico en las 4 páginas. No hay sistema de plantillas ni includes en el proyecto, así que la duplicación se mantiene como está hoy.

- **Por qué**: añadir un build o includes para esto estaría fuera de alcance.

## Risks / Trade-offs

- [Duplicación del marcado del header en 4 archivos] → Aceptada por coherencia con el estado actual; las tareas incluyen verificar las 4 páginas por igual.
- [Accesibilidad limitada del checkbox hack frente a `<button>` + ARIA] → Mitigada con label asociado, foco visible y operación por teclado; si en el futuro se añade JS, se puede migrar a un botón con `aria-expanded`.
- [El checkbox puede quedar "checked" al redimensionar de móvil a escritorio] → Sin efecto visible: en ≥768px el menú siempre se muestra y el icono está oculto; no hay comportamiento roto.
- [Hover styles actuales (`.nav-item:hover` con fondo `#D11A5B`) pueden verse distintos en la lista vertical] → Se revisan dentro de la media query para que el item ocupe todo el ancho clickable.

## Migration Plan

1. Añadir el marcado del toggle (checkbox + label) al header de las 4 páginas.
2. Añadir la media query y ajustar la regla `#nav-toggle, .menu-icon` en `styles.css`.
3. Verificar manualmente en navegador: ≥768px sin cambios; <768px despliegue/colapso, teclado y foco; en las 4 páginas.

Rollback: revertir los cambios en los 5 archivos (sitio estático, sin despliegue automatizado).

## Open Questions

- Icono del botón: ¿hamburguesa dibujada con CSS (spans/borders) o carácter "☰"? Se propone carácter "☰" dentro del label por simplicidad; puede cambiarse en implementación sin afectar al diseño.
