# MANUAL DE FORMATO · Slides de guías MAMUS

> Prompt de diseño para crear o editar slides de las guías digitales.
> Extraído del diseño final de la Guía 1 del Nivel 1 (`nivel1/guia1/index.html`).
> Este manual cubre **únicamente estilo, color, tipografía y estructura de slides**.
> No cubre la creación pedagógica de guías, ni la configuración de bloques Scratch, ni la integración del editor.

---

## 1. Regla de oro

- Todo lo que se dibuja **dentro del canvas** usa **unidades `cqw`** (relativas al ancho del contenedor). **Prohibido** usar valores fijos en px/puntos o `clamp()` para tamaños internos: el layout debe escalar 1:1 en cualquier resolución 16:9.
- El canvas mide **16:9** y escala con la ventana (`min-width` 520 × `min-height` 292).
- **Nunca** debe haber texto gris apagado como color principal. El cuerpo siempre se escribe en `--ink`.
- El contenido de cada slide debe caber sin desbordar en 1280×720 (scrollbar fina permitida al mínimo).

---

## 2. Paleta de colores (no inventar tonos nuevos)

```
--navy    #15345f   Base institucional oscura (botones, fondos oscuros)
--blue    #285aa6   Acento principal (eyebrows, encabezados laterales, círculos numerados)
--sky     #eaf5ff   Fondo suave azul (cards azules, pista-box)
--orange  #f28b2b   Énfasis/acción (highlight, números de lista, markers, íconos de nota)
--yellow  #ffd15a   Acento cálido (íconos de definición)
--green   #28a66a   Éxito / botón de finalizar / confirmación
--red     #d94a4a   Error / problemas
--ink     #18304c   Texto principal (SIEMPRE este para el cuerpo)
--paper   #ffffff   Fondo del canvas
--cream   #fff6e8   Fondo de cards y notas cálidas
--line    #d9e5f0   Bordes suaves
```

**Convenciones de uso:**
- **Texto corrido, títulos, captions → color `ink`. NUNCA `muted` gris.**
- Naranja (`orange`) = lo que el estudiante debe notar: números de pasos, `highlight`, íconos de `challenge-note` y `pista-box`.
- Azul (`blue`) = h3 de paneles ("Tu misión", "Algoritmo", etc.), eyebrow por defecto, botón "next" no destacado.
- Verde (`green`) = eyebrow de programación en bloques, botón `finish`, aprobación de quiz.
- Rojo (`red`) = solo para errores (recuadro `problem`, fallo de quiz).
- Cards: `cream` para notas/definiciones cálidas, `blue`(sky) para información, `white` para paneles neutros, `dark`(navy) solo para fondos oscuros tipo portada/reflexión.
- Fondo de página exterior: gradiente claro `#dbe8f4 → #f6fbff`. El canvas siempre en `--paper`.

---

## 3. Tipografía

- Familia: `Inter, ui-rounded, "Segoe UI", system-ui, sans-serif`.
- **Escala estándar de 4 tallas** (variables en `.canvas`). Todo hereda de estas:

```
--fs-title  3.45cqw   → solo h1 y h2  (line-height 1; h1 0.95; letter-spacing -0.035em)
--fs-sub    1.45cqw   → h3 y .lead   (h3 line-height 1.15; .lead line-height 1.42)
--fs-body   1.1cqw    → p, li, label, button, input, textarea, select, step-list li (p line-height 1.42)
--fs-note   0.85cqw   → captions, tags, nav-count, status-line, stage-caption, breadcrumbs
```

- **No** se usan tamaños intermedios sueltos con `clamp`. Si algo es caption → `--fs-note`; si es cuerpo → `--fs-body`; etc.
- Negritas al 800–900 para énfasis; `i`/cursiva solo para términos como *debugging*.
- Texto siempre alineado a la izquierda en columnas; centrado solo en placeholders/overlays.

---

## 4. Anatomía del slide

```
<section class="slide" id="sN">                     ← 100vh, centra el canvas
  <div class="canvas">                              ← 16:9, radius 2.4cqw, sombra, bg paper
    <div class="slide-eyebrow">…badge…</div>        ← OPcional: etiqueta pill arriba-derecha
    <div class="content [compact] [two-col|three-col]">
        …contenido según tipo de slide…
    </div>
    <div class="lesson-nav">…botones…</div>         ← SIEMPRE, barra inferior absoluta
  </div>
</section>
```

- `.content`: `padding: 4.2cqw 4.8cqw 7.6cqw`. **Los 7.6cqw inferiores están reservados para la barra de navegación**: el contenido nunca invade esa franja.
- `.content.compact`: `padding-top: 3.2cqw; padding-bottom: 7.2cqw` (slides de laboratorio, misiones, escenas).
- Gap por defecto del grid de contenido: `1.6cqw`; se ajusta por tipo (ver §6).
- Layouts: `.two-col` (1/1), `.two-col.wide-left` (1.18/0.82), `.two-col.wide-right` (0.86/1.14), `.three-col` (1/1/1, gap 1.4cqw).
- Si hay listas numeradas de pasos del usuario: `.steps-compact` (círculos azules con número).
- Números de pasos en listas de algoritmos (`.step-list`): **marcadores naranja**.

---

## 5. Barra de navegación (todas las slides)

Posición absoluta inferior dentro del canvas (`inset: auto 2.2cqw 1.65cqw 2.2cqw`).

| Elemento | Estilo |
|---|---|
| Botón prev | Fondo blanco, texto navy, borde 2px `#bfd2e5` |
| Botón next | Fondo `navy`, texto blanco, sombra |
| Botón next.finish | Fondo `green` |
| Botón next.locked | Opacidad .4, desaturado, `cursor:not-allowed` (puerta de laboratorio) |
| Progreso | Barra redondeada azul claro; relleno gradiente `#1a6cd1 → #4c97ff`, animación .25s |
| Contador (nav-count) | Pill celeste, texto navy, `--fs-note` |
| ctrl-btn | 3cqw × 3cqw; ícono SVG `1.87cqw` fijo |

**Nomenclatura de botones (no variar):**
- Prev siempre: `Regresar`
- Next por defecto: `Continuar`
- Inicio de misión (slide s13): `Comenzar misión`
- Nunca usar textos como "Historia lista", "Siguiente", etc.

---

## 6. Tipos de slide y su estructura exacta

### 6.1 Briefing de misión (portada s1)
- `.canvas.briefing` con imagen de fondo full-bleed (`.briefing-bg-img`, `object-fit:cover`).
- Eyebrow naranja arriba-derecha. Contenido en columna única `max-width:38cqw`.
- `h1` con `<span class="highlight">` palabra clave en naranja.
- `.lead` de qué aprenderá. Abajo `.briefing-meta`: 3 boxes translúcidos (blur) con título (`--fs-sub`, azul) y dato (`--fs-body`).
- Imagen de fondo: día/noche clara del tema; nunca texto clave en la mitad izquierda.

### 6.2 Concepto / Nuevo concepto (s2, s3, s12)
- Eyebrow azul `Nuevo concepto`. Estructura `two-col.wide-left`.
- Izquierda: `h2` + `.lead` (o fila de textos) + componentes (quote/problem/cards).
- Derecha: imagen `.slide-img` (inset 85% centrado o `--lg` ancho 110%).
- Nota pedagógica de cierre: `.challenge-note` a lo ancho (`grid-column:1 / -1`).

### 6.3 Laboratorio de clase (s4, s6, s7)
- Eyebrow naranja `Laboratorio de clase · Nivel N`.
- `.content.compact` con `grid-template-rows:auto 1fr` y `align-content:stretch`.
- Header `.mission-head`: `h2` + frase de misión en `.lead` (`--fs-sub`). El texto de misión va al nivel de subtítulo, no cuerpo.
- Debajo `.lab-shell` (el juego/runner ocupa el resto).

### 6.4 Debugeo en 4 pasos (s5)
- Contenido centrado con `gap:2.4cqw` (más aire vertical entre bloques).
- `.debug-cycle`: 4 `.cycle-step` en fila (círculo naranja numerado + h3 + p).
- Card azul informativa al cierre.

### 6.5 Scratch / bloques (s8, s10)
- Eyebrow verde (bloques) o naranja (mini reto).
- `flow-row` de cards: título breve, imagen/video `--card-img`, caption `--fs-note`.
- Archivo `.stage-caption` en `--fs-note` bajo imágenes de ejecución.
- Textos: `h2` + `.lead` + cuerpo; **condensar** (1 párrafo sólido, sin paréntesis largos ni redundancias).
- Cierres: `.challenge-note` (con `<b>Nota:</b>` en negrita dentro de párrafo normal) y/o `.pista-box` (`<strong>Pista:</strong>`).

### 6.6 Video / editor embebido (s9, s12, s11, y editors de escena s14/s16/s18/s20/s22)
- Slide casi a pantalla completa: `.content.compact` con `grid-template-rows:1fr`, **sin eyebrow**, **sin subtítulo**.
- `.blocks-embed`: caja con borde `#d5e5f3`, radius 1.4cqw. Variante `.video` = iframe 16:9 centrado.
- La etiqueta `h2` aparece **solo si hay contenido que introducir**; en slides de solo editor no se repite el título.

### 6.7 Briefing de misión de historia (s13 — Buscando a Nemo 2)
- Eyebrow naranja en mayúsculas: `MISIÓN · HISTORIA ANIMADA`.
- `h2` del nombre de la misión, sin subtítulo.
- `flow-row` 2 columnas (1.5fr/1fr): izquierda `.side-texts` con dos `.text-block` ("La historia" + "Tu misión" como h3 azules y texto en `.lead`); derecha `<video class="card-video">` (fondo negro).
- Cierre con `.challenge-note`.

### 6.8 Guía de escena (s13b, s15, s17, s19, s21) — formato estándar
Estructura exacta de estas slides (idéntica en las 5):

```
content.compact  gap:.9cqw ; padding-bottom:3.6cqw
  h2  "Escena N: Nombre"            ← sin subtítulo debajo
  .scene-grid  (margin-top:.9cqw)   ← grid 1fr / 1.28fr, gap .8cqw
     col.izq: .gif-stage
        .gif-tag   'Así se verá la escena N'  (uppercase, azul, --fs-note)
        <img gif>  max-height 20cqw, object-fit contain
        .gif-caption  (--fs-note, ink)
     col.der: .scene-panels
        .text-block > h3 'Tu misión' (azul) + p.lead
        .algo-block > h3 'Algoritmo' (azul) + ol.step-list
           marcadores naranjas; cuerpo en --fs-body
           diálogos con formato: «Personaje dice: “frase” durante X segundos.»
  .pista-box  (margin-top:.9cqw)    ← azul sky, ícono ⏱ azul
```

**Reglas duras de las guías de escena:**
- **No hay subtítulo** bajo el `h2` (el panel "Tu misión" cumple esa función). **No hay storyboard**.
- La duración estimada de la escena y el segundo de inicio (~): texto del `pista-box`.
- El `pista-box` se usa para el concepto técnico clave: sincronización, cambio de escena, aparición simultánea, estado inicial, verificación final.
- Ajuste vertical: título→grid = `margin-top:0.9cqw`; grid→pista = `margin-top:0.9cqw`. Igual en las 5 escenas.

### 6.9 MiniTest (s23)
- Eyebrow naranja `MiniTest de misión`; título `Comprueba lo aprendido`.
- Contenido con `gap:2.6cqw` (título y prueba bien separados).
- `.quiz-layout`: izquierda lista de preguntas (`.quiz-nav` pills: activa=azul, ok=verde ✓, bad=rojo ✗); derecha `.quiz-panel` (pregunta + `.feedback-box` + un botón `Comprobar`/`Siguiente pregunta`).
- Respuestas: caja blanca, borde `#dce6ef`; marcada = borde azul/fondo `#f0f6ff`; tras comprobar se bloquea (borde verde/fondo `#e9f8f0`).
- Feedback: `ok` verde, `bad` rojo, default gris azulado. Siempre visible.

### 6.10 Reporte de misión / reflexión (s24)
- `.canvas.reflection`: fondo gradiente `#15345f → #285aa6`, texto blanco.
- Izquierda: `h2` blanco + `.lead` blanco + `.pill-row` de conceptos.
- Derecha: `.card.white` con "Reflexión final" (h3 ink), 3 preguntas en `p` (ink), `<textarea>` grande con foco naranja.

---

## 7. Catálogo de componentes (copy-paste la estructura)

| Componente | Fondo/borde | Uso | Detalle |
|---|---|---|---|
| `.eyebrow` | `blue`, texto blanco | badge superior | pill 999px, weight 900; variantes `.orange` y `.green` |
| `.highlight` | — | palabra en naranja dentro de h1/p | `color: var(--orange)` |
| `.card` | `cream` / borde `#f2d7b2` | definiciones cálidas | radio 1.5cqw, shadow cálida; `.blue`→sky/#c6dff4; `.white`; `.dark` navy (extra: `.dark p` → `#eaf3ff`) |
| `.pill` | `#edf4fb` / `#d8e7f4`, texto navy | chips de etiquetas | pill 999px, weight 850 |
| `.quote` | blanco, borde izquierdo naranja | ejemplos/destacado | radio solo derecha |
| `.problem` | `#fff1f1` / `#f0b4b4`, texto `#8e2929` | errores/contraejemplos | weight 750 |
| `.steps-compact` | blanco / `--line` | pasos cortos numerados | círculos azules 1.7cqw |
| `.step-list` | — | algoritmos/escaleras | `list-style:decimal`, markers naranjas weight 900 |
| `.challenge-note` | `cream` / `#f2d7b2` | nota pedagógica principal | ícono naranja 2.6cqw; p weight 800 |
| `.pista-box` | `sky` / `#c6dff4` | pista técnica contextual | ícono azul 2.4cqw; p weight 600; texto normal para el cuerpo largo |
| `.flow-card` | blanco / `--line` | bloques en secuencia | círculo azul `.flow-n`; h3 `--fs-sub`; imagen `.card-img` max-height 20cqw; `.card-video` max-height 18cqw |
| `.gif-stage` | blanco / `--line` | preview de ejecución de escena | tag uppercase azul; img max-height 20cqw; caption `--fs-note` |
| `.definition` | `.card.blue` con `.icon` amarillo 5.2cqw | concepto con ícono | icono en `--yellow`, emoji 2.5cqw |
| `.image-placeholder` | gradiente azul→amarillo | lugar de imagen para video/imágen | texto blanco; `.orange` variante cálida |

**Íconos de nota:** `🎯` (challenge-note principal), `!` (misiones), `?` (pistas), `⏱` (pista-box de escenas).

---

## 8. Ajustes y observaciones aprendidas en la Guía 1 (anti-patrones)

- ❌ NO usar `--muted` (gris) para texto corporal → ✅ usar `--ink`.
- ❌ NO usar tamaños `clamp(…px…)` dentro del canvas → ✅ `cqw` puro (escala 1:1).
- ❌ NO repetir el título de la guía/escena en el slide del editor → ✅ editor a pantalla completa sin eyebrow.
- ❌ NO poner storyboards en las guías de escena → ✅ gif de la escena (`gif-stage`).
- ❌ NO duplicar el título con subtítulo en escenas → ✅ solo `h2`; "Tu misión" va en el panel derecho.
- ❌ NO textos largos que desborden → ✅ condensar y usar `.lead`/“--fs-sub` para ideas fuerza.
- ❌ NO escribir diálogos sin tiempo → ✅ siempre «durante X segundos».
- ❌ NO textos de botones inventados → ✅ `Regresar` / `Continuar` / `Comenzar misión`.
- ❌ NO dejar gap entre título, misión y recuadro inferior en escenas → ✅ `.9cqw` fijos en ambos puntos.
- ❌ NO cambiar el borde/radius de botones o cards por slide → ✅ tokenizar y reutilizar.
- La narrativa pide **coherencia total entre escenas**: tiempos acumulados de duración y segundo de inicio deben coincidir entre escenas consecutivas.

---

## 9. Checklist final de cada slide

1. [ ] Todas las medidas internas en `cqw`; sin px dentro del canvas.
2. [ ] Texto en `--ink` (sin grises).
3. [ ] Los 7.6cqw inferiores quedan libres para la barra de navegación.
4. [ ] Eyebrow correcto según tipo (azul concepto / naranja laboratorio-misión-reto-test / verde bloques).
5. [ ] Botones con nomenclatura correcta; puertas `locked` con `data-lab-gate`.
6. [ ] imágenes/gifs con `alt` descriptivo y `loading="lazy"`.
7. [ ] h2 sin subtítulo salvo briefing; guías de escena con la estructura §6.8 al pie de la letra.
8. [ ] Sin desborde en 1280×720 ni en 1920×1080.
9. [ ] Quiz: botón único, bloqueo tras comprobar, dots ✓/✗.
