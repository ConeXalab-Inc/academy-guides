# CHANGELOG.md

## [0.38.0] — 2026-08-13

### Ajuste — Sistema tipográfico estandarizado de 4 tallas

- Se definen 4 tamaños de letra únicos y proporcionales al ancho del canvas (variables en `.canvas`):
  - `--fs-title: 3.45cqw` → `h1`, `h2`
  - `--fs-sub: 1.4cqw` → `h3`, `.lead`
  - `--fs-body: 1.05cqw` → `p`, `li`, `label`, `button`, `input`, `textarea`, `select`, `.step-list li`
  - `--fs-note: .8cqw` → `.gif-tag`, `.gif-caption`, `.nav-count`, `.status-line`, `.stage-caption`, `span` de `.briefing-meta`
- Normalizadas las tallas intermedias que existían (h3 1.65→1.4, flow-card h3 1.35→1.4, step-list 1.1→1.05, captions 0.66–0.92→0.8, etc.).
- `s8` (dense) pasa `gap` de 1.2 a .7cqw para ajustar sin tocar tamaños (el único slide que se desbordaba).

**Verificado:** ratios constantes de talla en 1280×720 (título 3.45%, sub 1.4%, texto 1.05%, nota 0.8% del ancho del canvas); 25 slides sin overflow en 1024×576, 1280×720, 1366×640, 1600×900 y 1920×1080; JS OK.


## [0.37.0] — 2026-08-13

### Ajuste — Escalado 100% proporcional a la pantalla

- Eliminados todos los `clamp(px, Xcqw, px)` (fuente base del `.canvas`, `h1`/`h2`/`h3`, `.lead`, `.image-placeholder`, `.scene-panel li`, `.scene-mission`, `.scene-img`, `.step-list li`, `.flow-card h3`): ahora todo usa `cqw` puro, por lo que textos, cajas, íconos y espaciados crecen/shrinken en la misma proporción que el canvas en cualquier resolución.
- `min-width`/`min-height` del `.canvas` pasan de 800×450 (que rompían el 16:9 en pantallas pequeñas) a 520×292 (proporcionales): sin deformación en ningún tamaño.
- Botones de control `.ctrl-btn` suben de 2.7 a 3cqw y su SVG de 56% a 64% (íconos de zoom/fullscreen/narración más visibles).

**Verificado:** ratios constantes (`lead` 1.4%, `h2` 3.45% del ancho del canvas) en 1024×576, 1280×720, 1600×900 y 1920×1080; sin overflow en s15/s17/s19/s21; relación de aspecto 1.778 en 800×450, 1366×640 y 2560×1440; JS OK.


## [0.1.0] — 2026-08-05

### Añadido
- Proyecto montado con `server.js` (Node.js nativo, sin dependencias) y `package.json`.
- Estructura de assets: `assets/img/` para imágenes de la guía.
- `AUDIT.md` con diagnóstico inicial completo.
- `CHANGELOG.md` para registro de cambios.
- `.gitignore` básico.

### Modificado
- `guia-algoritmos.html` → `index.html` (renombrado para servir como entrada).

---

## [0.2.0] — 2026-08-05

### Modificado — Slide 1: Briefing de misión

**Objetivo pedagógico:** Portada narrativa que presenta la experiencia y genera curiosidad.

**Cambios:**
- Restaurada estructura de dos columnas (texto izquierda / imagen derecha).
- Reemplazado el placeholder por `<img src="assets/img/portada.png">` con `alt` descriptivo.
- Añadida clase `.briefing-img` para darle estilo a la imagen (border-radius, width 100%).
- Fondo gradient original del briefing restaurado.

**CSS añadido:**
- `.briefing-img` — imagen responsive con border-radius.

**Verificado:**
- El slide mantiene proporción 16:9.
- La imagen `assets/img/portada.png` existe y es accesible.
- El `alt` text describe correctamente la escena.
- El servidor Node.js arranca correctamente.

---

## [0.3.0] — 2026-08-05

### Modificado — Slides 2, 3 y 4

**Slide 2**
- Imagen real integrada: `assets/img/ejemplo1.png`.
- Nota inferior de reto añadida en recuadro con ícono.
- Imagen reducida para evitar choque con el label superior.
- Texto de ejemplo actualizado.

**Slide 3**
- Concepto de algoritmo ampliado y ajustado para 10 años.
- Lista “Un algoritmo debe tener:” con 4 elementos.
- Pasos convertidos a un bloque compacto para ahorrar espacio vertical.
- Imagen real integrada: `assets/img/ejemplo2.png` y escalada +10%.

**Slide 4 — Laboratorio del minero (nivel 1)**
- Visual del mapa actualizado con `assets/img/mapa1.png`.
- Cuadrícula lógica superpuesta con códigos por celda (`B`, `F`, `R`, `X`).
- Minero con sprites por dirección:
  - `assets/img/mineroarr.png`
  - `assets/img/mineroaba.png`
  - `assets/img/mineroizq.png`
  - `assets/img/mineroder.png`
- Comandos de construcción con colores diferenciados:
  - Avanzar (verde), Izquierda (morado), Derecha (naranja).
- Cola del algoritmo compacta con íconos/flechas, sin texto descriptivo.
- Animación de caída mantenida (encoge y desaparece).
- Overlay de estado mejorado para éxito y game over.

---

## [0.4.0] — 2026-08-06

### Modificado — Slide 10: Laboratorio de programación en bloques (estilo Scratch)

**Objetivo pedagógico:** Reformar cómo se construye el algoritmo con un editor de bloques tipo Scratch.

**Cambios:**
- Izquierda: el juego sobre la cuadrícula se mantiene; debajo se añadieron controles al estilo Scratch:
  - Botón de **bandera verde** (circular) que ejecuta y reinicia el programa.
  - Botón de **detener** (octágono rojo) que detiene la ejecución.
- Derecha: nuevo editor de bloques:
  - Paleta superior con 3 bloques tipo Scratch: **Avanzar**, **Girar a la izquierda**, **Girar a la derecha**.
  - Los bloques usan el estilo visual de Scratch: forma redondeada con pestaña superior y conector inferior, color degradado y texto blanco en negrita.
  - Zona de programa donde los bloques se encajan uno con otro (apilado vertical tipo script).
  - Se arrastra una copia del bloque desde la paleta (drag & drop) o se hace clic para agregarlo.
  - Los bloques en la zona de programa se pueden reordenar por arrastre y eliminar con `×`.
- Se eliminó el sistema de 3 etapas (secuencia/bucle/condicional) y los bloques repetir/condicional; ahora es un minijuego único con los 3 bloques base.
- Se mantienen sonidos (`playPop`) por instrucción y el panel de depuración.

**CSS añadido:**
- `.scratch-block` (+ clases `.forward`, `.left`, `.right`) — bloques tipo Scratch con conectores.
- `.flag-btn`, `.stop-btn` — bandera verde circular y octágono rojo (clip-path).
- `.block-stage`, `.block-editor`, `.palette`, `.drop-zone`, `.script-title`, `.editor-head`.

**Verificado:**
- `node -e` valida el JavaScript (JS OK).
- Servidor `node server.js --dir nivel1/guia1` responde 200 en `/`.

---

## [0.5.0] — 2026-08-06

### Añadido — Nuevo slide antes del MiniTest (s11: "Explora el editor de bloques")

**Objetivo pedagógico:** Mostrar un editor real de programación en bloques integrado en la guía.

**Cambios:**
- Nuevo slide `s11` entre el laboratorio de bloques (s10) y el MiniTest, con:
  - Título "Explora el editor de bloques".
  - Texto explicativo sobre programación en bloques.
  - Contenedor que ocupa todo el espacio restante con un `<iframe src="https://blocks.octabio.co">` (editor de bloques de Octabio).
- Renumerados los slides siguientes: MiniTest `s11` → `s12`, Reporte `s12` → `s13` (IDs únicos verificados).
- Botón "Siguiente" de s10 actualizado: "Explorar el editor →"; el nuevo slide avanza con "Ir al MiniTest →".
- El contador de progreso se actualiza automáticamente (13 slides).

**CSS añadido:**
- `.blocks-embed` + `.blocks-embed iframe` — contenedor responsive que llena la fila restante con el editor embebido.

**Verificado:**
- `blocks.octabio.co` responde 200 sin `X-Frame-Options` ni CSP `frame-ancestors` (embebible).
- `node -e` valida el JavaScript (JS OK) y no hay IDs de slide duplicados.
- El servidor sirve `nivel1/guia1/index.html` con el iframe incluido.

---

## [0.6.0] — 2026-08-06

### Modificado — Barra de progreso y navegación

**Cambios:**
- Se quitó la barra de progreso superior (topbar) junto con el contador.
- La barra de progreso ahora vive dentro del `.lesson-nav`, entre los botones "Regresar" y "Continuar".
- La barra no se muestra en la primera slide (s1) ni en la última (s13) vía CSS `#deck .slide:first-of-type / :last-of-type`.
- Todos los botones inferiores se simplificaron a solo "Regresar" o "Continuar" (se quitaron flechas y textos personalizados). El botón de la primera slide dice "Continuar" y el de cierre de la última también "Continuar" (mantiene el estilo verde `finish` y abre el modal de finalización).
- El JavaScript actualiza el ancho de la barra de la slide visible en el observer.

**CSS añadido/modificado:**
- `.lesson-nav .nav-progress` + `i` — barra integrada entre botones.
- Eliminados `.progress`, `.progress i`, `.counter`.

---

## [0.7.0] — 2026-08-06

### Eliminado — Slide 10 "Laboratorio de programación en bloques"

**Cambios:**
- Eliminado el slide `s10` "Laboratorio de programación en bloques" (aventura de bloques con drag & drop) y todo su código: HTML de la sección, CSS exclusivo (`.block-lab`, `.block-stage`, `.block-world`, `.world-grid`, `.world-cell`, `.block-controls`, `.flag-btn`/`.stop-btn`, `.block-editor`, `.editor-head`, `.palette`, `.scratch-block`, `.script-title`, `.drop-zone`) y el bloque JS (`blockStage`/`blockMeta`/`blockPalette`/`blockState`/`blockLab`, `buildBlockLab`, `renderBlockWorld`, `renderBlockQueue`, `blockForward`, `executeBlock`, `runBlocks`, `stopBlocks`, etc.).
- Se conservan los estilos y helpers compartidos: `.mission-overlay`, `.debug-panel`, `dirVectors`, `dirNames`, `keyCell`, `sleep` y las funciones de audio.
- `pauseAllLabs()` ya no referencia `blockState`.
- Renumerados los slides siguientes: `s11` "Explora el editor de bloques" → `s10`, `s12` "MiniTest" → `s11`, `s13` "Reporte" → `s12`. El contador y la barra de progreso se ajustan automáticamente (12 slides).

**Verificado:**
- JS válido (`node -e` con `new Function`) y sin tokens residuales del lab (`blockLab`, `blockState`, `scratch-block`, `drop-zone`, `flag-btn`, `world-grid`…).
- IDs de slide secuenciales 1–12 sin duplicados.
- El servidor sirve `nivel1/guia1/` con HTTP 200.

---

## [0.8.0] — 2026-08-06

### Modificado — Slide 8: "¿Qué es Scratch?"

**Objetivo pedagógico:** Introducir Scratch como lenguaje de programación visual donde los algoritmos se construyen encajando bloques de código (analogía con LEGO).

**Cambios:**
- Reescrito el slide `s8` con el título "¿Qué es Scratch?" y el texto insumo sobre algoritmo, bloques de color y programas que controlan personajes, objetos y escenarios.
- Nueva composición visual de tres elementos conectados con flechas (`flow-row`):
  1. **Algoritmo** — los 7 pasos del algoritmo: bandera, avanzar 200, decir "Hola", cambiar dirección, esperar 1 segundo, retroceder 200, decir "Adiós".
  2. **Bloques en Scratch** — la secuencia de bloques de colores del algoritmo (evento bandera, movimiento, "decir", esperar) en CSS puro, igual que un editor.
  3. **Ejecución** — escenario con un gato 🐱 animado con CSS keyframes (tipo GIF) que avanza, saluda "¡Hola!", gira, espera, retrocede y se despide "¡Adiós!", en bucle infinito.
- `data-title` del slide actualizado a "Qué es Scratch".

**CSS añadido:**
- `.code-block.looks` (púrpura), `.code-block.control` (naranja) y `.code-block.hat` (bloque de evento con borde superior redondeado, sin lengüeta).
- `.flow-row`, `.flow-arrow`, `.flow-card`, `.flow-head`, `.flow-n` — composición de 3 tarjetas con flechas.
- `.scratch-program` — pila compacta de bloques.
- `.scratch-stage`, `.stage-flag`, `.scratch-sprite`, `.bubble-hola`/`.bubble-adios` + `@keyframes scratch-run`, `show-hola`, `show-adios`, `flag-wave` — animación de ejecución tipo GIF.

**Verificado:**
- JS válido (`node -e`), 7 pasos y 7 bloques en la composición, keyframes presentes, slide IDs secuenciales 1–12 y servidor HTTP 200.

---

## [0.9.0] — 2026-08-06

### Añadido — Controles de vista en la navegación (todas las slides)

**Cambios:**
- Nuevos botones de control insertados en cada `.lesson-nav`, justo antes del botón "Continuar":
  - **Pantalla completa** — pone el documento (slide actual) en pantalla completa; al estar en pantalla completa el ícono cambia a "salir de pantalla completa" y al pulsarlo regresa al modo normal. Sincronizado con `fullscreenchange` (también responde a la tecla Esc).
  - **Zoom + / Zoom −** — amplía o reduce el tamaño del slide entre 0.6× y 1.9× en pasos de 0.15; los botones se deshabilitan en los límites.
- El zoom se aplica multiplicando el tamaño del `.canvas` por la variable `--zoom` (definida en `#deck`). Como el contenido interno usa unidades `cqw`, todo el slide escala proporcionalmente al hacer zoom.
- Al alejarse del 100% se desactiva el scroll-snap (`html.zoomed{scroll-snap-type:none}`) para poder hacer scroll libre dentro del slide ampliado; el `.canvas` conserva su `margin:auto` para que el contenido ampliado sea accesible.
- Los controles se inyectan por JS (`injectNavControls`) en los 12 `.lesson-nav` para no repetir HTML; el zoom es compartido entre slides (persiste al navegar).

**CSS añadido:**
- `.ctrl-group` y `.lesson-nav .ctrl-btn` — botones compactos con íconos SVG (zoom-out, zoom-in, fullscreen abrir/cerrar); estados hover, active, disabled y toggle `.fs-active` para intercambiar íconos de pantalla completa.
- `#deck{--zoom:1}`, canvas dimensionado con `calc(… * var(--zoom,1))` y `min-width/min-height` también escalados.

**Verificado:**
- JS válido (`node -e`), 12 `.lesson-nav` con controles, reglas CSS presentes y servidor HTTP 200.

---

## [0.10.0] — 2026-08-06

### Ajustado — Zoom bidimensional con scrollbars + botón de narración

**Cambios (zoom):**
- El `.canvas` ahora tiene `flex:none`, evitando que el contenedor flex lo encoja en horizontal al hacer zoom. Con esto el slide crece proporcionalmente en **ambas dimensiones** (16:9 intacto) y aparecen scrollbars vertical y horizontal en `.slide` para desplazarse, lo que facilita ajustar la visualización en distintas pantallas.
- El zoom sigue escalando el contenido interno (unidades `cqw`) sin cambiar la proporción de la pantalla.

**Añadido (narración):**
- Nuevo botón de narración en el `.ctrl-group` (junto a zoom y pantalla completa), con ícono de altavoz.
- Se muestra siempre en estado "desactivado" (gris, apagado). Al pulsarlo se reproduce la narración en voz alta del texto escrito en la diapositiva actual usando la Web Speech API (`speechSynthesis`, idioma `es`); el botón se enciende en verde con un pulso mientras narra. Al pulsarlo de nuevo se detiene.
- El texto se extrae del slide visible (se excluyen la barra de navegación, el eyebrow, los overlays de misión, botones y decoración).
- La narración se detiene automáticamente al navegar a otra diapositiva o cuando la pestaña pasa a segundo plano.

**CSS añadido:**
- `.ctrl-btn.narr-off` (estado desactivado) y `.ctrl-btn.narr-on` (activo, verde, con `@keyframes voice-pulse`).

**Verificado:**
- JS válido (`node -e`), botón `data-narrate` inyectado en los 12 slides, funciones de narración presentes y servidor HTTP 200.

---

## [0.11.0] — 2026-08-06

### Ajustado — Zoom: botón "ajustar a pantalla" y corrección de la rejilla de pasos

**Cambios:**
- Nuevo botón **"Ajustar al tamaño de la pantalla (100%)"** entre los botones de zoom − y +. Restablece el zoom a 1.0× de un solo clic y reposiciona el scroll del slide al inicio (arriba/izquierda) para volver a la vista normal.
- **Bug corregido**: el zoom no podía volver exactamente a 100% cuando se bajaba al mínimo (0.6×). La rejilla de pasos de 0.15 desde 1.0 hacia abajo era `1.0 → 0.85 → 0.7 → 0.6`, pero al subir desde 0.6 iba `0.75 → 0.9 → 1.05`, saltándose el 1.0. Se cambió el mínimo a **0.55×** para que la misma rejilla baje y suba exactamente por 1.0 (0.55 → 0.7 → 0.85 → 1.0).
- El botón de ajuste queda disponible en los 12 slides (se inyecta junto al resto de controles).

**Verificado:**
- JS válido (`node -e`), rejilla verificada: subiendo desde 0.55 se aterriza exactamente en 1.0, botón `data-zoom-fit` presente y servidor HTTP 200.

---

## [0.12.0] — 2026-08-07

### Modificado — Slide 8: nueva tarjeta de algoritmo e imágenes reales

**Objetivo pedagógico:** Reforzar que el orden importa: del algoritmo a sus bloques en Scratch y a la ejecución del programa.

**Cambios:**
- Tarjeta **1 (Algoritmo)** actualizada a los **6 pasos** de la profesora: (1) Al presionar la bandera hacer:, (2) Decir ¡Hola! durante 2 segundos, (3) Mover 200 pasos, (4) Esperar 1 segundo, (5) Decir ¡Adiós! durante 2 segundos, (6) Mover 200 pasos.
- Tarjeta **2 (Bloques en Scratch)**: reemplazada la pila de bloques CSS por la imagen real `assets/img/algoritmo.png` con `alt` descriptivo.
- Tarjeta **3 (Ejecución)**: reemplazada la animación CSS del gato por el GIF real `assets/img/gifalgoritmo.gif`; conservada la descripción de ejecución (el gato dice "¡Hola!", avanza, espera 1 segundo, dice "¡Adiós!" y vuelve a avanzar).

**CSS añadido/modificado:**
- `.card-img` — imagen responsive con `max-height` proporcional y sombra suave.
- Eliminados los estilos ya huérfanos de la animación CSS: `.scratch-program`, `.scratch-stage`, `.stage-flag`, `.scratch-sprite`, `.bubble*` y `@keyframes scratch-run`, `show-hola`, `show-adios`, `flag-wave`. Se conservan `.flow-*` y `.code-block.looks/.control/.hat` compartidos.

**Verificado:**
- JS válido (`node -e`), 6 pasos en la tarjeta, ambas imágenes referenciadas (`algoritmo.png` y `gifalgoritmo.gif`) y sin tokens residuales de `scratch-program`/`scratch-stage`/`scratch-sprite`.
- Las imágenes sirven HTTP 200 (62 KB y 6.1 MB) y el servidor responde en `nivel1/guia1/`.

---

## [0.13.0] — 2026-08-07

### Modificado — Slide 9: intro a Octabio Studio con video

**Objetivo pedagógico:** Presentar Octabio Studio como el laboratorio de programación donde se construirán los algoritmos.

**Cambios:**
- Reemplazado el slide `s9` ("Un algoritmo simple en bloques") por la introducción **"Conoce tu laboratorio de programación: Octabio Studio"**.
- El espacio restante lo ocupa un reproductor de video embebido de YouTube (`https://www.youtube.com/embed/5OUb91fDKXw`) reutilizando el contenedor `.blocks-embed` (titulo + `iframe` fullscreen que llena la fila restante).
- `data-title` del slide actualizado a "Conoce tu laboratorio: Octabio Studio" y eyebrow "Octabio Studio".

**CSS eliminado (huérfano tras quitar el `block-demo`):**
- `.block-demo`, `.code-block*` (event/motion/loop/condition/looks/control/hat), `.arrow-down`.

**Verificado:**
- JS válido (`node -e`), 12 slides secuenciales, `code-block`/`block-demo`/`arrow-down` sin residuos, embed de YouTube HTTP 200 y servidor en `nivel1/guia1/` HTTP 200.

---

## [0.14.0] — 2026-08-07

### Modificado — Slide 9: bloqueo de salidas del video de YouTube

**Objetivo pedagógico:** Que los estudiantes solo puedan ver el video de Octabio Studio sin salir de la plataforma.

**Cambios (iframe del video):**
- Añadido `sandbox="allow-scripts allow-same-origin allow-presentation"` **sin `allow-popups` ni `allow-top-navigation`**: los enlaces de salida de YouTube (logo, "Watch on YouTube", `target=_blank`) quedan silenciosamente bloqueados por el navegador.
- Parámetros de la URL del embed para eliminar videos sugeridos y branding:
  - `rel=0` — desactiva los videos relacionados.
  - `iv_load_policy=3` — desactiva anotaciones.
  - `modestbranding=1` — reduce el branding de YouTube en los controles.
  - `playsinline=1` — reproducción dentro de la página.
  - `loop=1` + `playlist=<id>` — el video se repite en bucle, evitando la pantalla de sugerencias "Up next" al terminar.
- El video solo puede reproducirse dentro del slide; no puede abrirse en otra pestaña desde el reproductor.

**Verificado:**
- JS válido (`node -e`), iframe con `sandbox` sin `allow-popups`/`allow-top-navigation`, parámetros `rel=0`, `loop=1` y `playlist` presentes, embed con los parámetros responde HTTP 200 y servidor en `nivel1/guia1/` HTTP 200.

---

## [0.15.0] — 2026-08-07

### Modificado — Navegación solo con botones

**Objetivo pedagógico:** Evitar que los estudiantes salten de slide con la rueda del mouse o las flechas; la navegación queda reservada a los botones "Regresar"/"Continuar".

**Cambios:**
- Eliminado el `scroll-snap-type:y mandatory` de `html` y el `scroll-snap-align`/`scroll-snap-stop` de `.slide` (y la regla `html.zoomed` que ya era innecesaria): la rueda ya no "cae" sobre el siguiente slide.
- Eliminado el manejador de teclado que navegaba con `ArrowRight`/`ArrowLeft`/`PageUp`/`PageDown`.
- Nuevo bloqueo de navegación por scroll/teclado cuando el zoom está al 100%:
  - `wheel` con `preventDefault()` (passive:false) — la rueda del mouse no desplaza la página entre slides.
  - `keydown` con `preventDefault()` sobre `ArrowUp/Down/Left/Right`, `PageUp/Down`, `Home/End` y barra espaciadora (no aplica dentro de `input/textarea/select`).
- Cuando el slide está en zoom (≠100%), el scroll y las flechas siguen funcionando para desplazarse dentro del slide ampliado (panning); la navegación entre slides solo ocurre vía `goToSlide()` desde los botones.

**Verificado:**
- JS válido (`node -e`), sin `scroll-snap` en `html` ni `.slide`, sin handlers de flecha de navegación, bloqueos de `wheel`/teclas presentes, `goToSlide` intacto y servidor HTTP 200.

---

## [0.16.0] — 2026-08-07

### Corregido — Vista única de slide, centrado en "Ajustar" y scroll en pantalla completa

**Problemas:**
- Al hacer zoom hacia abajo se alcanzaba a ver el slide anterior: al estar en zoom la rueda no se bloqueaba y, al no haber desborde interno en el slide, el scroll "rebotaba" a la página y desplazaba el deck.
- Al volver a "Ajustar a pantalla" el slide quedaba descentrado (la posición de scroll de la página quedaba a mitad de camino).
- En pantalla completa y al volver al modo normal se podía avanzar con el scroll.

**Cambios:**
- `html{overflow:hidden}`: la página ya no es desplazable por el usuario bajo ninguna condición. Con esto **siempre se ve un solo slide** por más pequeño que se haga el slide, y no existe scrollbar arrastrable ni scroll por rueda en pantalla completa o modo normal. El scroll programático (`scrollIntoView`) sigue funcionando para los botones de navegación.
- Botón "Ajustar al tamaño de la pantalla" (`applyZoom(1)`): además de restablecer el zoom, resetea el scroll interno del slide y centra el slide actual con `scrollIntoView({block:'start'})` para que quede perfectamente alineado.
- `fullscreenchange`: al entrar o salir de pantalla completa se realinea el slide actual al inicio del viewport, evitando el descentrado al volver al modo normal.

**Verificado:**
- JS válido (`node -e`), `overflow:hidden` presente en `html`, re-centrado en el botón de ajuste y en el cambio de pantalla completa, y servidor HTTP 200.

---

## [0.17.0] — 2026-08-07

### Corregido — Desplazamiento interno cuando el slide es más grande que la pantalla

**Problema:**
- Al ampliar el zoom el canvas superaba el alto del viewport, pero el slide usaba `min-height:100vh`, por lo que **crecía** para acomodar el contenido y el desborde quedaba en la página (`html` con `overflow:hidden`). Resultado: no había scroll interno, los botones de control del `lesson-nav` quedaban ocultos e inaccesibles y la página quedaba bloqueada.

**Cambios:**
- `.slide` pasa de `min-height:100vh` a **`height:100vh`** con `display:flex` y `overflow:auto`: el slide ocupa exactamente la pantalla y, cuando el canvas es más grande (zoom > 100%), el desborde cae **dentro** del slide, que se vuelve desplazable con la rueda y muestra scrollbars laterales para alcanzar cualquier parte, incluidos los botones de control.
- Se quitaron `justify-content/align-items:center` de `.slide` y se conserva `margin:auto` en `.canvas` (patrón canónico): en zoom >100% el extremo superior-izquierdo del canvas queda alcanzable con el scroll (el centrado por flex recortaría la parte inicial).
- La página sigue bloqueada (`html{overflow:hidden}`): solo se navega con botones y solo se ve un slide.

**Verificado:**
- JS válido (`node -e`), `.slide` con `height:100vh`+`overflow:auto` sin `min-height` ni centrado por flex, `.canvas` con `margin:auto`, y servidor HTTP 200.

---

## [0.18.0] — 2026-08-07

### Reestructurado — Un slide visible por vez (navegación por páginas)

**Cambio estructural:** Se abandona el modelo de "slides continuos en la misma página con scroll" y se adopta **una página, un slide visible**.

**Cambios:**
- CSS: `.slide{display:none}` por defecto y `.slide.active{display:flex}`. Solo el slide activo existe en el flujo de la página; el resto no se renderiza. Es imposible "ver el slide anterior o siguiente" porque no están en el layout.
- JS: `goToSlide(index)` ya no hace `scrollIntoView`; **cambia la clase `active`** (oculta el actual, muestra el objetivo), resetea su scroll interno y actualiza barra de progreso, contador y `document.title` vía `renderNavState()`.
- Eliminado el `IntersectionObserver` (ya no tiene sentido: no hay scroll que observar). El slide activo se controla explícitamente.
- Inicialización con `goToSlide(0)` al cargar.
- Se conservan los bloqueos de `wheel`/teclas (redundantes pero inofensivos) y `html{overflow:hidden}` como red de seguridad.
- La reglas `:first-of-type`/`:last-of-type` (ocultar barra de progreso en s1 y s12) siguen funcionando: son selectores estructurales.
- Zoom, narración, labs del minero, quiz, pantalla completa y modales intactos: todo el contenido se sigue construyendo al cargar y solo se muestra el slide activo.

**Verificado:**
- JS válido (`node -e`), 12 slides, `.slide{display:none}` + `.slide.active{display:flex}`, sin `IntersectionObserver` ni `scrollIntoView` en `goToSlide`, `goToSlide(0)` de arranque y servidor HTTP 200.

---

## [0.19.0] — 2026-08-07

### Corregido — Acceso a los botones de control cuando el slide desborda la pantalla

**Problema:**
- Al ampliar el slide (o en ventanas angostas donde el canvas mide 800px de ancho mínimo), los botones de control quedaban fuera de la pantalla y **no se podía hacer scroll para alcanzarlos**: los bloqueos de `wheel`/teclas seguían activos (solo se habilitaban con zoom) y, al 100%, la rueda no desplazaba el slide.

**Cambios:**
- Eliminados los `preventDefault()` globales de `wheel` y de las teclas de desplazamiento (flechas, PageUp/Down, Home/End, espacio), y la función `isZoomed()` que solo los usaba.
- Ahora el navegador desplaza naturalmente el `.slide` (que ya tiene `overflow:auto`): si el slide es más grande que la pantalla —al 100% en ventanas pequeñas o con zoom— la rueda y las flechas mueven el contenido interno y los botones de control quedan alcanzables.
- La estructura "un slide por página" lo hace seguro: con los demás slides en `display:none` y `html{overflow:hidden}`, la rueda **no puede** cambiar de slide; solo desplaza el contenido del slide activo. La navegación sigue siendo exclusiva de los botones.

**Verificado (Chrome headless contra el servidor local):**
- Al 100% con slide que desborda (viewport 400x800): `deltaX` de la rueda desplaza el slide (scrollLeft 0→420) y el botón de ajuste queda clicable.
- Al 100% en pantalla normal: la rueda no cambia de slide ni mueve nada (slide sigue en s1).
- Con zoom 1.3: la rueda desplaza el slide (scrollTop→209) y "Ajustar" restaura zoom 1 y scroll 0.
- Los botones `next`/`prev` siguen navegando (s1→s2).
- JS válido (`node -e`) y servidor HTTP 200.

---

## [0.20.0] — 2026-08-07

### Revertido — Vuelta al punto de inserción del video de YouTube (estado 0.13.0)

Se revierten los cambios estructurales de navegación/scroll/zoom que desconfiguraron la guía (versiones 0.14.0 a 0.19.0) y se restaura el modelo original de **slides continuos en una sola página con scroll**.

**Restaurado:**
- Navegación por scroll: `html` con `scroll-snap-type:y mandatory` + `html.zoomed{scroll-snap-type:none}` y `.slide` con `min-height:100vh`, `scroll-snap-align:start`, `scroll-snap-stop:always` y centrado flex.
- `goToSlide(index)` vuelve a usar `scrollIntoView({behavior:'smooth'})`; se restaura el `IntersectionObserver` para trackear el slide visible (barra de progreso, contador y `document.title`).
- Navegación con teclado restaurada: `ArrowRight`/`PageDown` y `ArrowLeft`/`PageUp` (respetando los labs bloqueados).
- Botón "Ajustar" y `fullscreenchange` sin re-centrado adicional (solo resetean el scroll interno del slide en `applyZoom(1)`).
- Eliminados: `html{overflow:hidden}`, `.slide.active`/`display:none`, `renderNavState()`, `goToSlide(0)` de arranque, y los bloqueos de `wheel`/teclas.

**Slide 9:**
- El iframe de YouTube queda como se insertó en 0.13.0 (embed simple sin sandbox ni parámetros), pero con el **nuevo video**: `https://www.youtube.com/embed/TNGJWjG7Og8` (enlace `https://youtu.be/TNGJWjG7Og8`).
- Título "Conoce tu laboratorio de programación: Octabio Studio" restaurado.

**Verificado:**
- JS válido (`node -e`), scroll-snap presente, `IntersectionObserver` y navegación por teclado restaurados, sin restos de `renderNavState`/`goToSlide(0)`/`.slide.active`, nuevo embed responde HTTP 200 y servidor HTTP 200.

---

## [0.21.0] — 2026-08-07

### Modificado — Slide 9: bloqueo de salidas y sugerencias del video

**Objetivo pedagógico:** Que los estudiantes solo vean el video de Octabio Studio dentro del slide, sin salir de la plataforma ni pasar a otros videos.

**Cambios (iframe del video `TNGJWjG7Og8`):**
- `sandbox="allow-scripts allow-same-origin allow-presentation"` **sin `allow-popups` ni `allow-top-navigation`**: el logo de YouTube y "Watch on YouTube" (enlaces `target=_blank`) quedan bloqueados silenciosamente por el navegador.
- Parámetros de URL para eliminar videos sugeridos y branding:
  - `rel=0` — desactiva los videos relacionados.
  - `iv_load_policy=3` — desactiva anotaciones.
  - `modestbranding=1` — reduce el branding en los controles.
  - `playsinline=1` — reproducción dentro de la página.
  - `loop=1` + `playlist=<id>` — el video se repite en bucle, evitando la pantalla de sugerencias "Up next" al terminar.

**Verificado:**
- JS válido (`node -e`), iframe con `sandbox` sin `allow-popups`/`allow-top-navigation`, parámetros `rel=0`, `loop=1` y `playlist` presentes, embed con los parámetros responde HTTP 200 y servidor en `nivel1/guia1/` HTTP 200.

---

## [0.22.0] — 2026-08-10

### Añadido — Slide del Mini reto (s10) + título sin "Conoce" + video 16:9

**Slide 9 (video):**
- Título sin la palabra "Conoce": h2 "Tu laboratorio de programación: Octabio Studio", `data-title` "Tu laboratorio: Octabio Studio" y `title` del iframe "Video: Tu laboratorio de programación: Octabio Studio".
- Contenedor del video con relación 16:9: clase `.blocks-embed.video` con `height:100%;max-width:100%;width:auto;aspect-ratio:16/9;justify-self:center`. Verificado en Chrome headless: contenedor de 969.8×545.5 px (ratio 1.778) centrado en el slide.

**Nuevo slide s10 "Mini reto: mi primer algoritmo" (después del video, antes de explorar el editor):**
- Reto de instrucciones escritas: el alumno redacta con sus palabras el algoritmo para que el robot minero llegue al cofre (sin editor de bloques todavía).
- Layout `.content two-col`: columna izquierda con `lead`, 3 pasos (`.steps-list` + `.step-line`) y nota de pista (`.challenge-note` con ícono `!`); columna derecha con `.card.white` y `textarea#retoText` para numerar las instrucciones.
- Nuevo CSS: `.card.white textarea` y su estado `:focus` (min-height 9cqw, borde, radio y sombra).
- Renumerados los slides siguientes: "Explora el editor de bloques" `s10` → `s11`, "MiniTest de misión" `s11` → `s12`, "Reporte de misión" `s12` → `s13` (IDs únicos verificados, 13 slides totales).

**Verificado:**
- JS válido (`node -e`), 13 slides con IDs únicos, en navegador: s10 muestra "10 / 13", título y textarea funcionales, navegación a s11 (editor) correcta y sin overflow vertical. Servidor HTTP 200.

---

## [0.23.0] — 2026-08-10

### Modificado — Slide del Mini reto (s10): ahora una misión de conversación en Scratch con ejemplo

**Objetivo pedagógico:** El alumno programa en Scratch una conversación entre dos personajes sincronizada con esperas de tiempo.

**Cambios en s10:**
- Título y `data-title` → "Mini reto: conversación en Scratch"; h2 "Tu misión: una conversación en Scratch".
- Misión en 4 pasos (`.steps-list` + `.step-line` compactos): elegir un fondo, agregar dos personajes a gusto, crear una conversación con esperas de tiempo para sincronizar los mensajes, y cada personaje debe decir al menos tres frases.
- Nota (`.challenge-note`): para mensajes largos, aumentar el tiempo de duración del mensaje y de las esperas para que no se sobrepongan las conversaciones.
- **Ejemplo mostrado en horizontal** (`.flow-row` con 3 `.flow-card` unidas por flechas `→`):
  1. "Código del astronauta" — `assets/img/bloquesastro.png`.
  2. "Código del perro explorador" — `assets/img/bloquesdog.png`.
  3. "Ejecución del programa" — video `assets/img/scratchejemplo1.mp4` (reproductor `<video controls playsinline preload="metadata">`).
- Eliminado el textarea del reto anterior y su CSS `.card.white textarea` (ya no se escribe texto en el slide).
- Nuevo CSS: `.card-video` (video 16:9 con `max-height:10.5cqw`, fondo oscuro y esquinas redondeadas).

**Verificado:**
- JS válido (`node -e`), 13 slides, en Chrome headless: s10 muestra "10 / 13", sin overflow vertical (diff 1px), las 3 tarjetas alineadas y del mismo alto, imágenes cargadas, video sin errores (duración 14.2 s), navegación a s11 (editor) correcta y servidor HTTP 200.

---

## [0.24.0] — 2026-08-10

### Modificado — Slide del Mini reto (s10): pasos integrados en el texto + más espacio para los códigos

- Los 4 pasos de la actividad (fondo, personajes, conversación con esperas, mínimo 3 frases) ya no van en cajas `.steps-list`/`.step-line`: se integraron como prosa en el `lead` de la misión, con un párrafo aparte que introduce el ejemplo ("observa los dos códigos y su ejecución").
- Elementos de código agrandados: `max-height` de las imágenes (`.card-img`) y del video (`.card-video`) subido de `10.5cqw` a `18cqw`; el video ocupa ahora ~241px de alto en la vista de 1380×776 y las tarjetas quedan de ~311px, aprovechando el espacio que liberaron los pasos.

**Verificado:**
- JS válido (`node -e`), sin restos de `steps-list` en s10, en Chrome headless: sin overflow vertical (diff 0 px), 3 tarjetas alineadas del mismo alto, video sin errores (14.2 s), navegación a s11 correcta y servidor HTTP 200.

---

## [0.25.0] — 2026-08-10

### Modificado — Slide del Mini reto (s10): sin flechas, códigos más anchos y nota en texto plano

- **Flechas eliminadas**: el `.flow-row` del s10 pasa a `grid-template-columns:1.15fr 1.15fr 1fr` (sin las dos `.flow-arrow`). Las tarjetas de código (astronauta y perro) ganan amplitud (410.9 px vs 358.7 px antes) mientras la del video conserva su ancho (~357 px).
- Las imágenes de código crecen: `bloquesastro.png` 167→192 px y `bloquesdog.png` 194→223 px de alto (a `max-height:18cqw`).
- **Nota reescrita sin negrita**: se quita el `<strong>` y se fuerza `font-weight:400` (anula el `font-weight:800` de `.challenge-note p`). Texto: "Nota: para mensajes largos, aumenta el tiempo de duración del mensaje y de las esperas para leerlos con calma y sin que se sobrepongan, fíjate que en el ejemplo mientras un personaje habla durante un tiempo, el otro espera ese mismo tiempo para responder."

**Verificado:**
- JS válido (`node -e`), sin `.flow-arrow` en s10, en Chrome headless: tarjetas de código más anchas que la del video, nota en `font-weight:400` sin `<strong>`, sin overflow vertical, contador "10 / 13" y navegación correcta.

---

## [0.26.0] — 2026-08-10

### Añadido — Slide del editor (s11): reto en texto en la parte superior

- Banner compacto `.reto-banner` en la parte superior del editor de bloques para que los estudiantes sepan qué hacer: "Tu reto: elige un fondo, agrega dos personajes y crea una conversación con esperas de tiempo para sincronizar sus mensajes. Cada personaje debe decir al menos tres frases."
- El `content` de s11 pasa de `grid-template-rows:1fr` a `grid-template-rows:auto 1fr` con `gap:.55cqw`: el banner ocupa solo su altura natural y el resto sigue siendo para el editor embebido (`blocks.octabio.co`).
- Nuevo CSS `.reto-banner` (fondo crema, borde, texto `font-weight:600`, "Tu reto:" en naranja y `font-weight:900`).

**Verificado:**
- JS válido (`node -e`), en Chrome headless: banner de ~53 px (2–3 líneas) sobre un editor que conserva ~73% del área del slide (552 px de alto), sin overflow vertical, contador "11 / 13" y navegación correcta.

---

## [0.27.0] — 2026-08-10

### Modificado — Slide del editor (s11): texto de misión sin recuadro

- El texto de la parte superior ya no va en un recuadro (se elimina `.reto-banner` y su CSS).
- Rótulo cambiado de "Tu reto:" a **"Misión:"**: "Misión: elige un fondo, agrega dos personajes y crea una conversación con esperas de tiempo para sincronizar sus mensajes. Cada personaje debe decir al menos tres frases."
- Se mantiene como texto plano (`<p>` con `font-weight:600` y "Misión:" en negrita) en `grid-template-rows:auto 1fr`, sin restar espacio al editor.

**Verificado:**
- JS válido (`node -e`), sin restos de `reto-banner` ni "Tu reto" en s11, editor conservando el área principal.

---

## [0.28.0] — 2026-08-10

### Añadido — Slide del editor (s11): pista de categorías de bloques

- Nueva línea debajo de la misión: "Los bloques que necesitas los encuentras en las categorías de Eventos, Apariencia y Control."
- La misión se mantiene en color oscuro (`--ink`) y la pista en gris suave (`--muted`).
- Ambas líneas se agrupan en un contenedor (`display:grid;gap:.25cqw`) para que la fila `1fr` del grid siga siendo del editor y este conserve ~542 px (72% del slide) sin overflow.

**Verificado:**
- JS válido (`node -e`), en Chrome headless: filas `auto 1fr` bien asignadas (textos 63 px + editor 542 px), iframe llenando el contenedor, sin overflow vertical, contador "11 / 13".

---

## [0.29.0] — 2026-08-10

### Modificado — Pista de categorías movida de s11 a s10

- Se quita de s11 la línea "Los bloques que necesitas los encuentras en las categorías de Eventos, Apariencia y Control." (junto con su contenedor). El editor recupera esa altura: ahora ~566 px (75% del slide).
- Se agrega en s10 como pista, justo después del párrafo que introduce el ejemplo: "Pista: los bloques que necesitas los encuentras en las categorías de Eventos, Apariencia y Control." (en gris suave `--muted`).

**Verificado:**
- JS válido (`node -e`), pista presente solo en s10, en Chrome headless: s10 sin overflow (diff 0 px) y s11 con el editor llenando la fila `1fr` (566 px) sin overflow.

---

## [0.30.0] — 2026-08-10

### Modificado — Slide del editor (s11): sin misión, editor a tamaño máximo

- Se elimina también el texto de la misión de s11; el slide vuelve a `grid-template-rows:1fr` con solo el `.blocks-embed`.
- El editor embebido ocupa ahora toda el área del slide: ~613 px de alto (100% del contenido), sin overflow. La misión y la pista quedan solo en s10.

**Verificado:**
- JS válido (`node -e`), sin `<p>` ni "Misión" en s11, en Chrome headless: fila única `1fr` de 613 px, iframe llenando el contenedor, sin overflow vertical.

---

## [0.31.0] — 2026-08-10

### Modificado — Slide del reto (s10): pista movida debajo de la nota, en recuadro azul

- La pista ya no es una línea gris suelta: ahora va **debajo de la nota**, en un recuadro propio `.pista-box` (fondo `--sky`, borde `#c6dff4`, ícono `?` azul con "Pista:" en negrita).
- Para que quepa sin overflow: `gap` del content de `.9cqw` → `.8cqw` y `padding-bottom` de `6.2cqw` → `5.6cqw`.

**Verificado:**
- JS válido (`node -e`), la pista aparece después de la nota dentro de `.pista-box`, en Chrome headless: sin overflow vertical (diff 0 px) y todos los elementos visibles.

---

## [0.32.0] — 2026-08-11

### Añadido — Slide "Objetos y escenarios" con video (s12)

- Nuevo slide `s12` (después del editor de bloques, antes del MiniTest) con el video `https://youtu.be/rjcRgbrVRuA` (embed `rjcRgbrVRuA`), título "Objetos y escenarios", eyebrow "Nuevos conceptos" y un breve lead.
- **Mismos bloqueos que el video de s9**: `sandbox="allow-scripts allow-same-origin allow-presentation"` sin `allow-popups` ni `allow-top-navigation` (logo / "Watch on YouTube" bloqueados) y parámetros `rel=0`, `iv_load_policy=3`, `modestbranding=1`, `playsinline=1`, `loop=1` + `playlist=<id>` (sin videos sugeridos ni pantalla "Up next").
- Reutiliza `.blocks-embed.video` (16:9). Renumerados los slides siguientes: MiniTest → `s13`, Reporte → `s14` (14 slides, IDs únicos verificados).

**Verificado:**
- JS válido (`node -e`), 14 slides con IDs únicos, sandbox sin popups/top-navigation, parámetros presentes, embed nuevo HTTP 200, en Chrome headless: s12 muestra "12 / 14", video 16:9 (ratio 1.778), sin overflow.

---

## [0.33.0] — 2026-08-11

### Añadido — Misión integradora "Caperucita en bloques" (5 guías + editor compartido)

**Estructura (10 slides nuevos, s13–s22):** alterna una guía de escena y un slide de editor a pantalla completa:
`s13` guía Esc 1 → `s14` editor → `s15` guía Esc 2 → `s16` editor → `s17` guía Esc 3 → `s18` editor → `s19` guía Esc 4 → `s20` editor → `s21` guía Esc 5 → `s22` editor. MiniTest → `s23`, Reporte → `s24` (24 slides, IDs únicos).

**Editor compartido (no pierde avance):**
- Un único iframe persistente `#sharedEditor` (`position:fixed`, fuera de `#deck`, cargado una vez, se oculta con `opacity/visibility` —ocultar no recarga el iframe—).
- Los 5 slides de editor tienen un contenedor hueco `.blocks-embed.shared-slot`; el `IntersectionObserver` trackea `currentSlide`, y `syncSharedEditor()` posiciona el iframe exactamente sobre el slot del slide visible (left/top/width/height vía `getBoundingClientRect`) y lo activa solo en los slides de editor.
- Durante cualquier scroll, el editor se oculta y 110 ms después de que el scroll se detiene vuelve a posicionarse (debounce); así nunca se muestra descolocado a mitad de la animación y aparece ya centrado al asentarse (fade-in).
- Se reposiciona también en `applyZoom()` y en `resize`; el mismo iframe se conserva entre escenas (`src` sin cambios, no se recarga), así el estudiante continúa construyendo los bloques escena a escena.

**5 guías de escena (ayuda decreciente, formato del diseño instruccional):**
- Cada una con eyebrow "Caperucita en bloques · Escena N", título, frase corta de la misión, storyboard de 5 nodos con resaltado de la escena actual (CASA → BOSQUE → ATAJO → ABUELA → FINAL), `IMGAGE SUGERIDA` placeholder compacto (composición descriptiva, estética alineada a la guía) y paneles "Tu misión" / "Debe ocurrir" / "Comprueba" (con "Puedes usar" en Esc 1-2 y "Piensa" —pregunta de debugging— en Esc 3-4).
- Esc 1 "La misión" (muy guiada, menciona algunos bloques), Esc 2 "En el bosque" (intermedia), Esc 3 "El atajo del lobo" (reto de velocidad sin bloques concretos), Esc 4 "Casa de la abuela" (reto de apariencia/visibilidad), Esc 5 "El descubrimiento" (autonomía, final "FIN").

**CSS nuevo:** `.storyboard/.sb-node/.sb-arrow`, `.scene-grid/.scene-panels/.scene-tag/.scene-panel`, `.scene-ocurre`, `.scene-check`, `.scene-use`, `.scene-mission`, `.scene-img`, `.shared-editor`.

**Verificado:**
- JS válido (`node -e`), 24 slides con IDs únicos, 5 slots de editor + 1 iframe compartido.
- En Chrome headless: las 5 guías sin overflow ("13/24"… "21/24"), en los slides de editor `#sharedEditor` activo con tamaño exacto al slot (1208.6×613) y con el same iframe (una sola instancia `blocks.octabio.co`); en las guías queda oculto. Navegación por botones/teclas OK.

---

## [0.34.0] — 2026-08-11

### Modificado — Guías de escena: pistas con bloques de código

Los 5 slides de guía (s13, s15, s17, s19, s21) ahora se asemejan al slide de misión (s10):

- Se reemplazan los chips "Puedes usar" / "Piensa" por una sección **"Pistas · los bloques que necesitas"** (`.hint-section`) debajo del grid imagen + paneles, con 4 tarjetas numeradas (`.hint-card`) al estilo de los `flow-card` de s10: número azul, título de qué hace el bloque, el bloque visual y una descripción corta de para qué se usa.
- **Bloques visuales estilo Scratch** (`.blk`): rellenos de color por categoría (eventos dorado con forma de sombrero `.blk-hat`, movimiento azul, apariencia morado, sonido rosa, control naranja, escenarios verde) con valores anidados en recuadros blancos (`.blk i`).
- Bloques pista por escena: Esc 1 (bandera, decir, esperar, caminar), Esc 2 (bandera, cambiar escenario, sonido, decir+esperar para hablar por turnos), Esc 3 (bandera, caminar, esperar = ritmo/velocidad, caminar lento) **+ pista-box de "Piensa"** sobre cómo ser más rápido, Esc 4 (bandera, decir, esconder, caminar+esperar) **+ pista-box "Piensa"** sobre la desaparición, Esc 5 (bandera, decir, mostrar, decir FIN).
- Se mantienen los paneles "Tu misión" / "Debe ocurrir" / "Comprueba"; se elimina `.scene-use`.

**CSS añadido:** `.hint-section/.hint-grid/.hint-card/.hint-head/.hint-n/.hint-desc/.blk-row/.blk/.blk-hat/.blk-{events,motion,looks,sound,control,scenes}`.

**Verificado:**
- JS válido (`node -e`); 20 tarjetas pista (4×5) y 22 bloques, sin usos de `.scene-use`.
- En Chrome headless: las 5 guías **sin overflow** a 1380×776; bloques con los 4 colores de categoría y sombrero correctos; título y contador intactos ("13 / 24").

---

## [0.35.0] — 2026-08-12

### Modificado — La misión pasa de "Caperucita" a "Buscando a Nemo 2"

La historia integradora se re-tematiza de Caperucita Roja a **Buscando a Nemo 2** (sin violencia: tiburón amistoso, reencuentro familiar).

**s13 → Briefing de misión (rediseño completo):**
- Etiqueta `MISIÓN · HISTORIA ANIMADA`, título "BUSCANDO A NEMO 2" y subtítulo "Una aventura programada en Scratch".
- Distribución 55/45 (`.nemo-grid`): izquierda = video stage 16:9 (`.video-stage`) con botón ▶ y caption "Mira la historia completa" (este modelo no admite video, placeholder hasta recibir el archivo); derecha = tarjetas **"La historia"** (`.nemo-card`) y **"Tu misión"**.
- Fila de pills: Personajes · Escenarios · Movimiento · Sonido; botón siguiente "Comenzar misión".

**s14–s22 → Escenas Nemo (estructura y contenidos):**
- s14 editor Esc 1 "En el arrecife" (tras el briefing), s15 guía Esc 2 "En el océano", s16 editor Esc 2, s17 guía Esc 3 "El tiburón particular" (+ pista-box "Piensa"), s18 editor Esc 3, s19 guía Esc 4 "El camino a casa" (+ pista-box "Piensa"), s20 editor Esc 4, s21 guía Esc 5 "Regreso con Marlin", s22 editor Esc 5.
- Storyboard Nemo de 5 nodos: ARRECIFE → OCÉANO → TIBURÓN → CAMINO → MARLIN (nodo actual resaltado).
- "Debe ocurrir" y "Comprueba" adaptados por escena; bloques pista reescritos (bandera, cambiar escenario "Océano"/"Mar profundo"/"Arrecife", reproducir sonido "Burbujas", decir, esperar, esconder, mostrar) con descripciones "para qué".

**Ajustes de espacio (evitar overflow):**
- padding-bottom de las guías 4.4→3.6cqw; `.scene-panel li` 0.27→0.22; `.scene-tag` 0.76→0.72; `.hint-card` 0.55/0.8→0.45/0.7; `.blk` 0.76/0.5-0.8→0.73/0.45-0.72; `.storyboard` 0.82/0.45→0.78/0.35; `.scene-mission` 0.45/0.6→0.35/0.55; `.pista-box` 0.7/1.05→0.55/0.9; `.hint-desc` 0.78→0.75.

**Verificado:**
- JS válido; 24 slides con IDs únicos; 0 referencias a "Caperucita" en index.html.
- En Chrome headless a 1380×776: las 5 guías sin overflow (storyboard incluido), editor compartido alineado 0px en s22 tras recorrer toda la misión ("22 / 24"), MiniTest y Reporte intactos ("24 / 24").

---

## [0.36.0] — 2026-08-12

### Modificado — Slide 13 con estilo del slide 10 y textos finales

El briefing de s13 se rehace siguiendo la composición del slide 10 (título + lead, fila de tarjetas numeradas, nota final) en vez del layout 55/45:

- `h2 "Buscando a Nemo 2"` + lead "Una aventura programada en Scratch" (alineación del s10).
- `flow-row` de 2 columnas: tarjeta **"La historia"** (flow-n 1, texto final de Nemo: explora el arrecife contra el consejo de Marlin, Dory lo acompaña, se pierden, tiburón vegetariano, escapan y Dory cree reconocer el camino) y tarjeta **"Tu misión"** en alto contraste (`.mission-card`): fondo gradiente azul, franja naranja superior, kicker "Tu misión" en ámbar, lead en blanco y párrafo de bloques ("hablen, se muevan, aparezcan en el momento correcto…").
- **Cadena de acciones** (`.act-shell`): "Tus personajes deberán:" y 6 píldoras enlazadas con flechas → Hablar → Moverse → Cambiar de escenario → Aparecer y desaparecer → Reaccionar → Actuar en el momento correcto.
- **Cierre conceptual**: `challenge-note` — "Cada personaje tendrá su propio programa, pero todos deberán trabajar juntos para contar una sola historia."

**CSS añadido:** `.mission-card` (y `::before`), `.mission-kicker`, `.mission-lead`, `.act-shell`, `.act-label`, `.act-chain`, `.act`, `.act-arr`.

### Ajuste — Slide 13: video cuadrado a la izquierda y tipografías alineadas con s10

- Nuevo layout `.split` (1.05fr/1fr): **izquierda** contenedor de video **cuadrado** `.video-stage` (30cqw × 30cqw, gradiente azul marino, etiqueta "Vídeo · ejecución del programa", botón ▶ y caption "Mira la historia completa") preparado para recibir el video de la ejecución; **derecha** dos recuadros apilados: `.flow-card` "La historia" (flow-n 1) y `.mission-card` "Tu misión" en alto contraste.
- Eliminados los `font-size` en línea que encogían los textos: lead, párrafos, títulos y nota conceptual vuelven a los tamaños por defecto del s10 (`p` 1.05cqw, `flow-card h3` 1.35cqw, `.lead` 1.4cqw). La cadena de acciones y el cierre conceptual se mantienen debajo.
- `.mission-card p` conserva solo el color blanco-azulado y hereda el tamaño por defecto; `.mission-lead` crece a 1.3cqw; pills `.act`, `.act-label`, `.vs-tag` y `.vs-caption` aumentadas.
- Obsoletas y eliminadas: `.nemo-grid`, `.nemo-left`, `.nemo-right`, `.nemo-card*` (el layout 55/45 desaparece).

**Verificado:**
- JS válido; sin overflow a 1336×752; `.video-stage` cuadrado (388×388 px, centrado en columna de 591 px); fuentes alineadas con s10 (párrafos 13.6 px, h3 17.5 px, lead 18.1 px); left: video square, right: historia + misión; 6 píldoras de acción intactas.

### Ajuste — Slide 13: unificadas las tarjetas al estilo s10

- "Tu misión" deja de ser un recuadro en alto contraste y pasa a ser una `.flow-card` idéntica a "La historia" (fondo blanco, borde `--line`, h3 y texto en formato normal estándar).
- "La historia" pierde el número 1 (`.flow-n`); ambos recuadros actúan como simples separadores de los textos con sus títulos.
- Eliminados el subtítulo `.lead` ("Una aventura programada en Scratch"), el caption bajo el video ("Mira la historia completa") y el CSS residual de `.mission-card`, `.mission-kicker` y `.mission-lead`.

**Verificado:**
- Sin overflow a 1336×752; `.video-stage` cuadrado (388×388 px); 2 `.flow-card` (La historia / Tu misión) sin `.flow-n` y con párrafos a 13.6 px; contador "1 / 24".

### Ajuste — Slide 13: textos sin recuadros y contenido centrado

- "La historia" y "Tu misión" dejan de ser tarjetas (`.flow-card`) y pasan a bloques de **texto normal** (`.text-block`): solo `h3` + `p` con los formatos estándar de los demás slides; cada bloque actúa como simple separador sin fondo ni borde.
- Contenedor derecho renombrado `.side-cards` → `.side-texts` (grid, `align-content:center`), alineado al centro vertical del video cuadrado.

**Verificado:**
- Contenido centrado verticalmente con márgenes superiores e inferiores simétricos (38/38 px a 1336×752, 34/34 px a 1263×684, 61/61 px a 1920×1080); sin overflow; video cuadrado alineado con los textos a <5 px.

### Ajuste — Slide 13: reformato completo siguiendo el slide 10

- Se descarta la composición anterior y s13 adopta la estructura de s10 (elementos y formatos ya existentes en la guía, sin inventar nuevos):
  - `h2 "Buscando a Nemo 2"` + `p.lead` "Una aventura programada en Scratch…" con el mismo formato del lead de s10.
  - `.flow-row` de 2 columnas: a la **izquierda** los dos textos (`.text-block` "La historia" y "Tu misión") **sin recuadro y sin numeración**; a la **derecha** un `<video class="card-video">` (como el del s10, con `controls`), apuntando a `assets/img/nemoejemplo.mp4` (pendiente de entregar el archivo).
  - Debajo, `challenge-note` (igual que s10, con icono `!` y `p` en `font-weight:400`) donde se **fusionan** la cadena de acciones y el cierre conceptual: "Tus personajes deberán hablar, moverse, cambiar de escenario, aparecer y desaparecer, reaccionar y actuar en el momento correcto. Cada personaje tendrá su propio programa, pero todos deberán trabajar juntos para contar una sola historia."
- Eliminados `.split`, `.video-stage`/placeholder cuadrado, `.video-wrap`, `.vs-*`, `.act-shell`, `.act-chain`, `.act` (píldoras con flechas) y su CSS.

**Verificado:**
- Sin overflow a 1336×752 y 1920×1080; centrado vertical simétrico (107/107 px y 169/169 px); hijos de `.content`: `h2, .lead, .flow-row, .challenge-note`; 2 `.text-block` sin caja ni `.flow-n`; `<video>` presente con `src=assets/img/nemoejemplo.mp4`; subtítulo bajo el título con lead de s10 (18.1 px, ink).

### Ajuste — Slide 13: video temporal del s10 y textos en formato lead

- `<video>` apunta temporalmente a `assets/img/scratchejemplo1.mp4` (el del slide 10) mientras se consigue el video de la ejecución de Nemo.
- Los párrafos de "La historia" y "Tu misión" reciben `class="lead"`: mismo formato que "Una aventura programada en Scratch…" (1.4cqw, ink); se mantienen los `h3` como títulos.

**Verificado:**
- Sin overflow a 1336×752 y 1920×1080; ambos `.text-block p` en formato lead (18.1 px); `videoSrc=assets/img/scratchejemplo1.mp4`.

### Ajuste — Slide 13: video más alto y sin lead de presentación

- Eliminado el `p.lead` "Una aventura programada en Scratch…" bajo el `h2` (los textos "La historia" y "Tu misión" conservan su clase `lead`).
- El `<video>` gana altura aprovechando el espacio: `max-height:none` + `align-self:stretch` (en línea), rellena el alto de la fila manteniendo `object-fit:contain`.

**Verificado:**
- Sin overflow a 1336×752; video 462×359 px (antes ~240 px), alto de fila 359 px; centrado vertical (62/62 px).

### Añadido — Slide 13b «En el arrecife» (instrucciones de la Escena 1)

Creado el slide guía de la Escena 1 (se inserta entre el briefing s13 y el editor s14; el contador pasa a 25 slides):

- Cabecera + `storyboard` (ARRECIFE en curso) como las demás guías de escena.
- `.scene-grid` con columna izquierda (`.scene-left`):
  - `.gif-stage`: caja "Así se verá la escena 1" con `gifalgoritmo.gif` como placeholder (a reemplazar por la escena 1).
- Columna derecha `.scene-panels`: **Tu misión** (descripción textual de la escena), **Recursos** (escenario `UnderWater`, personajes `Fish` triplicado: Marlin, Dory y Nemo) y **Algoritmo** (los 6 pasos del pseudocódigo con los diálogos de Marlin/Dory/Nemo y la salida a la derecha).
- `hint-section` con 2 tarjetas: "Encender la escena" (bandera verde) y "Hablar y esperar" (decir + esperar), avisando que mientras uno habla los demás esperan su turno, como en el ejercicio anterior.
- `pista-box` compacto **"La parte importante: la sincronización"** (icono ⏱): los tres programas arrancan a la vez con la bandera verde, se usan *esperas* para que no hablen todos a la vez y, tras hablar, se desplazan 1 segundo para salir de la pantalla (escena de 7 s). Mantiene el mismo estilo de nota compacta de las demás guías (s17/s19).
- `child` de `.content`: `div, .storyboard, .scene-grid, .hint-section, .pista-box`.

**CSS añadido:** `.scene-left`, `.gif-stage` (y `.gif-tag`, img, `.gif-caption`).

**Verificado:**
- Sin overflow a 1336×752 (márgenes 24/24 px); 25 slides; navegación indexada intacta; el editor compartido del s14 sigue posicionándose alineado (dx/dy = 0) sobre su `.shared-slot`.

### Ajuste — Slide 13: textos reescritos (prólogo + misión)

- **La historia**: ahora suena a prólogo/intro ("Esta historia comienza en un arrecife lleno de vida… emprenderá una aventura por el inmenso océano"), dejando de narrar las escenas.
- **Tu misión**: nuevo inicio — "Convertirás esta historia narrada en una historia animada, como se ve en el video, y crearás una minipelícula usando programación en bloques." — y se conserva el resto (hablen, se muevan, aparezcan… hasta completar la historia).

**Verificado:**
- Sin overflow a 1336×752 y 1920×1080; estructura intacta (`h2, .flow-row, .challenge-note`).
