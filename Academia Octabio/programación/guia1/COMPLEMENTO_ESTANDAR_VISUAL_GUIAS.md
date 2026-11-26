# Complemento visual y de formato para guias digitales MAMUS

Documento complementario a `nivel1/guia1/estandar-guias.pdf`.

Base de analisis: `nivel1/guia1/index.html`, `nivel1/guia2/index.html`, `nivel1/guia3/index.html`, `nivel1/guia4/index.html` (con enfasis en guias 3 y 4).

Objetivo: que, con este archivo + `estandar-guias.pdf` + una idea de sesion, la IA pueda generar una guia casi lista para implementar, coherente, progresiva y visualmente unificada.

---

## 1) Como usar este complemento

- `estandar-guias.pdf` define la pedagogia y la secuencia macro (Briefing -> Presaberes -> Laboratorio -> Miniproyecto -> Mision -> Mision especial -> MiniTest -> Reporte).
- Este `.md` define la capa de implementacion visual: estructura de slides, etiquetas, componentes UI, uso de imagenes, y reglas de consistencia entre guias.
- En caso de conflicto: **primero el PDF**, luego este complemento.

---

## 2) Hallazgos clave de estandarizacion (guias 1-4)

1. La base visual de `guia3` y `guia4` es la mas madura y debe ser el patron por defecto.
2. El panel de navegacion inferior ya esta estandarizado en `guia3/4` con `data-nav` + `navMarkup()` y debe usarse igual en todas.
3. Hay inconsistencia en la etiqueta superior (eyebrow): en guias previas depende demasiado del contenido puntual (`Buscando a Nemo 2 - Escena 4`, `Conoce a Octabio`, etc.).
4. La presencia visual es alta en guias recientes (aprox. `guia3: 87.9%`, `guia4: 92.0%` de slides con recurso visual). Este nivel debe mantenerse.

---

## 3) Sistema visual base obligatorio

Tomar como referencia la base de `guia3`/`guia4`:

- Lienzo 16:9, `canvas` centrado, fondo exterior degradado suave.
- Tokens de color institucionales (`--navy`, `--blue`, `--orange`, `--green`, `--red`, `--ink`, `--paper`, `--line`).
- Tipografia y escala unificadas (`--fs-title`, `--fs-sub`, `--fs-body`, `--fs-note`).
- Contenido interno con layout en rejilla y reserva inferior para navegacion (`padding-bottom` con espacio para nav).
- Componentes reutilizables: `card`, `pista-box`, `challenge-note`, `pill-row`, `flow-row`, `quiz-layout`, `reflection`.

### 3.1 Estructura HTML minima de cada slide

```html
<section class="slide" id="sN" data-title="Titulo descriptivo del slide">
  <div class="canvas">
    <div class="slide-eyebrow"><div class="eyebrow">Tipo de slide</div></div>
    <div class="content">
      <!-- contenido -->
    </div>
    <div class="lesson-nav" data-nav></div>
  </div>
</section>
```

Reglas:

- Todos los slides llevan `lesson-nav` con `data-nav`.
- Slides de solo editor pueden omitir eyebrow y texto principal.
- `data-title` debe describir el objetivo del slide (sirve para titulo del documento y navegacion).

---

## 4) Taxonomia estandar de etiquetas superiores (eyebrow)

Para evitar etiquetas dependientes del contenido narrativo, usar vocabulario controlado.

### 4.1 Etiquetas permitidas

| Componente | Eyebrow estandar | Color sugerido |
|---|---|---|
| Portada | `Portada` (o `Guia X - Nivel Y` solo en slide 1) | orange |
| Briefing | `Briefing` | purple u orange |
| Activacion | `Activacion` | green |
| Presaber/concepto | `Concepto` | blue |
| Laboratorio | `Laboratorio` | orange |
| Miniproyecto guiado | `Miniproyecto` | orange |
| Mini reto guiado | `Mini reto` | orange |
| Mision principal | `Mision` | orange |
| Mision de transferencia | `Mision especial` | red u orange |
| Construccion fisica | `Construccion` | green |
| Conexion de hardware | `Conexion` | orange |
| Programacion | `Programacion` | orange |
| Verificacion/ajuste | `Pruebas` | purple |
| Evaluacion | `MiniTest` | purple |
| Cierre | `Cierre` | orange |

### 4.2 Regla de consistencia

- El nombre especifico del reto va en `h2` y `data-title`, **no** en eyebrow.
- Si una etapa tiene varias pantallas, usar subtipo fijo: `Mision - Parte guiada`, `Mision - Implementacion`, `Mision - Verificacion`.
- Evitar eyebrows narrativos inestables como `Escena 2`, `Conoce a...`, `Nuevo uso de...`.

---

## 5) Orden estandar de la sesion (implementacion en slides)

Mantener la secuencia del PDF, con la siguiente traduccion visual.

### 5.1 Sesion de 2 horas (1 mision)

1. Portada (1 slide)
2. Briefing (1 slide)
3. Activacion de presaberes (1 slide)
4. Bloque de conceptos (3 a 6 slides, con imagen + ejemplo)
5. Laboratorio o mini reto exploratorio (1 a 3 slides)
6. Miniproyecto guiado por replicacion (2 a 5 slides + editor)
7. Mision (2 a 5 slides + editor)
8. Mision especial (1 a 3 slides + editor opcional)
9. MiniTest (1 slide, 5 preguntas)
10. Cierre/reflexion (1 slide)

### 5.2 Sesion de 4 horas (2 misiones)

1. Portada -> Briefing -> Activacion
2. Ciclo 1: Conceptos + Laboratorio + Miniproyecto
3. Mision 1 + Mision especial 1
4. Ciclo 2 (si aplica): Conceptos + Laboratorio + Miniproyecto
5. Mision 2 + Mision especial 2
6. MiniTest (unico al final)
7. Cierre/reflexion (unico al final)

---

## 6) Plantillas de componentes (nivel visual + contenido)

## 6.1 Portada

Debe contener siempre:

- Imagen a pantalla completa (`briefing-bg-img`) coherente con la sesion.
- Mega titulo (`h1`) con una palabra destacada (`.highlight`).
- Texto introductorio breve (`lead`).
- Datos de sesion (guia, duracion, ruta/tema) en `briefing-meta`.
- Pregunta orientadora en `pista-box`.

No incluir en portada:

- Lista larga de objetivos, materiales o instrucciones extensas.

## 6.2 Briefing

- Explica que se lograra/construira hoy.
- Combina texto + imagen principal.
- Debe conectar explicitamente con la mision (que problema resuelve).

## 6.3 Activacion de conocimientos previos

- Usar 3 o 4 tarjetas `quick-check`.
- Cada tarjeta: imagen representativa + concepto breve + pregunta con 2 opciones + feedback inmediato.
- Preguntas cortas, enfocadas, no triviales.

## 6.4 Conceptos

- Una idea central por slide.
- Casi siempre en layout de dos columnas: texto + apoyo visual.
- Incluir imagen, gif, diagrama o demo visual en cada concepto.
- Si el recurso no existe aun, incluir placeholder de imagen (ver seccion 8).

## 6.5 Mini retos / laboratorios

- Deben permitir experimentacion (no solo lectura).
- Estructura minima: consigna -> accion del estudiante -> observacion -> conclusion.
- Agregar una pregunta de interpretacion al cierre.

## 6.6 Actividades guiadas (miniproyecto por replicacion)

- Mostrar resultado esperado.
- Dividir en pasos claros con checkpoints.
- Mantener apoyo visual por paso (captura, gif o diagrama).
- Incluir al menos un ejercicio de variacion al final.

## 6.7 Misiones

- Presentar problema, requisitos y criterio de exito.
- No entregar la solucion completa.
- Para misiones largas, dividir en fases visuales estables (preparacion, construccion, programacion, pruebas).

## 6.8 Tipos de editor

- Scratch: `shared-slot` o `blocks-embed` con entorno de bloques Scratch.
- Robotica Octabio: `shared-slot` o `blocks-embed` para Octabio Blocks + slides de construccion/conexion.
- Python: mismo patron de flujo que Scratch, cambiando a editor Python (concepto -> mini reto -> guiado -> mision).

## 6.9 MiniTest (formato guia 4)

- 1 slide con `quiz-layout` y 5 preguntas.
- 4 opciones por pregunta, plausibles y de longitud parecida.
- Sin respuestas obvias por forma, longitud o palabras absolutas.
- Feedback explicativo tras comprobar (no solo correcto/incorrecto).

## 6.10 Cierre/reflexion

- Resumen con una idea central de la sesion.
- Tags/pills de conceptos trabajados.
- Una sola pregunta de transferencia/reflexion abierta.
- Campo de respuesta breve (bitacora de salida).

---

## 7) Panel de navegacion inferior (estandar unico)

Debe ser identico en todas las guias:

- Boton izquierda: `Regresar` (excepto primer slide).
- Barra de progreso central + contador `actual/total`.
- Grupo de controles: zoom -, ajustar, zoom +, fullscreen, narracion.
- Boton derecha: `Continuar` / `Terminar leccion` en ultimo slide.

Regla tecnica:

- Generar markup via `navMarkup()` y renderizar con `document.querySelectorAll('[data-nav]')`.
- No hardcodear barras de navegacion distintas por slide.

---

## 8) Estandar de uso de imagenes y placeholders

Meta:

- Minimo recomendado: **85% de slides con apoyo visual** (imagen, gif, video, diagrama o demo).
- Excepciones validas: editor puro, MiniTest, o una slide de transicion muy corta.

Cuando no exista recurso final, la IA debe proponer recuadro editable:

```html
<div class="image-placeholder">
  <strong>Imagen sugerida</strong>
  <span>[Descripcion visual concreta de lo que debe verse y por que ayuda a comprender el concepto]</span>
  <small>Alt sugerido: [texto alt descriptivo para accesibilidad]</small>
</div>
```

Adicionalmente, en el guion de la IA incluir por cada imagen:

- Tipo (`ilustracion`, `gif`, `foto`, `captura`, `diagrama`).
- Objetivo pedagogico.
- Prompt sugerido para produccion visual.
- `alt` sugerido.

---

## 9) Estandar para actividades por tipo (Scratch, robotica, Python)

## 9.1 Scratch

- Priorizar ejemplos visuales de bloques + ejecucion esperada.
- Usar reto corto antes del editor para que lleguen con hipotesis.
- En guiado, incluir checkpoints verificables.

## 9.2 Robotica con Octabio

- Secuencia recomendada: concepto -> elemento -> construccion -> conexion -> programacion -> pruebas.
- Cada paso de construccion debe tener apoyo visual (foto/gif/diagrama).
- Incluir al menos una slide de ajuste de umbral/calibracion o validacion.

## 9.3 Python (a implementar en nuevas guias)

- Misma progresion pedagogica que Scratch.
- Mantener equivalencias visuales Scratch <-> Python cuando aplique.
- Incluir ejemplos de codigo cortos, ejecutables y con salida esperada.
- Evitar teoria aislada sin testbench o mini experimento.

---

## 10) Reglas de calidad de preguntas (MiniTest)

Checklist obligatorio por pregunta:

1. Evalua comprension aplicada, no memoria literal.
2. 4 opciones plausibles.
3. Longitud similar entre opciones.
4. Solo una correcta sustentable.
5. Feedback de 2 a 4 frases:
   - por que la correcta funciona,
   - como se relaciona con la sesion,
   - cual es la confusion comun.

Reglas anti-sesgo:

- No usar `todas las anteriores` / `ninguna de las anteriores`.
- No repetir patrones de respuesta correcta en la misma posicion.
- Evitar opcion claramente mas larga o mas tecnica que delate la correcta.

---

## 11) Formato de salida que debe producir la IA

Cuando se le pida crear una guia, la IA debe entregar:

1. **Mapa de sesion** (objetivo, progresion y evidencias).
2. **Tabla de slides** con columnas:
   - `#`
   - `Componente`
   - `Eyebrow estandar`
   - `Titulo del slide`
   - `Objetivo del slide`
   - `Interaccion`
   - `Recurso visual o placeholder`
3. **Borrador de contenido por slide** casi implementable (titulos, textos, preguntas, feedback).
4. **Lista de assets pendientes** para docente/desarrollador.
5. **Checklist final de cumplimiento** (estructura + visual + evaluacion + cierre).

---

## 12) Checklist final de estandarizacion visual

- [ ] La secuencia respeta el PDF (estructura oficial).
- [ ] Portada incluye mega titulo, intro, datos y pregunta orientadora.
- [ ] Navegacion inferior es unica y consistente en todos los slides.
- [ ] Eyebrows usan vocabulario controlado (no etiquetas narrativas inestables).
- [ ] Activacion tiene 3-4 tarjetas con pregunta de 2 opciones y feedback.
- [ ] Casi todos los conceptos tienen apoyo visual (>=85% de slides con recurso visual).
- [ ] Mini retos/labs permiten experimentacion y cierre interpretativo.
- [ ] Misiones plantean problema y criterios sin dar solucion completa.
- [ ] MiniTest tiene exactamente 5 preguntas con opciones plausibles y feedback explicativo.
- [ ] Cierre resume idea central + pregunta de transferencia.

---

## 13) Regla maestra de este complemento

La guia debe sentirse como una **misma familia visual y narrativa** entre sesiones: cambia el contenido, pero no cambia la experiencia base de navegacion, etiquetas, estructura, ritmo didactico y claridad visual.
