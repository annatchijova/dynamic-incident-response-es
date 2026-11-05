# Acelerando la respuesta a incidentes con IA

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Accelerating Incident Response with AI", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/considerations-ai.html

## Tesis

El capítulo se enfoca en aplicaciones prácticas e inmediatas de IA generativa en IR, no en posibilidades teóricas. La IA reduce de forma significativa el MTTR cuando la aplica un analista con criterio, pero trae riesgos serios de alucinación, exposición de datos e imprecisión que exigen mitigación activa.

## Conceptos clave

- **Alucinaciones**: el modelo genera información incorrecta con total confianza — el riesgo es particular cuando el hallazgo se acepta sin verificar.
- **Shadow AI**: pegar datos sensibles del incidente en cualquier servicio de IA a mano, lo cual puede convertir un incidente ya contenido en un evento de divulgación de datos.
- **Salida no determinística**: el mismo prompt produce resultados distintos en consultas distintas, lo cual complica la validación.
- **Fecha de corte de entrenamiento**: el modelo no tiene inteligencia de amenazas actualizada y puede referenciar técnicas ya obsoletas — el analista tiene que reconocer esto activamente.
- **Sanitización de datos**: reemplazar IPs reales por rangos de documentación RFC 5737 (p. ej. 192.0.2.0/24), sustituir dominios de ejemplo, y redactar PII antes de compartir con una plataforma de IA comercial. El capítulo aclara que esto reduce pero no elimina el riesgo de exposición.

## Técnicas de prompting rápido

- **Prompting iterativo**: empezar amplio y refinar el foco progresivamente.
- **Delimitadores**: comillas triples o tags estilo XML para separar instrucciones de datos.
- **Pedido de salida estructurada**: especificar arrays JSON o tablas con claves definidas.
- **Asignación de rol**: establecer una persona analista para enmarcar la profundidad técnica esperada.
- **Razonamiento *chain-of-thought***: pedir análisis paso a paso antes de la conclusión.
- **Recolección de información**: preguntarle al modelo qué datos fortalecerían su propio análisis.

## Prompts estructurados para tareas complejas

Elementos recomendados: sección de rol y objetivo, instrucciones y restricciones explícitas, pasos de razonamiento que invoquen resolución sistemática, definición del formato de salida, ejemplos del resultado deseado (*one-shot*/*few-shot*), sección de contexto, y un resumen final que reitere las restricciones clave. El capítulo recomienda tratar los prompts ya refinados como herramientas reutilizables, versionadas en Git.

## Opciones de despliegue

- **Modelos comerciales de frontera** (OpenAI, Anthropic, Google, Microsoft): mejor desempeño en análisis de código, interpretación de logs y razonamiento complejo; los datos salen hacia un proveedor externo — los acuerdos empresariales suelen incluir cláusulas de no entrenamiento, pero el prompt puede igual retenerse para QA o prevención de abuso. Apto para aprender con datos no sensibles; para incidentes reales hace falta un acuerdo organizacional de manejo de datos previo.
- **Modelos de pesos abiertos, hosteados en la nube**: desempeño moderado y mejorando rápido; los datos quedan dentro de la infraestructura cloud de la organización, evitando al proveedor de IA de terceros; balancea privacidad contra menor carga de gestión de infraestructura.
- **Modelos de pesos abiertos, locales**: todos los datos quedan en infraestructura propia; alta complejidad de puesta en marcha (hardware con GPU, mantenimiento continuo); desempeño moderado pero mejorando rápido; la mejor opción para entornos muy regulados.

## Ejemplos del capítulo

**Análisis y desofuscación de código**: el capítulo muestra cómo un modelo, con un prompt estructurado, identifica una tarea programada de Windows que ejecuta PowerShell oculto como mecanismo de persistencia/movimiento lateral (disparado por eventos de login fallido) — análisis que a mano llevaría horas.

**Extracción de IOCs**: un prompt estructurado para extraer indicadores de compromiso de un reporte de amenazas, pidiendo hashes de archivo, dominios, familias de malware e identificadores de actor de amenaza en formato tabla.

## Herramientas y tecnologías nombradas

OpenAI, Anthropic, Google, Microsoft (proveedores comerciales de frontera) · DeepSeek, Llama (Meta), Phi (Microsoft) como modelos de pesos abiertos aptos para despliegue local · RFC 5737 (rangos de documentación) y RFC 1918 (rangos IP privados) para sanitización · Git para versionar librerías de prompts · Model Context Protocol (MCP), mencionado para casos de uso avanzados de integración de workflow.

## Advertencias y límites

- Las alucinaciones generan falsedades con total confianza — especialmente problemático cuando la salida de la IA evita la verificación humana.
- Exposición de datos: incluso con cláusulas de no entrenamiento, el prompt puede quedar guardado para QA/logging en la plataforma comercial.
- La no determinación impide verificar de forma independiente un mismo hallazgo.
- Una fecha de corte de entrenamiento vieja puede volver obsoleta una recomendación sin que el analista lo note.
- Algunas organizaciones prohíben la IA directamente; otras exigen gobernanza de política antes de implementarla.
- Los marcos de cumplimiento regulatorio pueden entrar en conflicto con los requisitos de una plataforma de IA comercial.
- Ataques de deanonimización pueden reidentificar datos sanitizados por correlación — el capítulo cita como ejemplo el caso del Netflix Prize.
- La velocidad no garantiza precisión: la validación humana sigue siendo esencial.

## Relación con otros capítulos

El capítulo remite a secciones posteriores propias (fundamentos de prompting, casos de uso fundacionales/intermedios/avanzados, consideraciones operativas) que no se desarrollan en esta síntesis por estar fuera del cuerpo central de DAIR; la progresión va de lo simple a integración de infraestructura sofisticada, manteniendo siempre los mismos principios de fondo: comunicación clara, verificación, y uso apropiado.

## Preguntas de estudio

1. ¿Tu organización tiene una política de "Shadow AI" explícita, o depende del criterio individual de cada analista?
2. Tomá un prompt que usarías para analizar un IOC real y aplicale los delimitadores y la estructura que describe el capítulo. ¿Cambia la calidad de la respuesta?
3. ¿Qué pasaría si sanitizás mal un dato (dejás una IP real en vez de reemplazarla por el rango RFC 5737) antes de pegarlo en un modelo comercial? ¿Qué proceso de revisión lo detectaría?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Accelerating Incident Response with AI". CC BY 4.0. https://dynamicincidentresponse.com/chapters/considerations-ai.html
