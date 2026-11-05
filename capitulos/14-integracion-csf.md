# Integrando DAIR con NIST CSF 2.0

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Integrating DAIR with NIST CSF 2.0", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/integration.html

## Tesis

Cumplimiento y efectividad operativa no son objetivos mutuamente excluyentes. Una organización puede satisfacer requisitos de auditoría *y* lograr resultados reales de respuesta a incidentes a la vez, alineando DAIR con NIST CSF 2.0. La idea de fondo: las prácticas tácticas de DAIR generan artefactos de cumplimiento de forma natural, sin necesidad de un proceso administrativo paralelo.

## Las seis funciones de CSF 2.0 (repaso)

- **Govern (GV)**: estrategia de gestión de riesgo, expectativas y política comunicadas y monitoreadas.
- **Identify (ID)**: comprensión de activos, vulnerabilidades, amenazas e impactos potenciales de negocio.
- **Protect (PR)**: salvaguardas que gestionan el riesgo antes de que ocurra un incidente.
- **Detect (DE)**: hallazgo y análisis de ataques y compromisos.
- **Respond (RS)**: acciones tomadas en respuesta a incidentes detectados, incluyendo actividad iterativa que se adapta a información nueva.
- **Recover (RC)**: restauración de activos y operaciones afectadas, más las actividades posteriores que capturan lecciones e implementan mejoras preventivas.

## Mapa DAIR → CSF 2.0 (reconstrucción propia a partir de la Tabla del capítulo)

| Waypoint DAIR | Función(es) CSF | Actividades clave | Artefactos de cumplimiento típicos |
|---|---|---|---|
| Prepare | Protect (PR) | Documentar procedimientos de respuesta, desarrollar playbooks, desplegar detección, configurar preparación forense, entrenar personal | Planes de IR, playbooks, listas de contacto, registros de entrenamiento |
| Detect / Verify / Triage | Detect (DE) | Monitoreo de alertas, verificación de eventos, priorización basada en riesgo | Logs de alerta, decisiones de triage, registros de falsos positivos, documentación de declaración del incidente |
| Response Actions Loop | Respond (RS) | Ciclo iterativo Scope→Contain→Eradicate→Recover, adaptándose a hallazgos nuevos | Análisis de scoping, decisiones de contención, registros de erradicación, verificación de recuperación (acumulados a través de iteraciones) |
| Recover | Recover (RC) | Restauración de sistemas, validación operativa, implementación de mejoras | Registros de finalización de restauración, documentación de validación |
| Debrief | Recover (RC) | Análisis de causa raíz, captura de lecciones aprendidas, recomendaciones de mejora, seguimiento de implementación | Reportes de debrief, documentos de RCA, registros de seguimiento de mejoras |
| Coordinación con decision-makers | Govern (GV) / Identify (ID) | Consulta continua con stakeholders, evaluación de impacto de negocio, guía alineada a riesgo durante toda la respuesta | Registros de consulta a stakeholders, decisiones de clasificación de riesgo, documentación de autorización |

## Conceptos clave adicionales

**Coordinación continua con decision-makers**: no ocurre solo al declarar o cerrar el incidente — es guía constante sobre expansión de alcance, enfoques de contención, impacto operativo aceptable y prioridades de recuperación. Esto genera registros que mapean directamente a las categorías de Govern relacionadas con aceptación de riesgo y alineación organizacional.

**La iteración como artefacto de cumplimiento, no como falla**: los modelos tradicionales tratan volver a una fase anterior como un fracaso; DAIR la reencuadra como comportamiento esperado y apropiado. Si se documenta qué información nueva disparó cada ciclo y qué remediación resultó, la iteración deja de leerse como debilidad y pasa a ser evidencia de una respuesta exhaustiva, adaptativa y bien pensada.

## Ejemplo del capítulo: Govern a través de DAIR (Tabla 3 del original, reconstruida)

- **Contexto organizacional (GV.OC)**: durante Prepare, crear el mapeo de notificación regulatoria y los criterios de clasificación de riesgo; durante Verify/Triage de cada incidente, documentar la decisión de clasificación contra esos umbrales ya acordados. Resultado: registros de decisión de triage que muestran el razonamiento de clasificación.
- **Estrategia de gestión de riesgo (GV.RM)**: al salir del Response Actions Loop, obtener aceptación formal de riesgo; durante Debrief, mapear lecciones aprendidas al registro de riesgo empresarial. Un auditor recibe el registro firmado de aceptación de riesgo al salir del loop y los datos de tendencia de métricas enviados a la función de riesgo empresarial.
- **Roles, responsabilidades y autoridades (GV.RR)**: desarrollar la matriz de autoridad del incidente y los umbrales de escalamiento durante Prepare, con roles nombrados (no títulos genéricos), mantenida como documentación formal revisada antes de que ocurra un incidente.
- **Gestión de riesgo de cadena de suministro (GV.SC)**: mapear obligaciones de terceros y requisitos de notificación durante Prepare; durante Contain, incluir procedimientos de revocación de acceso a terceros; después de Debrief, trackear remediación relacionada con proveedores.

## Ejemplo de iteración como evidencia de Respond

Un Scope inicial identifica una sola cuenta de usuario comprometida. Contain aísla esa cuenta; Eradicate remueve el acceso del atacante. Pero la validación en Recover descubre tareas programadas sospechosas en un sistema secundario. En vez de cerrar el incidente, eso dispara una segunda iteración del Response Actions Loop: un nuevo Scope descubre movimiento lateral, Contain aísla sistemas adicionales, Eradicate remueve persistencia en el alcance ampliado. La documentación de ambas iteraciones demuestra capacidad de respuesta adaptativa y un esfuerzo de remediación integral — exactamente el tipo de evidencia que un auditor de CSF 2.0 busca.

## Preparación para auditoría (recomendaciones del capítulo)

1. Organizar la documentación de incidentes por alineación con función CSF, no cronológicamente.
2. Cruzar referencias entre actividades DAIR y terminología CSF en planes y procedimientos de respuesta.
3. Entrenar al personal para explicar conceptos DAIR usando vocabulario de CSF 2.0.
4. Mantener formatos estandarizados de reporte de incidente (reportes, líneas de tiempo, resúmenes de lecciones aprendidas).

## Configuración del sistema de tracking de incidentes

- **Diseño de campos de estado**: reflejar terminología CSF/DAIR ("Detección completa", "Verificación pendiente", "Contención activa", "Erradicación en progreso", "Recuperación en curso") — genera registros que demuestran cobertura de función.
- **Vinculación de evidencia**: campos del sistema que enlazan documentos de análisis de scoping, decisiones de contención, registros de erradicación y verificación de recuperación a un incidente específico.
- **Documentación de decisión**: campos que capturan qué decision-makers fueron consultados, qué guía dieron, y cómo su input influyó en la respuesta — satisface directamente los requisitos de Govern.
- **Plantillas de comunicación**: específicas por audiencia (ejecutiva vs. técnica), ambas documentando la información apropiada para su respectiva audiencia.

## Advertencias y límites

- **La iteración solo demuestra exhaustividad si está documentada**: un ciclo no documentado puede leerse como confusión operativa en vez de respuesta adaptativa — hay que registrar qué información disparó cada ciclo y qué remediación resultó.
- **Supone documentación ya existente**: el capítulo asume que la organización ya mantiene documentación exhaustiva durante las actividades DAIR. "La mayoría de los artefactos de cumplimiento ya existen" — pero solo para quien documenta el razonamiento junto con la acción, no solo la acción.
- **Timing de la evaluación de madurez**: la integración asume que la evaluación de capacidad ocurre después de que la organización ya manejó varios incidentes — un programa recién formado, con poco historial, puede tener dificultad para mostrar datos de tendencia o implementación de lecciones de debriefs previos.
- **Dependencias de terceros**: el cumplimiento de GV.SC exige haber mapeado obligaciones de terceros y requisitos contractuales de notificación *antes* de que ocurra un incidente, durante Prepare — intentar determinarlos durante un incidente activo genera riesgo de incumplimiento.

## Relación con otros capítulos

Retoma directamente la matriz de autoridad y el plan de comunicación de emergencia desarrollados en Prepare ([05-prepare.md](05-prepare.md)). Se apoya en NIST SP 800-61 Rev. 3 como el estándar fundacional que reencuadra la IR como componente de gestión integral de riesgo — ya presentado y criticado en [03-modelos-existentes.md](03-modelos-existentes.md). El capítulo señala que CSF 2.0 refleja prácticas ya consolidadas de respuesta a incidentes, y que DAIR simplemente las formaliza — de ahí la alineación natural entre ambos.

## Preguntas de estudio

1. Tomá un incidente reciente de tu organización y mapealo contra la tabla DAIR→CSF. ¿Qué artefactos de cumplimiento ya tenés, y cuáles te faltan por completo?
2. ¿Tu sistema de tracking de incidentes usa terminología CSF/DAIR en sus campos de estado, o terminología ad-hoc que un auditor externo no reconocería?
3. ¿Tu organización mapeó las obligaciones de notificación de terceros (GV.SC) *antes* de que ocurra un incidente, o lo descubrís recién cuando pasa algo?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Integrating DAIR with NIST CSF 2.0". CC BY 4.0. https://dynamicincidentresponse.com/chapters/integration.html
