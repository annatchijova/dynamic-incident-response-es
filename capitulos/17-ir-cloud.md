# Respuesta a incidentes para sistemas cloud

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Incident Response for Cloud Systems", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/considerations-cloud.html

## Tesis

Extiende DAIR (Prepare, Detect, Response Actions, Debrief) con consideraciones específicas de cloud. Los entornos cloud presentan desafíos únicos que difieren de forma significativa de las investigaciones on-premises tradicionales: patrones de ataque, vectores de acceso inicial y mecanismos de persistencia distintos a los de la infraestructura legacy.

## Conceptos clave

**Modelo de responsabilidad compartida**: moldea tanto la preparación como la ejecución de la IR. La organización es responsable de configurar los mecanismos de visibilidad (logging y monitoreo) que el proveedor cloud no activa por defecto. Esto crea un vacío crítico: un log cloud que nunca se habilitó simplemente no existe, y no hay forma de reconstruirlo después del hecho.

**Recursos efímeros**: instancias de cómputo y cargas de trabajo en contenedores que se aprovisionan y destruyen rápidamente — complica la preservación forense y la reconstrucción de línea de tiempo respecto del hardware on-premises, que es estático.

**Plano de gestión vs. plano de datos**:
- **Plano de gestión**: logs de la capa de control, habilitados por defecto en general; registra cambios de identidad y acceso.
- **Plano de datos**: logs de acceso a aplicación y almacenamiento; deshabilitados por defecto, críticos de habilitar de forma selectiva por el trade-off entre costo y volumen.

## Patrones de ataque cloud más comunes

**Vectores de acceso inicial** (según datos de Google Threat Horizons citados en el capítulo, más del 80% de la actividad observada):
1. **Credenciales débiles o ausentes** (47,1%): ingeniería social contra cuentas sin MFA habilita acceso amplio al entorno.
2. **Configuraciones erróneas** (29,4%): brechas de habilidad durante la migración a cloud dejan datos expuestos o privilegios excesivos.
3. **Compromiso de API/UI**: endpoints de aplicación mal asegurados exponen el plano de gestión una vez logrado un punto de apoyo inicial.

**Motivaciones e impactos del atacante** (según el Mandiant M-Trends 2025 Report citado):
- **Robo de datos/extorsión**: observado en casi dos tercios (66%) de los compromisos cloud.
- **Ransomware**: variantes cloud-específicas que borran snapshots, modifican políticas de ciclo de vida, o bloquean administradores manipulando IAM.
- **Cryptomining**: cuentas comprometidas aprovisionan recursos GPU en múltiples regiones, generando ingreso para el atacante e inflando el costo cloud de la víctima.
- **Escalada lateral**: servicios de metadata en workloads comprometidos entregan credenciales que permiten pivotar de cómputo a control del plano de gestión.

El Orca Security 2025 State of Cloud Security Report, también citado, cuantifica exposición de datos: 33% de las organizaciones con buckets de storage expuestos públicamente contenían datos sensibles; 38% de las bases de datos expuestas tenían información sensible; 28% de las funciones cloud accesibles tenían secretos en texto plano embebidos en el código.

## Preparación: estrategia de logging

**Lag time y retención** son variables críticas de planificación. El capítulo cita que los logs de Azure Entra ID se retienen solo 7 días en el tier gratuito y 30 días con licencia premium — insuficiente para investigaciones que descubren el incidente tras un *dwell time* extendido.

**Priorización de logging del plano de datos**: habilitar logging de acceso en sistemas que almacenan datos sensibles o son blancos probables, balanceando visibilidad investigativa contra costo de almacenamiento. Ejemplo del capítulo: tiene sentido pagar el costo de loguear accesos a un bucket de registros confidenciales; puede no justificarse para un bucket de assets de un sitio web público.

**Logging centralizado**: un SIEM o un Log Analytics workspace que consume los logs de la plataforma cloud con retención extendida (resolviendo el límite por defecto de 7-30 días) simplifica la investigación y contempla amenazas de *dwell* prolongado.

## Preparación: arquitectura de permisos

**Línea base de acceso basada en rol**: todo respondedor necesita acceso global de solo lectura que permita revisar logs, enumerar usuarios y examinar recursos — en AWS la policy administrada SecurityAudit, en Azure el rol Security Reader, en Google Cloud el rol Security Reviewer.

**Segregación de infraestructura forense**: cuentas o proyectos forenses dedicados con permisos elevados, para evitar contaminar evidencia y reducir la interferencia del atacante durante el análisis.

**Gestión de acceso de escritura** — tres enfoques que el capítulo compara, para balancear mínimo privilegio contra urgencia de respuesta:
1. **Cuentas de servicio automatizadas**: automatizaciones ya construidas ejecutan acciones de contención en nombre del respondedor, evitando acceso elevado permanente.
2. **Elevación just-in-time**: Azure PIM, AWS IAM Identity Center, o Google Cloud IAM Conditions — activación de rol acotada en el tiempo.
3. **Cuentas break-glass**: credenciales selladas para acceso de emergencia cuando los otros mecanismos fallan; su uso dispara alertas y exige revisión posterior al incidente.

## Detección: herramientas cloud-native

**AWS GuardDuty**: servicio gestionado de detección de amenazas que monitorea cuentas y workloads con ML, detección de anomalías e inteligencia de amenazas. Capacidades clave: escaneo de malware sin agente (GuardDuty Malware Protection crea snapshots EBS para escanear sin afectar el workload corriendo); preservación automática de evidencia (el snapshot EBS se retiene cuando se detecta malware); escaneo bajo demanda, especificando ARNs de instancias EC2 para hosts que todavía no dispararon un hallazgo automático.

**Azure Microsoft Defender for Cloud**: monitorea recursos y logs de auditoría de Microsoft 365/Azure buscando actividad sospechosa, generando alertas de seguridad con detalle del recurso afectado y entidades relacionadas para escalar.

## Acciones de respuesta — procedimientos específicos de cloud

**Scoping del compromiso**: examinar los roles/políticas IAM adjuntos a la identidad comprometida; consultar los logs de auditoría del plano de gestión para ver todas las acciones de esa identidad; identificar recursos modificados, accedidos o creados durante la ventana de compromiso; cruzar con logs del plano de datos para evaluar exposición de datos.

**Aislamiento de recursos**: modificar reglas de security group para restringir egress, deshabilitar asociaciones de IP pública, implementar ACLs de red, revocar credenciales temporales de sesiones assume-role.

**Erradicación de persistencia**: los mecanismos típicos que usa el atacante son crear usuarios IAM adicionales con acceso de consola/programático, agregar claves SSH a instancias de cómputo, modificar roles de ejecución de Lambda, y desplegar imágenes de contenedor con backdoor en el registro. La remediación exige revocación sistemática de credenciales, remoción de permisos y borrado de artefactos a través de todos los cambios del plano de gestión.

## Debrief con preguntas cloud-específicas

El capítulo propone preguntas de debrief propias del contexto cloud: ¿qué vacíos de logging dificultaron la investigación? ¿qué debilidad de configuración habilitó el acceso inicial? ¿cuánto demoró la detección? ¿la contención fue efectiva o había una alternativa mejor? ¿hubo pivote hacia el plano de gestión, y se podría haber evitado?

## Herramientas y tecnologías nombradas

Amazon GuardDuty · Azure Microsoft Defender for Cloud · Azure Entra ID · Azure PIM · AWS IAM Identity Center · Google Cloud IAM Conditions · SIEM/Log Analytics workspace · snapshots EBS.

## Advertencias y límites

- **El riesgo crítico es la ausencia de logging**: a diferencia de on-premises, donde el log puede existir sin recolectar, un log cloud nunca habilitado no se puede reconstruir — una asimetría que genera ceguera investigativa irreversible.
- **Trade-off costo/visibilidad**: no es viable loguear todo en todos los recursos; habilitarlo selectivamente en activos de alto valor es un compromiso necesario que deja vacíos potenciales en sistemas de menor prioridad.
- **Vacíos de retención**: los períodos por defecto (7-30 días) no alcanzan para incidentes con *dwell time* de semanas o meses; conseguir retención adecuada exige comprar features premium o implementar almacenamiento externo.
- **Velocidad de aprovisionamiento de acceso**: balancear mínimo privilegio contra velocidad de respuesta genera tensión operativa real — el acceso elevado permanente viola principios de seguridad, pero pedirlo durante un incidente activo introduce demoras que benefician al atacante. La organización tiene que pre-armar la solución, no improvisarla en medio de la crisis.

## Relación con otros capítulos

El capítulo remite explícitamente a la Parte 2 (el modelo DAIR completo) para la guía detallada de cada actividad de respuesta, usando este capítulo solo para sumar contexto cloud-específico sobre ese material base.

## Preguntas de estudio

1. Revisá hoy mismo la retención de logs de tu identidad cloud principal (Entra ID, IAM, etc.) — ¿alcanza para un *dwell time* de varias semanas?
2. ¿Tu organización usa elevación just-in-time o cuentas break-glass para acceso de escritura durante un incidente, o se improvisa en el momento?
3. Tomá el ejemplo de escalada lateral vía metadata de workload — ¿tu entorno tiene ese vector cerrado hoy?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Incident Response for Cloud Systems". CC BY 4.0. https://dynamicincidentresponse.com/chapters/considerations-cloud.html
