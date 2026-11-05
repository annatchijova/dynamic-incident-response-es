# Un enfoque dinámico de la respuesta a incidentes (el modelo DAIR)

> Guía de estudio en español — síntesis propia, no traducción. Basado en "A Dynamic Approach to Incident Response", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/dynamicapproach.html

**Este es el capítulo bisagra del libro.** Todo lo anterior (historia, modelos existentes y sus límites) es la justificación para este capítulo; todo lo posterior (Prepare → Debrief) es el desarrollo operativo de lo que acá se define.

## Tesis

Los incidentes modernos no son lineales y la respuesta es, por naturaleza, iterativa. Modelos como PICERL o NIST SP 800-61 imponen fronteras secuenciales artificiales que no reflejan cómo ocurre realmente una investigación: actividades que se superponen, análisis que obliga a volver sobre pasos "ya cerrados".

## Vocabulario fundacional del modelo

- **Waypoints**: puntos de decisión en el proceso — no "pasos" con inicio y fin discretos, sino hitos.
- **Outcomes**: resultados deseados en cada waypoint.
- **Actions**: actividades recurrentes o continuas (no eventos puntuales) que se sostienen a lo largo del proceso.
- **Coordinación con decision-makers**: capa persistente que envuelve todo el proceso. Los stakeholders aportan contexto de negocio — prioridad, criticidad de sistemas, sensibilidad de datos, impacto operativo aceptable — que el equipo de respuesta (IRT) no puede inferir solo.

## Los cinco waypoints

1. **Prepare** — que el IRT tenga, antes de que ocurra el incidente, las habilidades, herramientas y procedimientos necesarios (entrenamiento, adquisición de herramientas, desarrollo de políticas).
2. **Detect** — monitoreo continuo, incluyendo *threat hunting* y descubrimiento de incidentes: identificar EOIs vía sistemas de monitoreo, alertas y búsqueda proactiva.
3. **Verify and Triage** — acciones concurrentes: verificar que el EOI observado es efectivamente un incidente (evitar gastar recursos en falsos positivos) y priorizar según objetivos de negocio, no solo severidad técnica.
4. **Response Actions Loop** — el componente iterativo central del modelo (ver abajo).
5. **Debrief** — evaluación posterior: fortalezas/debilidades del sistema y de la respuesta, captura de métricas para mejora continua.

## El Response Actions Loop — cuatro pasos internos, cíclicos

- **Scope**: determinar la amplitud real del compromiso — qué sistemas tienen IOCs, qué TTPs usó el atacante, qué sistemas de negocio están afectados. El *scoping* es continuo: cada hallazgo analítico puede ampliar lo que se entiende por "alcance" del incidente.
- **Contain**: aislar sistemas afectados para frenar la propagación (segmentación de red, restricción de accesos, baja de sistemas). La estrategia de contención balancea aislamiento exhaustivo contra continuidad de negocio.
- **Eradicate**: remover amenazas conocidas y mecanismos de persistencia. Puede revelar TTPs del atacante que no se conocían antes — y eso obliga a volver al paso de Scope.
- **Recover**: restaurar sistemas a estado operativo, por limpieza o por reemplazo con versiones limpias. La recuperación valida que la erradicación efectivamente removió todo el compromiso.

Estos cuatro pasos se repiten en ciclo a medida que aparece información nueva — es la manifestación concreta de "no linealidad" que el modelo reclama como su aporte central.

## Comparación explícita con PICERL / NIST SP 800-61

Los modelos tradicionales presentan la respuesta como pasos secuenciales (Preparation → Detection → Containment → Eradication → Recovery → Lessons Learned), con fronteras artificiales que sugieren que cada fase termina antes de que empiece la siguiente. DAIR rechaza esa linealidad: la detección sigue ocurriendo durante toda la respuesta, el análisis hecho durante la erradicación puede obligar a ampliar el *scoping*, y contención/recuperación ocurren de forma iterativa, no secuencial. El propio libro aclara que aunque DAIR tiene semejanza conceptual con los marcos existentes, "la forma en que aplicamos el modelo DAIR y lo que enfatizamos como acciones esenciales es diferente" (paráfrasis cercana del original).

## Relación con el ciclo OODA de Boyd

El capítulo no menciona explícitamente el ciclo OODA (Observe-Orient-Decide-Act) de Boyd en esta sección, pero el ciclo Scope-Contain-Eradicate-Recover refleja su misma estructura: orientación continua basada en información nueva, iteración rápida en vez de progresión lineal. (La FAQ del sitio oficial sí afirma explícitamente que "DAIR is built on Boyd's OODA loop" — la conexión se vuelve explícita ahí aunque en el cuerpo de este capítulo quede más implícita.)

## Figuras del capítulo (según el original — consultar el PDF/HTML para el detalle visual)

- **Figura 1**: diagrama de flujo de DAIR — waypoints lineales (Prepare → Debrief) con el Response Actions Loop representado como círculo no lineal (Scope/Contain/Eradicate/Recover).
- **Figura 2**: "Stepped Approach" — Contain y Eradicate como bloques secuenciales con fronteras duras entre "Isolate/Evidence Gathering" y "Evidence Analysis/Remove Persistence".
- **Figura 3**: "Waypoints and Actions" — las mismas actividades, pero representadas como barras en degradé que se superponen sin frontera dura, mostrando el contraste con la Figura 2.
- **Figura 4**: DAIR con la capa de coordinación de decision-makers envolviendo todo el proceso.
- **Figura 5**: el waypoint "Verify and Triage" resaltado dentro de la estructura del modelo.

## Ejemplo de coordinación con decision-makers (resumen)

El libro plantea un escenario de quince sistemas comprometidos: cinco servidores de base de datos de producción que generan USD 500.000/hora, y diez estaciones de trabajo del área de finanzas. Sin input de los decision-makers, el IRT investigaría todo por igual. Con coordinación, el liderazgo aporta contexto clave: la caída de la base de datos requiere notificación por SLA, las estaciones de finanzas no tienen acceso a datos sensibles de clientes, y la prioridad operativa es continuidad del servicio al cliente. El IRT ajusta su respuesta en consecuencia: respuesta en vivo sobre producción durante ventanas de bajo tráfico, y segmentación de red para finanzas recién después del cierre trimestral. La idea central: las acciones de respuesta se alinean con las prioridades de la organización, no con perseguir cada pista técnica por igual.

## Advertencias explícitas

- La coordinación con decision-makers no es opcional: el equipo de respuesta debe buscar activamente su guía durante todo el ciclo de vida del incidente.
- Sin esa coordinación, el IRT puede tomar acciones técnicamente correctas pero organizacionalmente dañinas — el ejemplo que da el libro es poner *todos* los sistemas offline simultáneamente para hacer imaging.
- El equipo de respuesta no puede operar aislado de las prioridades de negocio y la realidad operativa de la organización.

## Herramientas y tecnologías nombradas

Ninguna marca o producto específico — el capítulo habla en términos genéricos de "sistemas de monitoreo", "alertas", "análisis de sistema de archivos", "segmentación de red", "recolección forense".

## Relación con otros capítulos

- Es la síntesis directa de la crítica hecha en "Incident Response Models and Their Limitations" ([03-modelos-existentes.md](03-modelos-existentes.md)).
- Cada uno de los cinco waypoints tiene su propio capítulo de desarrollo operativo: Prepare, Detect, Verify and Triage, Response Actions Loop, Scope, Contain, Eradicate, Recover, Debrief.
- El crosswalk formal con NIST CSF 2.0 (mencionado acá solo de pasada) se desarrolla a fondo en "Integrating DAIR with NIST CSF 2.0".

## Preguntas de estudio

1. Dar un ejemplo propio (no el de la base de datos/finanzas) donde ignorar a los decision-makers lleve a una acción "técnicamente correcta pero organizacionalmente dañina".
2. ¿Por qué separar "Verify" de "Triage" como una sola acción concurrente, en vez de dos waypoints distintos, es coherente con la tesis de no linealidad del modelo?
3. ¿En qué se diferencia reescribir Contain→Eradicate como barras superpuestas (Figura 3) de representarlas como bloques secuenciales (Figura 2), en términos de qué decisión operativa habilita cada representación?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "A Dynamic Approach to Incident Response". CC BY 4.0. https://dynamicincidentresponse.com/chapters/dynamicapproach.html
