# Scope

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Scope Activity", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/scope.html — ver también el anexo oficial [step-by-step-scope.md](../anexos/step-by-step-scope.md).

## Propósito

El puente entre Verify/Triage y el ciclo Contain-Eradicate-Recover: pasar de "tenemos un incidente" a "conocemos la amplitud y profundidad real de este incidente". Sin un *scoping* adecuado, la organización corre el riesgo de atender solo los síntomas visibles mientras gran parte del ataque queda sin detectar — el libro usa como advertencia un caso ("NovaFlow") donde procesos sospechosos hallados en un sistema nunca se buscaron en el resto de la organización.

## Conceptos clave

**IOCs técnicos**: artefactos concretos y buscables — hashes de archivo, direcciones/dominios de red, nombres de proceso, modificaciones de registro, anomalías de cuenta.

**IOCs de comportamiento**: indicadores basados en patrón — sincronización temporal entre sistemas, flujos de datos inusuales, patrones de autenticación propios de movimiento lateral.

**Reconstrucción de línea de tiempo**: identificar al "paciente cero" (el compromiso inicial), las rutas de movimiento lateral, la secuencia de despliegue de mecanismos de persistencia, y la cronología de acceso a datos.

## Metodologías de scoping

**Hunting a nivel empresa**: analistas usan herramientas centralizadas — SIEM, sistemas de agregación de logs, plataformas EDR — para buscar IOCs coincidentes en todo el entorno. Las plataformas de *threat hunting* que integran datos de endpoint, red y logging dan la visión más amplia posible de indicadores de compromiso potenciales.

**Scoping progresivo (por fases)**:
1. **Priorización de activos críticos**: domain controllers, file servers, bases de datos.
2. **Expansión lateral**: sistemas conectados directamente a los hosts ya comprometidos.
3. **Barrido ambiental**: el resto de los sistemas de la organización.

## Procedimientos y técnicas

**Análisis de línea de tiempo** (ejemplo del capítulo): un set de datos de actividad de red con nueve eventos de movimiento lateral entre IPs internas en dos horas, usando identificadores de C2 del atacante graficados cronológicamente para revelar el patrón de progresión.

**Contra-estrategias anti-forenses**: el capítulo advierte que los atacantes borran o modifican logs. El respondedor debe identificar vacíos en los timestamps de log, tamaños de archivo de log inusuales, o eventos de seguridad que indiquen borrado de logs.

## Herramientas y tecnologías nombradas

SIEM y sistemas de agregación de logs · plataformas EDR · herramientas de inventario y escaneo activo · scripts de evaluación de compromiso a medida (PowerShell/shell) · específicas de OT: **Dragos**, **Malcolm** (Idaho National Laboratory), **Zeek** con **ICSNPP** (ICS Network Protocol Parsers) · específicas de cloud: APIs del proveedor cloud, herramientas de seguridad de runtime de contenedores, servicios de logging cloud-native.

## Límites y advertencias críticas

**Vacíos de visibilidad** que dificultan el scoping:
- Sistemas no gestionados (BYOD, shadow IT, sistemas legacy) fuera del inventario de activos.
- Logging limitado en plataformas legacy/ICS — el capítulo menciona específicamente que el **Siemens S7-1200** carece de capacidades de logging centralizado.
- El muestreo de flujo de red (frecuentemente en proporciones de 1:1000) puede perderse conexiones de corta duración o *beaconing* de C2 de bajo volumen.
- Entornos cloud/serverless pueden quedar invisibles para herramientas tradicionales de endpoint.
- La evidencia en recursos cloud efímeros desaparece al desasignarse el recurso.

**Técnicas anti-forenses**: borrado/modificación de logs que crea vacíos en la línea de tiempo; el atacante oculta su presencia manipulando el sistema.

**Advertencia procedimental puntual**: verificar la tasa de muestreo configurada en los dispositivos de captura de flujo de red, y pedir exportación sin muestreo en las rutas de tráfico de mayor valor — el muestreo de paquetes por defecto puede socavar por completo la efectividad del scoping frente a un atacante sofisticado.

## Relación con otros capítulos

DAIR ubica Scope entre Verify/Triage y el ciclo Contain-Eradicate-Recover — refleja su rol como paso obligado antes de una contención dirigida: sin entender la amplitud del ataque, cualquier esfuerzo de respuesta queda incompleto. Cada pasada por el Response Actions Loop ([08-response-actions-loop.md](08-response-actions-loop.md)) saca a la luz artefactos nuevos que extienden la línea de tiempo hacia atrás o revelan actividad adicional del atacante — por eso scoping es iterativo, nunca un evento único.

## Preguntas de estudio

1. ¿Tu entorno tiene sistemas fuera del inventario de activos (BYOD, shadow IT, legacy)? ¿Cómo los incorporarías a un scoping de incidente real hoy?
2. Verificá (o pedí verificar) la tasa de muestreo de tus dispositivos de captura de flujo de red. ¿Qué tan ciego te deja ese muestreo frente a un *beaconing* de bajo volumen?
3. Dado el caso NovaFlow (procesos sospechosos nunca buscados en el resto de la organización), ¿qué paso concreto de scoping progresivo lo hubiera evitado?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Scope Activity". CC BY 4.0. https://dynamicincidentresponse.com/chapters/scope.html
