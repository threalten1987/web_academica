## ADDED Requirements

### Requirement: Menú horizontal en pantallas grandes

El sitio SHALL mostrar el menú de navegación (`.nav-menu`) como una barra horizontal visible en todas las páginas cuando el ancho del viewport sea igual o superior al breakpoint definido (768px). En este modo, el botón hamburguesa (`.menu-icon`) MUST permanecer oculto.

#### Scenario: Visualización en escritorio

- **WHEN** el usuario abre cualquier página del sitio con un viewport de 768px o más de ancho
- **THEN** el menú de navegación se muestra en horizontal con todos los enlaces visibles y el botón hamburguesa no se muestra

#### Scenario: Navegación entre páginas en escritorio

- **WHEN** el usuario pulsa un enlace del menú con un viewport de 768px o más
- **THEN** el navegador navega a la página destino del enlace sin que el estado del menú cambie

### Requirement: Menú hamburguesa en pantallas pequeñas

El sitio SHALL ocultar el `.nav-menu` por defecto y SHALL mostrar un botón hamburguesa (`.menu-icon`) en el header cuando el ancho del viewport sea inferior a 768px. Al activar el botón, el menú MUST desplegarse en vertical mostrando todos los enlaces; al desactivarlo, el menú MUST volver a ocultarse.

#### Scenario: Menú colapsado por defecto en móvil

- **WHEN** el usuario abre cualquier página del sitio con un viewport menor a 768px de ancho
- **THEN** el menú de navegación está oculto y el botón hamburguesa es visible en el header

#### Scenario: Despliegue del menú en móvil

- **WHEN** el usuario pulsa el botón hamburguesa con un viewport menor a 768px
- **THEN** el menú de navegación se despliega en vertical mostrando todos los enlaces (Inicio, Publicaciones, Docencia, Investigación, CV)

#### Scenario: Colapso del menú en móvil

- **WHEN** el usuario pulsa de nuevo el botón hamburguesa con el menú desplegado
- **THEN** el menú de navegación se oculta

### Requirement: Toggle sin JavaScript

El mecanismo de despliegue/colapso del menú SHALL implementarse únicamente con HTML y CSS, mediante un checkbox oculto (`#nav-toggle`) asociado a un label (`.menu-icon`), sin requerir JavaScript.

#### Scenario: Funcionamiento sin JavaScript

- **WHEN** el usuario visita cualquier página con JavaScript deshabilitado y viewport menor a 768px
- **THEN** el botón hamburguesa sigue desplegando y colapsando el menú correctamente

### Requirement: Consistencia del menú entre páginas

Todas las páginas del sitio (`index.html`, `publications.html`, `teaching.html`, `research.html`) SHALL incluir el mismo marcado del header/nav con el toggle hamburguesa y MUST compartir la misma hoja de estilos, de modo que el comportamiento responsive sea idéntico en todas ellas.

#### Scenario: Comportamiento idéntico en todas las páginas

- **WHEN** el usuario abre cualquiera de las 4 páginas del sitio con un viewport menor a 768px
- **THEN** todas muestran el botón hamburguesa y el menú se despliega/colapsa de la misma forma

### Requirement: Accesibilidad del toggle

El botón hamburguesa SHALL ser operable con teclado (el checkbox es focusable y activable con espacio/Enter vía su label asociado) y SHALL tener un indicador visual de foco. El label MUST estar programáticamente asociado al checkbox.

#### Scenario: Navegación por teclado

- **WHEN** el usuario navega con Tab hasta el botón hamburguesa y pulsa espacio o Enter
- **THEN** el menú se despliega o colapsa y el estado de foco es visible

#### Scenario: Foco visible

- **WHEN** el checkbox `#nav-toggle` recibe el foco por teclado
- **THEN** el icono hamburguesa muestra un indicador visual de foco (outline o estilo equivalente)
