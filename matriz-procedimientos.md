# Matriz de procedimientos operativos

Procedimientos operativos descriptos en cada actividad DAIR, con su capítulo fuente. Síntesis propia — no sustituye el checklist oficial en [anexos/](anexos/).

| Actividad | Procedimiento | Condición / disparador | Capítulo |
|---|---|---|---|
| Prepare | Desarrollar políticas (ransom, legales, divulgación) en colaboración con stakeholders | Antes de cualquier incidente | [05](capitulos/05-prepare.md) |
| Prepare | Definir niveles de autorización de contención (1/2/3) | Para evitar parálisis de escalamiento | [05](capitulos/05-prepare.md) |
| Prepare | Clasificar riesgo con matriz o árbol de decisión | Al diseñar el programa de IR | [05](capitulos/05-prepare.md) |
| Detect | Aplicar detección híbrida (firma + comportamiento + ML) | Siempre, para cubrir amenazas conocidas y nuevas | [06](capitulos/06-detect.md) |
| Detect | Escalar en la Pyramid of Pain hacia indicadores de comportamiento | Cuando el *hunting* enfrenta "tiranía de elección infinita" | [06](capitulos/06-detect.md) |
| Detect | Acotar líneas base por unidad de negocio | En organizaciones grandes con perfiles de actividad heterogéneos | [06](capitulos/06-detect.md) |
| Verify/Triage | Clasificar el EOI en continuar/detener/diferir | Tras recibir un EOI | [07](capitulos/07-verify-triage.md) |
| Verify/Triage | Enriquecer EOIs con CTI (VirusTotal, OTX, Shodan) | Durante la verificación | [07](capitulos/07-verify-triage.md) |
| Verify/Triage | Documentar de forma continua, separada de otras notas | Desde el inicio del caso | [07](capitulos/07-verify-triage.md) |
| Response Actions Loop | Repetir Scope→Contain→Eradicate→Recover | Ante cualquiera de los 5 disparadores de re-entrada | [08](capitulos/08-response-actions-loop.md) |
| Response Actions Loop | Registrar por escrito la decisión de salida del loop | Al cerrar la respuesta activa | [08](capitulos/08-response-actions-loop.md) |
| Scope | Hunting enterprise-wide con SIEM/EDR por IOC | Tras verificar el incidente | [09](capitulos/09-scope.md) |
| Scope | Scoping progresivo (crítico → lateral → ambiental) | Para priorizar recursos limitados | [09](capitulos/09-scope.md) |
| Scope | Verificar tasa de muestreo de flujo de red | Antes de confiar en el resultado del scoping de red | [09](capitulos/09-scope.md) |
| Contain | Preferir aislamiento EDR sobre controles de red puros | Al aislar un sistema comprometido | [10](capitulos/10-contain.md) |
| Contain | Reenviar logs a ubicación centralizada de inmediato | Apenas se descubre el compromiso | [10](capitulos/10-contain.md) |
| Contain | Decidir terminar vs. monitorear con criterios pre-acordados | Antes del incidente, no durante | [10](capitulos/10-contain.md) |
| Eradicate | Correr investigación corta y larga en paralelo | Durante toda la erradicación | [11](capitulos/11-eradicate.md) |
| Eradicate | Responder las 5 preguntas críticas (vector, credenciales, sistemas, persistencia, vulnerabilidad) | Antes de dar por cerrada la erradicación | [11](capitulos/11-eradicate.md) |
| Recover | Completar el checklist de 9 pasos pre-restauración | Antes de activar cualquier sistema | [12](capitulos/12-recover.md) |
| Recover | Escanear IOCs en último lugar, tras el hardening completo | Como último paso del checklist | [12](capitulos/12-recover.md) |
| Recover | Obtener sign-off documentado del dueño del sistema | Antes de devolver el sistema a producción | [12](capitulos/12-recover.md) |
| Debrief | Decidir retención/baja de activos temporales (evidencia, cuentas, monitoreo) | Al cerrar el incidente | [13](capitulos/13-debrief.md) |
| Debrief | Consolidar documentación dispersa en un registro único | Mientras el recuerdo de los respondedores está fresco | [13](capitulos/13-debrief.md) |
| Debrief | Correr AAR y mapear lecciones al registro de riesgo | Tras el cierre, aprovechando la ventana de atención post-crisis | [13](capitulos/13-debrief.md) |
| Cloud | Habilitar logging del plano de datos en activos de alto valor | En preparación, antes del incidente | [17](capitulos/17-ir-cloud.md) |
| Cloud | Usar elevación just-in-time o break-glass para acceso de escritura | Durante contención/erradicación en cloud | [17](capitulos/17-ir-cloud.md) |
| OT | Verificar y hacer triage con ingeniería antes de contener | Siempre, en cualquier evento OT | [18](capitulos/18-ir-ot.md) |
| OT | Coordinar contención con downtime planificado | Cuando la acción requiere parar el proceso físico | [18](capitulos/18-ir-ot.md) |
| Ransomware | Negociar solo tras determinar sensibilidad de datos y exposición regulatoria | Si se considera pagar | [16](capitulos/16-ir-ransomware.md) |
| Ransomware | Validar clave de descifrado antes de restauración completa | Tras un pago o entrega de clave | [16](capitulos/16-ir-ransomware.md) |

## Ver también

[Matriz de decisiones y condiciones](matriz-decisiones.md) para las bifurcaciones de criterio (no procedimiento mecánico) que cada actividad exige.
