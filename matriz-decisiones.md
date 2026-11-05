# Matriz de decisiones y condiciones

Bifurcaciones de criterio que DAIR exige explícitamente — no procedimientos mecánicos, sino puntos donde un humano (analista o decision-maker) tiene que decidir con información incompleta.

| Decisión | Opciones | Condición que inclina la balanza | Quién decide | Capítulo |
|---|---|---|---|---|
| Resultado de la verificación | Continuar / Detener / Diferir | Evidencia suficiente vs. insuficiente vs. ambigua | Analista + decision-maker | [07](capitulos/07-verify-triage.md) |
| Nivel de autorización de contención | Tier 1 (SOC) / Tier 2 (service owner) / Tier 3 (ejecutivo) | Impacto de la acción, no antigüedad del respondedor | Predefinido en Prepare | [05](capitulos/05-prepare.md) |
| Estrategia de contención | Pasiva / Activa / Adaptativa | Sofisticación del atacante, riesgo de acelerar su cronograma | Equipo de respuesta + decision-makers | [10](capitulos/10-contain.md) |
| Terminar vs. monitorear | Terminación inmediata / Monitoreo extendido / Mixto | Destrucción activa de datos (→terminar) vs. *dwell time* + monitoreo maduro (→monitorear) | Criterios pre-acordados, no el momento | [10](capitulos/10-contain.md) |
| Re-entrar al Response Actions Loop | Sí / No | Nuevo IOC, expansión de alcance, erradicación incompleta, revelación de evidencia, o cambio de prioridad de negocio | Equipo de respuesta | [08](capitulos/08-response-actions-loop.md) |
| Salir del loop | Sí / No | Indicadores técnicos + de negocio + requisitos organizacionales alineados | Decision-maker nombrado, por escrito | [08](capitulos/08-response-actions-loop.md) |
| Retener evidencia forense | Retener / Eliminar | Riesgo de litigio, obligación regulatoria, involucramiento de fuerzas de seguridad, vs. costo de almacenamiento | Legales + equipo de respuesta | [13](capitulos/13-debrief.md) |
| Retener monitoreo reforzado | Retener / Modificar / Dar de baja | Cubre vacío real vs. sobrecarga operativa vs. sostenibilidad de mantenimiento | Equipo de respuesta + operaciones | [13](capitulos/13-debrief.md) |
| Pagar o no un rescate | Pagar / No pagar | Sensibilidad de datos expuestos, exposición regulatoria, certeza de recibir clave | Decision-maker ejecutivo + legales | [16](capitulos/16-ir-ransomware.md) |
| Aislar un sistema OT | Aislar / Monitorear sin aislar | Riesgo operacional y de seguridad física de la acción vs. de la amenaza | Ingeniería + equipo de seguridad, en conjunto | [18](capitulos/18-ir-ot.md) |
| Habilitar logging adicional en cloud | Habilitar / No habilitar | Sensibilidad del activo vs. costo de almacenamiento | Equipo de preparación, antes del incidente | [17](capitulos/17-ir-cloud.md) |
| Nivel de acceso de escritura en cloud durante respuesta | Service account automatizada / Just-in-time / Break-glass | Urgencia de la acción vs. principio de mínimo privilegio | Predefinido en Prepare | [17](capitulos/17-ir-cloud.md) |
| Usar IA generativa sobre datos del incidente | Sí, sanitizado / Sí, en modelo local / No | Sensibilidad del dato, política organizacional, marco regulatorio | Analista + política organizacional | [15](capitulos/15-ir-con-ia.md) |

## Principio transversal

En casi todas las filas, el libro insiste en lo mismo: la decisión debe estar **pre-acordada antes del incidente**, no improvisada bajo presión en el momento — ver en particular [05-prepare.md](capitulos/05-prepare.md) y [10-contain.md](capitulos/10-contain.md) ("pre-agreed criteria rather than judgment made in the moment").

## Ver también

[Matriz de procedimientos operativos](matriz-procedimientos.md) para los pasos mecánicos que acompañan cada decisión.
