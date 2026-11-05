# Eradicate

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Eradicate Activity", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/eradicate.html — ver también el anexo oficial [step-by-step-eradicate.md](../anexos/step-by-step-eradicate.md).

## Propósito

Pasar de frenar al atacante (Contain) a remover sistemáticamente su presencia y revertir los cambios que hizo en el entorno. La erradicación busca eliminar el acceso del atacante y devolver los sistemas a un estado seguro — a diferencia de la contención, que frena la actividad en curso de forma inmediata, erradicar es un trabajo de fondo.

La tensión central: sostener rigor investigativo (para no quedar expuesto a una recompromisión) contra la urgencia operativa de volver a producir.

## Dos pistas de investigación en paralelo

- **Investigación corta (*short-form*)**: análisis rápido de evidencia para identificar método del atacante, mecanismos de persistencia y sistemas comprometidos. Prioriza velocidad; normalmente se completa durante la erradicación misma.
- **Investigación larga (*long-form*)**: análisis forense integral que sigue en paralelo, construyendo entendimiento más profundo de las TTPs para prevención futura, cumplimiento regulatorio, o un eventual proceso legal.

Ambas corren en paralelo para balancear urgencia contra profundidad forense.

## Análisis de causa raíz

Entender las condiciones de fondo que permitieron el compromiso — identificar el vector de acceso inicial, las credenciales comprometidas, los sistemas afectados, los mecanismos de persistencia, y la vulnerabilidad explotada.

## Preguntas críticas que la organización debe responder

- ¿Cuál fue el vector de acceso inicial? ¿Ya se cerró?
- ¿Qué credenciales se comprometieron? ¿Ya se rotaron?
- ¿A qué otros sistemas accedió el atacante?
- ¿Qué mecanismos de persistencia desplegó?
- ¿Qué vulnerabilidad habilitó el ataque? ¿Ya está parcheada?

Si alguna de estas preguntas queda sin respuesta, la erradicación es, por definición, incompleta.

## Procedimientos

**Enfoque guiado por investigación**: en vez de reconstruir sistemas de inmediato, el respondedor tiene que analizar la evidencia recolectada —logs, capturas de memoria, imágenes de disco, tráfico de red— para entender el método del atacante antes de remover nada.

**El atajo peligroso que el capítulo nombra explícitamente**: reconstruir sistemas desde medios limpios o imágenes gold sin investigación previa, y devolverlos a producción, para que el atacante vuelva a comprometer los mismos sistemas horas, días o semanas después. Es el patrón de falla más citado del capítulo.

**Remoción de artefactos y persistencia**: identificar y eliminar los componentes instalados por el atacante, cerrar los puntos de entrada explotados, y validar el éxito de la erradicación antes de pasar a Recover.

## Advertencias y límites

- **Tensión de tiempo**: apurar la erradicación arriesga dejar mecanismos de acceso persistente y vulnerabilidades sin resolver; pero invertir demasiado tiempo investigando cada detalle acumula impacto de negocio mientras el liderazgo cuestiona por qué los sistemas siguen offline. No hay una respuesta genérica — es un juicio caso por caso.
- **Riesgo de investigación incompleta**: saltear la investigación a favor de una recuperación rápida deja la puerta abierta a una recompromisión por el mismo vector exacto.
- **Restricciones de recursos**: la investigación larga exige recursos significativos y expertise especializado, lo cual compite con la capacidad organizacional disponible en simultáneo con otras demandas del incidente.

## Herramientas y tecnologías mencionadas

El capítulo no enumera productos específicos — habla de insumos analíticos: logs y su análisis, capturas de memoria, imágenes de disco/análisis forense, análisis de tráfico de red, sistemas BDR (Business Disaster Recovery).

## Relación con otros capítulos

Erradicar depende de la evidencia que salió de Contain ([10-contain.md](10-contain.md)) y es el paso obligado antes de Recover ([12-recover.md](../capitulos/12-recover.md)) — no se puede validar una recuperación si la erradicación no se confirmó primero. Dentro del Response Actions Loop, una erradicación incompleta es uno de los cinco disparadores explícitos de re-entrada al ciclo (ver [08-response-actions-loop.md](08-response-actions-loop.md)).

## Preguntas de estudio

1. Tomá las cinco preguntas críticas del capítulo y aplicalas a un incidente real o hipotético de tu entorno. ¿Cuántas podés responder hoy con confianza?
2. ¿Cómo evitarías en tu organización el "atajo peligroso" (reconstruir sin investigar) bajo presión de negocio para volver a producción ya?
3. ¿Qué recursos tenés disponibles hoy para sostener una investigación *long-form* en paralelo con la *short-form*, sin que una canibalice a la otra?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Eradicate Activity". CC BY 4.0. https://dynamicincidentresponse.com/chapters/eradicate.html
