## 1. Marcado HTML del toggle

- [x] 1.1 Añadir en `index.html` el `<input type="checkbox" id="nav-toggle">` y el `<label class="menu-icon" for="nav-toggle">☰</label>` dentro de `.navbar`, antes de `.nav-menu`
- [x] 1.2 Replicar el mismo marcado del header en `publications.html`
- [x] 1.3 Replicar el mismo marcado del header en `teaching.html`
- [x] 1.4 Replicar el mismo marcado del header en `research.html`
- [x] 1.5 Verificar que el marcado del header es idéntico en las 4 páginas

## 2. Estilos CSS del menú responsive

- [x] 2.1 Añadir en `styles.css` la media query `@media (max-width: 767px)`: ocultar `.nav-menu` por defecto y mostrar `.menu-icon`
- [x] 2.2 Añadir la regla `#nav-toggle:checked ~ .nav-menu` para desplegar el menú en vertical dentro del header (en flujo, sin overlay)
- [x] 2.3 Ocultar `#nav-toggle` visualmente sin `display: none` en el breakpoint móvil (visually hidden / opacity 0) para mantenerlo focusable
- [x] 2.4 Añadir indicador de foco visible sobre `.menu-icon` cuando `#nav-toggle` recibe foco (`:focus-visible` / `:focus`)
- [x] 2.5 Ajustar estilos del menú vertical: items a ancho completo, padding táctil adecuado y hover coherente con el estilo actual
- [x] 2.6 Confirmar que fuera de la media query (≥768px) no cambia ninguna regla existente del menú

## 3. Verificación

- [x] 3.1 Verificar en navegador con viewport ≥768px: menú horizontal visible, sin botón hamburguesa, sin regresiones visuales en las 4 páginas
- [x] 3.2 Verificar en navegador con viewport <768px: menú oculto por defecto, botón visible, despliegue/colapso al pulsarlo en las 4 páginas
- [x] 3.3 Verificar operación con teclado: Tab hasta el toggle, espacio/Enter despliega y colapsa, indicador de foco visible
- [x] 3.4 Verificar que el toggle funciona con JavaScript deshabilitado
- [x] 3.5 Ejecutar `openspec validate make-menu-responsive` para validar los artefactos del cambio
