# Debrief

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Debrief Activity", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/debrief.html — ver también el anexo oficial [step-by-step-debrief.md](../anexos/step-by-step-debrief.md).

## Propósito

El cierre formal de la respuesta activa, y al mismo tiempo el disparador del aprendizaje organizacional. Debrief marca la conclusión del incidente activo y hace la transición hacia el aprendizaje post-incidente — transforma la experiencia vivida en mejoras duraderas, con reflexión crítica tanto sobre el método del atacante como sobre las fallas propias de la organización en la respuesta.

## Conceptos clave

- **Cierre del incidente**: finalización formal de las operaciones de respuesta — exige evaluar qué hacer con los activos temporales (sistemas aislados, imágenes forenses, cuentas temporales, monitoreo reforzado), consolidar documentación dispersa, y capturar métricas de la respuesta.
- **Activos temporales**: recursos creados durante la respuesta que requieren una decisión explícita de retención, modificación o baja.
- **After-Action Review (AAR)**: reflexión estructurada sobre qué pasó, qué se aprendió, y cómo mejorar la próxima respuesta.

## Cuándo pasar de respuesta activa a debrief (dos condiciones)

1. **Rendimiento decreciente**: el Response Actions Loop deja de producir información nueva sobre presencia o persistencia del atacante.
2. **Determinación del liderazgo**: los decision-makers evalúan que la recuperación de negocio es suficiente, aunque queden consideraciones técnicas residuales.

Determinar ese momento de transición requiere criterio tanto del equipo de respuesta como de los decision-makers organizacionales — no es automático.

## Gestión de activos temporales (procedimientos)

**Evidencia forense**: revisar todos los artefactos recolectados (capturas de red, imágenes de disco, volcados de memoria, archivos de log); consultar a legales sobre requisitos de retención según riesgo de litigio, obligaciones regulatorias e involucramiento de fuerzas de seguridad; balancear el costo de almacenamiento contra la utilidad investigativa futura; documentar explícitamente la decisión de retención.

**Cuentas y accesos temporales**: identificar todas las cuentas temporales creadas durante la respuesta usando la documentación del incidente; revocarlas o borrarlas salvo que haya una razón operativa de peso para mantenerlas; si una cuenta tiene valor continuo, integrarla a los procesos estándar de gestión de accesos; documentar quién la removió y cuándo.

**Monitoreo reforzado**: evaluar su retención según cuatro factores — ¿cubre un vacío de visibilidad identificado durante el incidente? ¿genera alertas excesivas o sobrecarga de performance? ¿la organización puede sostener su mantenimiento? ¿encaja en la estrategia de monitoreo/detección más amplia? Documentar la razón de la retención, qué se modifica para uso permanente, y quién queda a cargo del mantenimiento.

## Consolidación de documentación

El equipo consolida documentación dispersa (sistemas de ticketing, canales de chat, documentos compartidos, notas individuales) en un registro oficial del incidente:

1. Validar la línea de tiempo del incidente con los respondedores clave mientras el recuerdo todavía está fresco.
2. Llenar los vacíos de documentación e inconsistencias detectadas en la revisión.
3. Crear un registro integral que funcione como memoria institucional para futura respuesta y *threat hunting*.

Principio reiterado: construir la documentación de forma continua durante toda la respuesta, no postergarla hasta el debrief — el mismo principio ya visto en Verify and Triage ([07-verify-triage.md](07-verify-triage.md)).

## Captura de métricas

El debrief captura datos cuantitativos que sirven de línea base para el *after-action review* y para mejoras futuras de la respuesta.

## Estrategias de debrief: cierre primero, aprendizaje después

Primero las actividades de cierre (transición desde la respuesta activa, gestión de activos temporales, consolidación de documentación, captura de métricas). Recién después las estrategias de aprendizaje organizacional: realizar AARs estructurados, impulsar mejora organizacional abogando por recursos, desarrollar reportes de incidente integrales, presentar hallazgos a stakeholders.

## Contexto estratégico: la ventana de oportunidad post-incidente

El período inmediatamente posterior a un incidente ofrece una ventana única para impulsar mejoras de seguridad — stakeholders que normalmente resisten inversión en seguridad se vuelven más receptivos frente a evidencia tangible de compromiso. El capítulo cita a Winston Churchill ("never let a good crisis go to waste") para enmarcar la idea de convertir la conciencia de crisis en cambio organizacional duradero antes de que la atención se mueva a otra prioridad.

## El riesgo de no aprender

Un equipo de respuesta que no aprende de sus incidentes queda progresivamente más atrás de adversarios que tratan cada operación como una oportunidad de aprendizaje — los atacantes refinan sus tácticas en base a su propio éxito operativo, y si el defensor no hace lo mismo, la brecha se ensancha con cada incidente.

## Herramientas y tecnologías mencionadas

Sistemas de ticketing · canales de chat · documentos compartidos · planillas tipo Excel para trackear eventos del incidente con timestamps y descripciones (mostrado como figura en el original).

## Advertencias y límites

- **Costo de almacenamiento**: hay que sopesar el costo continuo de guardar evidencia forense contra su utilidad futura potencial.
- **Carga de mantenimiento**: el monitoreo reforzado puede imponer sobrecarga de performance o generar alertas excesivas que afectan negativamente a los equipos de operaciones.
- **Riesgo de superficie de ataque**: retener cuentas temporales aumenta la superficie de ataque y puede introducir riesgo adicional.
- **Dispersión de la información**: la información crítica del incidente existe inicialmente repartida en múltiples lugares — consolidarla exige un esfuerzo deliberado, no espontáneo.

## Relación con otros capítulos

Debrief ocurre cuando el Response Actions Loop ([08-response-actions-loop.md](08-response-actions-loop.md)) deja de producir información nueva sobre la amenaza. Las decisiones de retención de evidencia conectan con procesos legales y cumplimiento regulatorio. Es también el capítulo que más se conecta con "Integrating DAIR with NIST CSF 2.0" ([14-integracion-csf.md](14-integracion-csf.md)), porque los reportes de debrief son uno de los artefactos de cumplimiento que ese capítulo documenta.

## Preguntas de estudio

1. En el último incidente (real o simulado) de tu organización, ¿cuánto tiempo pasó entre el cierre de la respuesta activa y la realización del AAR? ¿Qué se perdió en ese lapso?
2. Armá tu propio checklist de gestión de activos temporales (evidencia, cuentas, monitoreo) para el próximo incidente que cierres.
3. ¿Cómo aprovecharías vos la "ventana post-incidente" para conseguir un recurso o presupuesto que antes te negaban?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Debrief Activity". CC BY 4.0. https://dynamicincidentresponse.com/chapters/debrief.html
