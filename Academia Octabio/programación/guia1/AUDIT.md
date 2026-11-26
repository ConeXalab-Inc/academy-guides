# AUDIT.md — Diagnóstico inicial de Guía 1

## Archivos analizados

| Archivo | Ruta | Estado |
|---------|------|--------|
| HTML prototipo | `guia-algoritmos.html` | 738 líneas, 12 slides |
| Estándar MAMUS | `estandar-guias.pdf` | 1085 líneas de texto extraído |

---

## Slides existentes vs. estándar MAMUS

| # | Slide actual | Componente MAMUS esperado | Coincidencia |
|---|-------------|--------------------------|-------------|
| 1 | Briefing de misión | Briefing | ✅ Completo |
| 2 | Presaberes: instrucciones claras | Presaberes | ⚠️ Falta campo de respuesta |
| 3 | Presaberes: qué es un algoritmo | Presaberes | ⚠️ Falta comprobación |
| 4 | Laboratorio del minero nivel 1 | Laboratorio | ⚠️ Falta predicción y conclusión |
| 5 | Presaberes: debugging | Presaberes | ⚠️ 4 pasos, deben ser 5 |
| 6 | Laboratorio del minero nivel 2 | Laboratorio | ⚠️ Falta predicción y conclusión |
| 7 | Laboratorio del minero nivel 3 | Laboratorio | ⚠️ Falta predicción y conclusión |
| 8 | Programación en bloques | Presaberes | ✅ Completo |
| 9 | Ejemplo de algoritmo en bloques | **Miniproyecto** | ❌ Es demo estático, no Miniproyecto |
| 10 | Aventura de bloques (3 tabs) | **Misión 1 + ME1 + Misión 2 + ME2** | ❌ Un solo slide mezcla todo |
| 11 | MiniTest de misión | MiniTest | ⚠️ Sin persistencia |
| 12 | Reporte de misión | Reporte | ⚠️ Sin persistencia real |

---

## Brechas estructurales críticas

| Componente faltante | Según estándar MAMUS | Estado actual |
|--------------------|---------------------|---------------|
| Miniproyecto formal | Checkpoints, pasos numerados, variaciones | ❌ Demo visual estática en slide 9 |
| Misión 1 (secuencias+bucles) | Problema, requisitos, pruebas | ❌ No existe como slide separado |
| Misión especial 1 | Variante autónoma | ❌ No existe |
| Misión 2 (condicionales) | Problema, requisitos, pruebas | ❌ No existe como slide separado |
| Misión especial 2 | Variante autónoma combinada | ❌ No existe |

**Total actual: 12 slides → Total necesario: 15 slides (+3 nuevos)**

---

## Problemas técnicos encontrados

### Críticos
1. **Sin persistencia**: No se guarda slide actual, respuestas, progreso ni resultados
2. **Bloques macro-planos**: `Repetir 3 × avanzar` como bloque único sin jerarquía (`{ type: 'loop', count: 3, children: [...] }`)
3. **Sin inserción ni reordenamiento**: Los comandos solo se agregan al final
4. **Sin soporte táctil**: El block lab depende de HTML5 drag & drop que falla en móviles

> Los ítems 2–4 quedan obsoletos: el block lab (slide s10) se eliminó por completo en v0.7.0.
5. **Variables globales**: `slides`, `minerStates`, `quiz` en ámbito global

### Medios
6. **Sin pausa por scroll**: Solo hay `visibilitychange`, no `IntersectionObserver` en labs
7. **Sin accesibilidad**: Sin indicadores de foco, aria-live, soporte de teclado completo ni `prefers-reduced-motion` (el media query existe pero no hay lógica asociada)
8. **Sin navegación por teclado completa**: Las flechas izquierda/derecha y PageUp/PageDown funcionan, pero no hay atajos para laboratorios
9. **Sin campos de predicción/conclusión**: El ciclo pedagógico "predice → manipula → observa → compara → explica" está incompleto

### Menores
10. **Sin metadata de imagen accesible**: Los placeholders tienen descripción pero no `alt` text estructurado
11. **Ciclo de debugging con 4 pasos**: Debe incluir "Prueba nuevamente"
12. **Sin bloqueo de doble ejecución**: Hay chequeo básico pero no es robusto

---

## Componentes reutilizables del código actual

| Componente | Archivo línea | Estado |
|-----------|--------------|--------|
| Motor del minero (grid, comandos, ejecución, animación) | L495-L597 | ✅ Usable con refactorización |
| Sistema de navegación (goToSlide, IntersectionObserver, teclado) | L458-L487 | ✅ Usable con mejoras |
| Barra superior (progreso, contador) | L224-L228 | ✅ Usable |
| Overlays de misión (éxito/fallo/incompleto) | L557-L558 | ✅ Usable |
| Estructura CSS de slide 16:9, container queries | L41-L52 | ✅ Usable |
| Placeholder de imágenes reusable | L77-L86 | ✅ Usable |
| Motor de bloques (renderWorld, ejecución lineal) | L600-L709 | ⚠️ Refactorizar a jerárquico |
| MiniTest (preguntas, opciones, feedback) | L712-L729 | ✅ Usable con persistencia |

---

## Propuesta de estructura final (15 slides)

| # | Componente MAMUS | Propósito pedagógico | Estado |
|---|-----------------|---------------------|--------|
| 1 | Briefing de misión | Portada narrativa | Conservar + ajustar |
| 2 | Presaberes | Instrucciones claras | Añadir campo respuesta |
| 3 | Presaberes | Qué es un algoritmo | Añadir comprobación |
| 4 | Laboratorio | Minero nivel 1 (sin debug) | Añadir predicción + conclusión |
| 5 | Presaberes | Debugging (5 pasos) | Corregir ciclo |
| 6 | Laboratorio | Minero nivel 2 (debug) | Añadir predicción + conclusión |
| 7 | Laboratorio | Minero nivel 3 (debug completo) | Añadir predicción + conclusión |
| 8 | Presaberes | Programación en bloques | Conservar |
| 9 | **Miniproyecto** | Programa tu primer recorrido | **Rehacer completo** |
| 10 | **Misión 1** | Secuencias y bucles | **Nuevo** |
| 11 | **Misión especial 1** | Variante autónoma | **Nuevo** |
| 12 | **Misión 2** | Condicionales | **Nuevo** |
| 13 | **Misión especial 2** | Reto combinado autónomo | **Nuevo** |
| 14 | MiniTest de misión | 5 preguntas | Conservar + persistencia |
| 15 | Reporte de misión | Reflexión final | Conservar + persistencia |

---

## Plan de trabajo

1. **Fundación**: Persistencia, navegación mejorada, CSS accesibilidad
2. **Slides 1-8**: Ajustes incrementales (campos de respuesta, comprobación, predicción, conclusión, ciclo debugging)
3. **Slides 9**: Miniproyecto completo con motor interactivo y checkpoints
4. **Slides 10-13**: Cuatro misiones con motor jerárquico de bloques
5. **Slides 14-15**: MiniTest y Reporte con persistencia

---

*Auditado el 2026-08-05 contra el estándar MAMUS v1.0*
