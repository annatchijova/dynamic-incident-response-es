# Response Actions Loop

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Response Actions Loop", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/responseactionsloop.html — ver también el anexo oficial [step-by-step-response-actions-loop.md](../anexos/step-by-step-response-actions-loop.md).

## Propósito

Formalizar por qué Scope-Contain-Eradicate-Recover es un ciclo y no una secuencia: cada pasada genera información nueva que obliga, en muchos casos, a repetir un paso anterior. La respuesta a incidentes es, en palabras del capítulo, un proceso de aprendizaje.

**Distinción importante con el ciclo OODA de Boyd**: el loop de DAIR optimiza para la exhaustividad de todo el equipo a través de múltiples investigaciones simultáneas, no para la velocidad de decisión de un individuo — que es lo que OODA prioriza en escenarios de combate. Son ciclos iterativos emparentados, pero con objetivos distintos.

## Las cuatro actividades del loop, en profundidad

**Scope** — determina la amplitud del compromiso. Iteraciones sucesivas revelan: sistemas adicionales con variantes de malware coincidentes, IOCs antes desconocidos que aparecen al profundizar el análisis, rutas de movimiento lateral no detectadas al inicio, repositorios de datos accedidos por el atacante.

**Contain** — frena el daño preservando evidencia.
- *Iteraciones tempranas*: aislar sistemas obviamente comprometidos, bloquear IPs maliciosas conocidas, deshabilitar cuentas comprometidas.
- *Iteraciones posteriores*: segmentación de red basada en los patrones de movimiento lateral ya observados, restricciones específicas de aplicación contra las herramientas del atacante, e incluso contención "engañosa" (deceptive containment) que desorienta al atacante mientras el equipo mantiene visibilidad sobre su actividad.

**Eradicate** — elimina la presencia del atacante, y rara vez tiene éxito completo en el primer intento.
- *Erradicación inicial*: remueve artefactos obvios — malware conocido, cuentas maliciosas, mecanismos de persistencia ya identificados.
- *Iteraciones posteriores*: atienden persistencia más sofisticada descubierta con análisis más profundo — monitoreo de comportamiento que revela backdoors ocultos, compromisos de cadena de suministro que requieren coordinación con el proveedor, técnicas *living-off-the-land* con herramientas legítimas.

**Recover** — devuelve los sistemas a la normalidad atendiendo la causa raíz.
- *Recuperación temprana*: restauración desde backup, reseteo de credenciales, parcheo de vulnerabilidades.
- *Iteraciones posteriores*: mejoras sistémicas — monitoreo reforzado para el patrón de ataque específico, cambios de política que atacan la falla de proceso de fondo, modificaciones arquitectónicas que previenen la recurrencia.

## Cinco disparadores que obligan a re-entrar al loop

1. **IOCs nuevos**: el análisis revela indicadores antes desconocidos → se vuelve a Scope. Ejemplo del capítulo: un script PowerShell hallado en el registro de un sistema dispara la búsqueda de modificaciones de registro similares en otros equipos; el análisis de red que revela comunicación con infraestructura C2 adicional dispara *scoping* sobre otros sistemas que se comunican con esos mismos servidores.
2. **Expansión de alcance**: indicadores ya conocidos resultan tener un alcance mayor al entendido inicialmente — no es un IOC nuevo, es reconocer que el compromiso ya identificado llega más lejos. Ejemplo: una cuenta de servicio comprometida, vista primero en una aplicación de marketing, también está activa en sistemas de finanzas con datos regulados — expande el radio del incidente sin que cambie el IOC de base.
3. **Erradicación incompleta**: intentos fallidos de erradicación revelan mecanismos de persistencia más sofisticados. Sistemas que parecían limpios muestran señales de reinfección — persistencia no detectada o acceso del atacante por un vector todavía no identificado.
4. **Revelaciones del análisis de evidencia**: el análisis detallado de la evidencia recolectada descubre frecuentemente algo nuevo — forense de memoria que revela familias de malware adicionales, reconstrucción de línea de tiempo que muestra una fecha de compromiso más temprana, análisis de logs que identifica sistemas afectados antes desconocidos, o ingeniería inversa de malware que expone capacidades ocultas.
5. **Cambios en prioridades de negocio y obligaciones externas**: sistemas críticos nuevos que requieren contención inmediata, requisitos regulatorios que exigen *scoping* adicional, condiciones de la póliza de seguro cibernético que exigen acciones específicas, o pedidos de fuerzas de seguridad/reguladores que postergan la contención o exigen preservación de evidencia.

**El punto central del capítulo**: estos disparadores no son fallas del equipo, son parte esperada del proceso de aprendizaje.

## Cómo decidir cuándo salir del loop

Tres dimensiones de criterio:

- **Indicadores técnicos**: no aparecen IOCs nuevos en el *scoping*, el monitoreo no muestra señales de actividad del atacante, la verificación de erradicación confirma la remoción de la amenaza, los sistemas operan con normalidad tras la recuperación.
- **Indicadores de negocio**: se cumplieron los objetivos operativos, se alcanzó un nivel de riesgo aceptable, el análisis costo-beneficio respalda cerrar la respuesta activa, se consideraron las restricciones de recursos.
- **Requisitos organizacionales**: se cumplen las condiciones regulatorias para el cierre formal, hay sign-off del liderazgo sobre el riesgo residual aceptado, y se balanceó monitoreo continuo contra reanudación operativa.

**Detalle de implementación crítico**: la decisión de salir del loop debe quedar escrita como una decisión positiva y atribuida a alguien, no como un acuerdo implícito. El registro debe nombrar a quien decide, los indicadores técnicos y de negocio que la respaldan, el riesgo residual aceptado, y la fecha y hora exacta. El capítulo observa algo revelador sobre esto: ejecutivos que verbalmente estaban dispuestos a dar por cerrado un incidente a veces reconsideran cuando se les dice que su nombre va a figurar junto a esa decisión en el registro.

## Ejemplos del capítulo

Comparación de dos diagramas — proceso lineal vs. iterativo — donde el enfoque lineal falla en aprender sobre amenazas adicionales en el camino, mientras que el modelo iterativo descubre varias amenazas relacionadas a través de pasadas sucesivas del loop.

Ejemplo de *scoping*: malware identificado en un segmento de red puede aparecer corriendo en hosts de una subsidiaria distinta, adquirida en una fusión reciente — eso dispara otra pasada de *scoping*, a menudo con stakeholders, consideraciones regulatorias y requisitos de contención distintos a los de la respuesta inicial.

Ejemplo regulatorio: reguladores pueden exigir *scoping* adicional para garantizar cumplimiento; nuevos objetivos de negocio pueden obligar a revisar los planes de recuperación ya definidos.

## Documentación requerida en cada paso

- **Scope**: sistemas examinados, indicadores buscados, hallazgos.
- **Contain**: medidas de aislamiento, alternativas consideradas, motivo de la elección.
- **Eradicate**: artefactos removidos, métodos de verificación, dificultades encontradas.
- **Recover**: sistemas restaurados, pasos de validación, mejoras de seguridad implementadas.

**Evaluación de impacto**: funciones de negocio afectadas, cantidad aproximada de usuarios impactados, impacto en ingresos por caída de sistemas, workarounds implementados. El capítulo señala que estos datos de impacto cada vez más alimentan reportes regulatorios posteriores al cierre — nombra explícitamente la **DORA (Digital Operational Resilience Act)**, que exige a organizaciones del sector financiero reportar impacto y costos asociados.

**Comunicación diferenciada por audiencia**: resúmenes ejecutivos para liderazgo (impacto de negocio, reducción de riesgo, recursos necesarios), briefings técnicos para IT/seguridad (detalles de implementación, monitoreo, validación), comunicación a usuarios (disrupciones, workarounds, tiempos estimados).

## Advertencias y límites

- **Fatiga del equipo**: iteraciones múltiples cansan al equipo; hace falta rotación y descanso para sostener efectividad. Las restricciones de presupuesto pueden obligar a priorizar solo las actividades de *scoping* y remediación más críticas.
- **Tensión costo-beneficio**: el costo de un disparador perdido se acumula — los puntos de apoyo del atacante persisten, la evidencia envejece, la confianza de los stakeholders se erosiona cuando los mismos sistemas vuelven a aparecer en hallazgos nuevos. Pero también hay que evitar sobre-iterar: hay que balancear la necesidad de una respuesta exhaustiva contra la realidad de los recursos disponibles, evitando el *burnout*.
- **Por qué fallan los enfoques de una sola pasada**: entendimiento inicial incompleto → remediación parcial que deja puntos de apoyo del atacante intactos; descubrimientos durante la erradicación que revelan sistemas comprometidos adicionales; análisis de evidencia que descubre vectores de ataque o mecanismos de persistencia antes desconocidos.
- **Timing y preservación de evidencia**: reconstruir detalles de impacto *antes* del cierre es sustancialmente más fácil que hacerlo después, cuando la memoria se desdibuja y las ventanas de retención de logs empiezan a vencer.

## Herramientas y tecnologías nombradas

El capítulo evita deliberadamente recomendar herramientas puntuales — habla de categorías y restricciones ("las limitaciones de la herramienta pueden condicionar la velocidad de iteración, en particular cuando el análisis forense o la recolección de evidencia requieren procesos manuales que consumen tiempo"). Se mencionan, sin marca, sistemas de tracking/case management, controles de acceso dentro de sistemas de ticketing existentes, y capacidades forenses (forense de memoria, reconstrucción de línea de tiempo, análisis de logs, ingeniería inversa de malware).

## Relación con otros capítulos

El loop opera dentro del proceso más amplio Prepare → Debrief. Lo que sigue después de salir del loop es Debrief ([12-debrief.md](12-debrief.md)), que recoge las lecciones de cada iteración. Las referencias a DORA, coordinación con fuerzas de seguridad y contacto con reguladores conectan este capítulo con el contexto legal/regulatorio que se retoma en otras partes del libro. Los capítulos dedicados Scope, Contain, Eradicate y Recover desarrollan cada actividad del loop en mucho más detalle operativo.

## Preguntas de estudio

1. De los cinco disparadores de re-entrada al loop, ¿cuál es el que tu organización detecta más tarde hoy, y por qué?
2. Redactá, para un cierre de incidente reciente (real o hipotético), el registro de la decisión de salida del loop con los cuatro elementos que pide el capítulo (quién decide, indicadores de respaldo, riesgo residual aceptado, fecha/hora).
3. ¿Cómo balanceás en la práctica "evitar el burnout del equipo" contra "el costo de un disparador perdido"? Dar un ejemplo concreto de una decisión que tomarías distinto hoy sabiendo esto.

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Response Actions Loop". CC BY 4.0. https://dynamicincidentresponse.com/chapters/responseactionsloop.html
