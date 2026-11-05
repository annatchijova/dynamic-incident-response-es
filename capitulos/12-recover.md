# Recover

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Recover Activity", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/recover.html — ver también el anexo oficial [step-by-step-recover.md](../anexos/step-by-step-recover.md).

## Propósito

La transición de eliminar la amenaza a restaurar la operación normal. Recuperar es un proceso orquestado que garantiza que los sistemas restaurados sean seguros, funcionales y estén listos para soportar la operación *antes* de devolverlos a producción — no es simplemente "sacar la contención y prender todo de nuevo".

La tensión que el capítulo nombra: la urgencia de restaurar servicio contra la necesidad de una validación exhaustiva. Apurar la recuperación arriesga recompromisión por vulnerabilidades que sobrevivieron; demorarse de más acumula el impacto del incidente.

## Conceptos clave

- **Verificación previa a la restauración**: confirma que la erradicación fue exitosa y que las causas raíz se remediaron, *antes* de activar cualquier sistema.
- **Pruebas de validación del sistema**: pruebas funcionales (¿las aplicaciones operan correctamente?), validación de controles de seguridad (¿el agente EDR, el firewall y el logging funcionan?), pruebas de interconectividad (¿el sistema se comunica bien con sistemas dependientes, bases de datos y flujos de autenticación?).
- **Aceptación del dueño del sistema (*system owner acceptance*)**: validación de la unidad de negocio que establece responsabilidad y confirma que el sistema está listo para operar, documentada con un sign-off formal.
- **Monitoreo reforzado**: observabilidad elevada durante y después de la restauración para detectar anomalías.

## Checklist previo a la restauración (nueve pasos, según el capítulo)

1. Confirmación de remediación de la causa raíz (parches, rotación de credenciales, corrección de configuración).
2. Aplicación de actualizaciones de seguridad pendientes.
3. Verificación de remoción de mecanismos de persistencia.
4. Validación de que el backup a usar es anterior al incidente (no posterior).
5. Verificación del proceso de reconstrucción usando fuentes confiables.
6. Confirmación del estado de los controles de seguridad.
7. Escaneo final de IOCs — **a propósito, el último paso**, para que el escaneo refleje la configuración real de producción y no un estado intermedio sin endurecer todavía.

**Guía crítica**: el escaneo de IOCs tiene que ocurrir *después* de todo el hardening, nunca antes — si se escanea en un estado intermedio, el resultado no dice nada sobre el sistema que realmente va a producción.

## Proceso de validación del sistema

- **Pruebas funcionales**: recorrer los flujos operativos estándar usando documentación de UAT (User Acceptance Testing) ya existente.
- **Validación de controles de seguridad**: confirmar que el EDR reporta, que el firewall de host está configurado según política, y que el logging está habilitado.
- **Verificación de interconectividad**: probar conexiones a base de datos, comunicación entre servidores de aplicación, y flujos de autenticación.

## Marco de aceptación del dueño del sistema

- Involucramiento temprano del dueño en la planificación de la validación.
- Provisión de planes de prueba, o testing de aceptación liderado por la propia unidad de negocio.
- Sign-off documentado, que establece una línea base y una transferencia clara de responsabilidad.

## Advertencias y límites

1. **Complejidad de validar la línea de tiempo**: hace falta una cronología precisa del incidente para poder validar que un backup realmente es anterior al compromiso — sin esa cronología, no se puede confiar en el backup elegido.
2. **Disponibilidad del dueño del sistema**: la aceptación exige participación de la unidad de negocio, lo cual puede demorar la recuperación si esa persona no está disponible.
3. **Incompletitud de las pruebas técnicas**: la validación técnica puede no detectar problemas operativos que solo conocen los usuarios de negocio.
4. **Drift de configuración**: sistemas offline por períodos extendidos pueden necesitar una validación más extensa de lo habitual.
5. **Riesgo de atribución injusta**: cualquier problema posterior puede atribuirse al esfuerzo de respuesta al incidente, incluso cuando ese problema ya existía antes del incidente — una advertencia práctica para documentar bien el estado previo.

## Herramientas y tecnologías mencionadas

Agentes EDR · firewalls basados en host · sistemas de backup (con validación de línea de tiempo) · herramientas de escaneo de IOCs (sin marca específica) · infraestructura de logging. El capítulo se mantiene deliberadamente a nivel de categoría de capacidad, no de producto.

## Relación con otros capítulos

Recover usa directamente los hallazgos de Detect/Scope (los IOCs para la validación final) y de Eradicate ([11-eradicate.md](11-eradicate.md)) — no se puede validar una recuperación si la erradicación no se confirmó antes. Las métricas que salen de esta fase alimentan la revisión posterior en Debrief ([13-debrief.md](13-debrief.md)).

## Preguntas de estudio

1. ¿Tu organización documenta el estado "previo al incidente" de forma tal que pueda defenderse de una atribución injusta de problemas no relacionados?
2. Si tu backup más reciente es de hace tres días y el compromiso lleva dos semanas sin detectarse, ¿qué implica eso para el paso 4 del checklist?
3. ¿Qué pasa en tu organización si el dueño del sistema no está disponible para el sign-off? ¿Hay una ruta de escalamiento definida?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Recover Activity". CC BY 4.0. https://dynamicincidentresponse.com/chapters/recover.html
