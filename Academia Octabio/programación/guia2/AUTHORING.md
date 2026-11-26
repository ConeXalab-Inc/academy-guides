# Autoría de guías HTML para MAMUS

**Objetivo.** Una lección horizontal completa en un solo `guide.html`. El estudiante la ve con tu diseño; MAMUS guarda progreso, tiempos y respuestas, y decide si puede avanzar.

**Método.** Copia el esqueleto (o imita `guide.html`). Rellena diapositivas. Habla con MAMUS solo por `window.MamusGuide`. El validador comprueba el marcado; no hace falta memorizar el contrato interno.

No inventes otra navegación, otra persistencia ni otros scripts de runtime. La única entrada pública es `mamus-guide.js`.

En local la navegación es libre. Los gates del estudiante se comprueban en MAMUS, no en el preview.

---

## 1. Esqueleto

```html
<!doctype html>
<html lang="es" data-mamus-guide-version="1">
<head>
  <meta charset="utf-8" />
  <title>Título de la guía</title>
  <link rel="stylesheet" href="mamus/mamus-guide-shell.css" data-mamus-runtime />
  <link rel="stylesheet" href="mamus/mamus-guide-theme.css" data-mamus-runtime />
  <script src="mamus/mamus-guide.js" data-mamus-runtime></script>
  <style>
    .mamus-guide__canvas { container-type: inline-size; }
  </style>
</head>
<body class="mamus-guide" data-design-width="1920" data-design-height="1080">
  <div class="mamus-guide__viewport">
    <div class="mamus-guide__scaler">

      <section class="mamus-guide__slide is-active"
               data-slide-id="portada"
               data-title="Portada"
               data-mamus-speech="Frase pensada para escucharse, no un volcado del DOM.">
        <div class="mamus-guide__canvas">
          <div class="mamus-guide__columns">
            <div class="mamus-guide__column" data-width="60">
              <h1>Título</h1>
              <p>Contenido.</p>
            </div>
            <div class="mamus-guide__column" data-width="40">
              <p>Apoyo.</p>
            </div>
          </div>
        </div>
      </section>

    </div>
  </div>

  <nav class="mamus-guide__toolbar" aria-label="Controles de la guía">
    <button type="button" data-mamus-prev>Regresar</button>
    <span data-mamus-counter>1 / 1</span>
    <button type="button" data-mamus-zoom-out aria-label="Alejar">−</button>
    <button type="button" data-mamus-zoom-in aria-label="Acercar">+</button>
    <button type="button" data-mamus-speak aria-label="Leer">▶</button>
    <button type="button" data-mamus-fullscreen aria-label="Pantalla completa">⛶</button>
    <button type="button" data-mamus-next>Continuar</button>
  </nav>

  <div class="mamus-guide__rotate-notice">
    <p>Gira el dispositivo.</p>
    <button type="button" data-mamus-dismiss-rotate>Continuar así</button>
  </div>
</body>
</html>
```

No listes `protocol.js`, `runtime.js` ni el harness: el loader los carga. No pongas la barra ni el aviso de rotación dentro del viewport. No marques `is-active` más que en la primera diapositiva.

Al publicar, MAMUS retira las etiquetas `data-mamus-runtime` e inyecta su copia.

---

## 2. Lienzo

**Objetivo.** Cada diapositiva es una lámina 1920×1080. MAMUS la escala; tú no adaptas al viewport.

**Método.** Jerarquía exacta: `viewport → scaler → slide → canvas → columns → column`. Una o dos columnas; `data-width` suma 100. Tipografía en `px` o `cqw` relativos al canvas. Si el bloque puede crecer, envuélvelo en `mamus-guide__scrollable`. A sangre: `mamus-guide__canvas is-flush`.

```html
<section class="mamus-guide__slide" data-slide-id="idea" data-title="Una idea">
  <div class="mamus-guide__canvas">
    <div class="mamus-guide__columns">
      <div class="mamus-guide__column" data-width="100">
        <div class="mamus-guide__scrollable">
          <ol>
            <li>Paso que puede alargarse.</li>
          </ol>
        </div>
      </div>
    </div>
  </div>
</section>
```

No uses `vw` / `vh` en el contenido. No pongas tres columnas del shell (maqueta paneles extra *dentro* de una columna). No uses `position: fixed` en contenido: se sale de la escala. No pelees la transición con `display` / `visibility` en `.mamus-guide__slide`. No reutilices un `data-slide-id` ya publicado.

---

## 3. Barra

**Objetivo.** El estudiante cambia de diapositiva, hace zoom, escucha y entra a pantalla completa con *tu* barra. El look es tuyo; los ganchos son de MAMUS.

**Método.** Una barra fuera del scaler, con `data-mamus-prev`, `data-mamus-counter`, `data-mamus-next`, `data-mamus-zoom-out`, `data-mamus-zoom-in`, `data-mamus-speak` y `data-mamus-fullscreen`. Opcionales: `data-mamus-progress`, `data-mamus-zoom-fit`. Dentro de una diapositiva puedes repetir `data-mamus-next` / `data-mamus-prev` («Comenzar →»).

No montes una segunda barra. No toques `disabled` ni clases de estado (`is-first`, `narr-on`, `fs-active`…): el runtime las escribe. No implementes `scroll-snap`, anclas ni `scrollIntoView` para pasar de lámina.

Un IDE o un vídeo a sangre no debe hacer zoom:

```html
<section class="mamus-guide__slide"
         data-slide-id="editor-bloques"
         data-title="Editor"
         data-mamus-zoom="lock">
```

---

## 4. Reto

**Objetivo.** No avanzar hasta resolver la actividad.

**Método.** Marca la diapositiva y avisa una vez al completar. Pausa la simulación al salir.

```html
<section class="mamus-guide__slide"
         data-slide-id="laboratorio"
         data-title="Laboratorio"
         data-gate="challenge">
```

```js
window.MamusGuide.completeChallenge();

window.MamusGuide.on('mamus-guide:slide-leave', (event) => {
  if (event.detail.slideId === 'laboratorio') pausarSimulacion();
});
window.MamusGuide.on('mamus-guide:slide-enter', (event) => {
  if (event.detail.slideId === 'laboratorio') prepararSimulacion();
});
```

No deshabilites el botón siguiente a mano. No dejes temporizadores corriendo en una lámina invisible. Si la actividad usa flechas o espacio, reclama el teclado y suéltalo:

```js
window.MamusGuide.captureKeyboard(true);
window.MamusGuide.captureKeyboard(false);
```

---

## 5. Cuestionario

**Objetivo.** Un solo minitest calificable por guía. El estudiante elige, comprueba, y no sale hasta responder todas. No hay segundo intento.

**Método.** Una diapositiva `data-mamus-quiz="graded"` con `data-quiz-id`. Cada pregunta es un `.mamus-question`. Deja `[data-mamus-question-nav]` vacío; el runtime lo rellena. `data-correct` viaja en autoría; MAMUS lo retira al publicar.

```html
<section class="mamus-guide__slide"
         data-slide-id="minitest"
         data-title="Minitest"
         data-mamus-quiz="graded"
         data-quiz-id="minitest-guia-1">
  <div class="mamus-guide__canvas">
    <div class="mamus-guide__columns">
      <div class="mamus-guide__column" data-width="100">
        <nav class="mamus-question-nav" data-mamus-question-nav aria-label="Preguntas"></nav>
        <article class="mamus-question is-active"
                 data-question-id="q1"
                 data-correct="b"
                 data-feedback-correct="Porque 2+2 es 4."
                 data-feedback-wrong="Revisa la suma.">
          <h3>¿Cuánto es 2+2?</h3>
          <button type="button" class="mamus-choice" data-option-id="a">3</button>
          <button type="button" class="mamus-choice" data-option-id="b">4</button>
          <p data-mamus-feedback>Selecciona y comprueba.</p>
          <button type="button" data-mamus-check>Comprobar</button>
        </article>
      </div>
    </div>
  </div>
</section>
```

No pongas un segundo `data-mamus-quiz="graded"`. No uses `data-question-id` en un check de práctica: bloquearía la salida. La práctica es JavaScript tuyo; si quieres registrarla:

```js
window.MamusGuide.notifyFormative({
  slideId: 'presaberes',
  actividad: 'check-algoritmo',
  acierto: true,
});
```

No cambies un `data-question-id` ya publicado.

---

## 6. Texto libre

**Objetivo.** Guardar lo que escribe el estudiante sin un botón «Guardar».

```html
<textarea data-mamus-open-answer="prediccion-bug"></textarea>
```

No uses `localStorage`, cookies ni `fetch` para progreso.

---

## 7. Embeds

**Objetivo.** Un IDE o un vídeo ocupa el lienzo; la barra de la guía se queda abajo.

```html
<section class="mamus-guide__slide"
         data-slide-id="editor-bloques"
         data-title="Editor de bloques"
         data-mamus-zoom="lock">
  <div class="mamus-guide__canvas is-flush">
    <div class="mamus-guide__columns is-stretch">
      <div class="mamus-guide__column" data-width="100">
        <div class="blocks-embed">
          <iframe src="https://blocks.octabio.co"
                  title="Editor de bloques"
                  loading="lazy"
                  allowfullscreen></iframe>
        </div>
      </div>
    </div>
  </div>
</section>
```

No montes un overlay «Volver a la guía». No cargues CDNs, fuentes remotas ni analíticas. Assets propios: rutas relativas. No metas `.php` ni `.htaccess` en el ZIP.

---

## 8. Interface

Toda conversación con MAMUS pasa por `window.MamusGuide`. No leas globals internos ni envíes `postMessage` a mano.

| Para | Cómo |
| --- | --- |
| Cerrar un reto | `completeChallenge()` |
| Práctica sin nota | `notifyFormative({ ... })` |
| Teclado de una actividad | `captureKeyboard(true\|false)` |
| Pausar al cambiar de lámina | `on('mamus-guide:slide-enter' \| 'mamus-guide:slide-leave', ...)` |
| Saber dónde está | `getCurrentSlide()` → `{ id, index, title }` |

`requestNext` / `requestPrev` piden el cambio; MAMUS puede responder `mamus-guide:navigation-denied` (`gate-pending`, `quiz-pending`, `out-of-bounds`). Zoom, lectura y pantalla completa ya los cubre la barra: no armes otra.

---

## 9. Entrega

```
1/
  type.txt      # html-guide
  guide.html
  assets/       # opcional
```

No pongas `layout.txt=vertical`. No mezcles otros tipos de slide. Abre `guide.html` y recorre barra, zoom y lectura. Los retos y el minitest se verifican en MAMUS como estudiante.
