# Verify and Triage

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Verify and Triage Activity", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/verifytriage.html — ver también el anexo oficial [step-by-step-verify-triage.md](../anexos/step-by-step-verify-triage.md).

## Propósito

Es la función de filtro (*gating*) entre Detect y el Response Actions Loop: decidir si lo detectado es un incidente real y, si lo es, cuántos recursos organizacionales merece antes de involucrar a más stakeholders.

## Conceptos clave

- **Verificación**: determinar si un evento reportado es un incidente real o un falso positivo — evita gastar recursos en compromisos que no existen.
- **Triage**: trabajar junto a los decision-makers para determinar qué acción de respuesta corresponde, según la clasificación de riesgo y la información disponible.
- **Falso positivo**: evento que parece sospechoso pero no tiene evidencia de compromiso real.
- **Decision-makers**: quienes tienen autoridad para asignar recursos de respuesta — gerentes, ejecutivos, dueños de datos, legales, líderes de unidad de negocio.
- **EOI**: indicadores técnicos sospechosos que requieren investigación y enriquecimiento con inteligencia de amenazas.

## Las tres salidas posibles de la verificación

1. **Continuar**: el incidente se evalúa como real → escala al equipo de respuesta más amplio.
2. **Detener**: evidencia insuficiente de compromiso → se cierra el caso y se documentan los hallazgos.
3. **Diferir**: información insuficiente para decidir → se pide información adicional antes de resolver.

## Criterios de priorización (cuatro niveles)

- **Bajo**: anomalías menores, impacto organizacional mínimo.
- **Medio**: preocupación potencial que requiere investigación sin disrupción operativa.
- **Alto**: incidente confirmado que afecta operaciones de negocio o integridad de datos.
- **Crítico**: incidente mayor que exige escalamiento ejecutivo y contención inmediata.

La evaluación de riesgo pondera pérdida financiera, operativa y reputacional, además del impacto regulatorio potencial.

## Procedimientos de verificación

**Qué documentar**: identificador único del incidente (usualmente autogenerado), título descriptivo, handler asignado, resumen con fuente del reporte y timestamp, clasificación inicial, referencias a la evidencia recogida en Detect. Principio central: documentar *a medida que* el incidente avanza produce un mejor registro que reconstruirlo después de responder.

**Integración de inteligencia de amenazas (CTI)** refuerza la verificación de tres formas:
1. **Validación y enriquecimiento de EOIs**: consultar bases de reputación (VirusTotal, AlienVault OTX, Shodan) para ver si un indicador se correlaciona con actividad maliciosa conocida.
2. **Contexto de riesgo**: información de atribución y de actor de amenaza informa la clasificación inicial.
3. **Pivoteo de indicadores**: expandir desde un IOC puntual hacia indicadores relacionados.

**Ejemplo del capítulo**: la IP `147.45.44.131`, vista en descargas de un script PowerShell, se cruzó contra fuentes de CTI — VirusTotal mostró 15 de 95 proveedores marcándola como maliciosa, y AlienVault OTX aportó contexto adicional sobre el patrón de ataque.

## Integridad de la documentación

El capítulo advierte sobre el valor legal de la documentación: la contraparte puede cuestionar la autenticidad de las notas, preguntando si el cuaderno de trabajo contiene contenido no relacionado o señales de manipulación. Recomendación concreta: mantener la documentación del incidente separada de cualquier otro trabajo.

## Relación con otros modelos y capítulos

A diferencia de PICERL o NIST SP 800-61, que tratan detección y respuesta como un ciclo continuo, DAIR ubica la verificación como un *checkpoint* deliberado que evita asignar recursos a incidentes todavía no confirmados. Verify and Triage usa la información recogida en Detect sin necesitar todavía una investigación de alcance completa — esa viene después, en Scope, dentro del Response Actions Loop ([08-response-actions-loop.md](08-response-actions-loop.md)).

## Herramientas y tecnologías nombradas

VirusTotal · AlienVault OTX · Shodan · feeds comerciales de inteligencia de amenazas · plataformas de tracking de incidentes (sin mandato de una en particular).

## Advertencias

- En esta etapa la visibilidad suele ser limitada: hay que apoyarse en lo recogido durante Detect, no en una investigación completa.
- A veces el proceso de verificación no encuentra evidencia de compromiso pese a un comportamiento inexplicado que sugiere lo contrario — hay que aceptar esa incertidumbre, no forzar una conclusión.
- Los criterios de evaluación de riesgo varían bastante entre analistas de una misma organización — la consistencia de la clasificación requiere lineamientos organizacionales explícitos, no criterio individual.
- Bajo presión de respuesta activa, los analistas tienden naturalmente a postergar la documentación — el capítulo insiste en tratarla como práctica continua, no como tarea de cierre.

## Preguntas de estudio

1. Tomá un EOI real de tu entorno y recorré las tres salidas posibles (continuar/detener/diferir). ¿Qué información te falta hoy para decidir con confianza?
2. ¿Tu organización tiene lineamientos explícitos de clasificación de riesgo, o depende del criterio individual del analista de turno?
3. ¿Cómo mantenés vos la documentación del incidente separada del resto de tus notas de trabajo diario?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Verify and Triage Activity". CC BY 4.0. https://dynamicincidentresponse.com/chapters/verifytriage.html
