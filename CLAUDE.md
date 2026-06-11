# ExamPrince7Generator — Contexto del proyecto

Simulador de examen **PRINCE2 7ª Edición Foundation** completo, construido como aplicación web single-page en español.

## Archivos

| Archivo | Descripción |
|---|---|
| `index.html` | Toda la app: CSS + HTML + JavaScript en un único fichero (~279 KB, ~2746 líneas) |
| `server.js` | Servidor estático Node.js mínimo en el puerto 5151 |

Para lanzar: `node server.js` → http://localhost:5151

## Arquitectura de index.html

El fichero tiene tres bloques secuenciales:

1. **`<style>`** (líneas ~6–346): variables CSS, componentes (cards, options, timer, history, toast…)
2. **HTML** (líneas ~348–550): cuatro pantallas (`screen-home`, `screen-exam`, `screen-results`, `screen-history`) + toast
3. **`<script>`** (línea ~551 en adelante):
   - `QUESTION_BANK`: array de objetos con todas las preguntas
   - Lógica de la app: configuración, examen, temporizador, resultados, historial en `localStorage`

## Estructura de una pregunta

```js
{
  id: 1,
  topic: "Visión general",       // ver lista de temas abajo
  difficulty: "easy",            // "easy" | "medium" | "hard"
  question: "¿Texto...?",
  options: ["A", "B", "C", "D"],
  correct: 2,                    // índice base-0 de la opción correcta
  explanation: "Texto explicativo..."
}
```

## Temas existentes en el banco de preguntas

- `"Visión general"` — principios, prácticas, procesos, conceptos clave (output/outcome/benefit, tolerancias, etapas…)
- `"Prácticas - Caso de negocio"`
- `"Prácticas - Organización"`
- `"Prácticas - Planes"`
- `"Prácticas - Calidad"`
- `"Prácticas - Riesgo"`
- `"Prácticas - Cuestiones"`
- `"Prácticas - Progreso"`
- `"Proceso - Puesta en marcha de un proyecto"`
- `"Proceso - Inicio de un proyecto"`
- `"Proceso - Dirección de un proyecto"`
- `"Proceso - Control de una etapa"`
- `"Proceso - Gestión de la entrega de productos"`
- `"Proceso - Gestión de los límites de etapa"`
- `"Proceso - Cierre de un proyecto"`
- `"Personas"` — liderazgo, gestión del cambio organizacional (temas nuevos en la 7ª edición)
- `"Examen de muestra 1"` — las 60 preguntas del examen de muestra oficial de PeopleCert (IDs 557–616), con respuestas y explicaciones de la clave oficial; todas con dificultad `medium`. Agrupado en el selector bajo "Exámenes oficiales".
- `"Examen de muestra 2"` — las 60 preguntas del segundo examen de muestra oficial de PeopleCert (IDs 617–676), con respuestas y explicaciones de la clave oficial; todas con dificultad `medium`. Agrupado en el selector bajo "Exámenes oficiales".

## Banco de preguntas

- **676 preguntas** (IDs del 1 al 676), en español
- Distribuidas entre easy / medium / hard
- El selector de temas en la pantalla Home se genera desde `TOPIC_GROUPS` / `TOPIC_LABELS` (en el `<script>`): los temas nuevos requieren añadir el tema a un grupo y, opcionalmente, una etiqueta corta

## Funcionalidades de la app

- **Configuración**: dificultad, filtro por tema, nº de preguntas (10/20/30/40/60), tiempo límite (sin límite / 15–90 min), mostrar explicaciones al responder o al finalizar
- **Examen**: temporizador en tiempo real con alertas de color (amarillo < 10 min, rojo < 3 min), navegación libre entre preguntas, marcado de respuestas
- **Resultados**: puntuación %, APROBADO/SUSPENDIDO (umbral 65%), estadísticas, revisión completa de respuestas con explicaciones
- **Historial**: guardado en `localStorage`, con opción de borrar

## Contexto del examen real PRINCE2 7 Foundation

- 60 preguntas de opción múltiple
- 60 minutos
- Umbral de aprobación: **65% (39/60 correctas)**
- Cubre 7 Principios · 7 Prácticas · 7 Procesos

## Convenciones para modificar

- Todo va en `index.html`; no crear ficheros JS/CSS separados salvo que se pida explícitamente.
- Al añadir preguntas, respetar el formato del objeto y asignar un `id` único correlativo.
- Para que un tema nuevo aparezca en el selector hay que añadirlo a `TOPIC_GROUPS` (y su etiqueta corta a `TOPIC_LABELS`); no hace falta tocar el HTML.
- El servidor `server.js` no necesita modificarse para cambios en la app.
