# Dynamic Incident Response — Guía de estudio en español

Guía de estudio técnica en español de *Dynamic Incident Response: A Framework for Security Teams*, de **Joshua Wright** (con colaboradores Ryan Chapman, Megan Roddie-Fonseca y Dean Parsons).

**Esto no es una traducción del libro.** Es una síntesis técnica propia, capítulo por capítulo, escrita en español, pensada para estudiar el contenido sustantivo sin necesidad de leer inglés. Cada archivo está atribuido a la fuente exacta que resume.

## Licencia y atribución

La obra original está publicada bajo **Creative Commons Attribution 4.0 (CC BY 4.0)**: "Free to read, share, and adapt". Fuente oficial: https://dynamicincidentresponse.com/ · PDF oficial: https://dl.dynamicincidentresponse.com/dynamicir.pdf

- **Obra original**: *Dynamic Incident Response: A Framework for Security Teams*, © Joshua Wright.
- **Licencia**: CC BY 4.0 — https://creativecommons.org/licenses/by/4.0/
- **Transformación realizada en este repositorio**: síntesis técnica y traducción parcial al español, reorganizada por capítulo, con glosario, matrices de procedimientos/decisiones y análisis crítico propio agregado. No es una reproducción íntegra ni una traducción palabra por palabra del texto original.
- Los archivos en `anexos/` son las guías oficiales "Step-by-Step" (en inglés), descargadas sin modificar desde `dl.dynamicincidentresponse.com/resources/` — están publicadas por el propio autor explícitamente para reutilización ("drop the Markdown into your ticketing system, wiki, or AI agent"), así que se incluyen tal cual, con su atribución.

## Índice maestro

### Portada / front matter
- [Prefacio](capitulos/front-prefacio.md)
- [Prólogo (John Strand)](capitulos/front-prologo.md)

### Parte 1 — Elementos de la respuesta a incidentes
- [Caso de estudio: Supply Chain Calamity](capitulos/caso-supply-chain-calamity.md)
- [Introducción](capitulos/00-introduccion.md)
- [Una breve historia de la respuesta a incidentes](capitulos/01-historia-ir.md)
- [Primeros pasos (Getting Started)](capitulos/02-primeros-pasos.md)
- [Modelos de respuesta a incidentes y sus límites](capitulos/03-modelos-existentes.md)

### Parte 2 — Un enfoque dinámico de la respuesta a incidentes (DAIR)
- [El modelo DAIR](capitulos/04-dair-modelo.md)
- [Prepare](capitulos/05-prepare.md)
- [Detect](capitulos/06-detect.md)
- [Verify and Triage](capitulos/07-verify-triage.md)
- [Response Actions Loop](capitulos/08-response-actions-loop.md)
- [Scope](capitulos/09-scope.md)
- [Contain](capitulos/10-contain.md)
- [Eradicate](capitulos/11-eradicate.md)
- [Recover](capitulos/12-recover.md)
- [Debrief](capitulos/13-debrief.md)

### Parte 3 — Consideraciones especiales
- [Integrando DAIR con NIST CSF 2.0](capitulos/14-integracion-csf.md)
- [Acelerando la respuesta a incidentes con IA](capitulos/15-ir-con-ia.md)
- [Respuesta a incidentes para ransomware](capitulos/16-ir-ransomware.md)
- [Respuesta a incidentes para sistemas cloud](capitulos/17-ir-cloud.md)
- [Respuesta a incidentes para tecnología operacional (OT)](capitulos/18-ir-ot.md)

### Cierre
- [Epílogo (Afterword)](capitulos/zz-epilogo.md)

### Materiales complementarios propios
- [Glosario bilingüe](glosario.md)
- [Índice de herramientas y técnicas](indice-herramientas.md)
- [Matriz de procedimientos operativos](matriz-procedimientos.md)
- [Matriz de decisiones y condiciones](matriz-decisiones.md)
- [Análisis crítico: DAIR vs. PICERL / NIST SP 800-61 / NIST CSF 2.0](analisis-critico.md)
- [Registro de cobertura y fuentes](registro-cobertura.md)

### Anexos oficiales (guías Step-by-Step del autor, en inglés, sin modificar)
- [Prepare](anexos/step-by-step-prepare.md) · [Detect](anexos/step-by-step-detect.md) · [Verify and Triage](anexos/step-by-step-verify-triage.md) · [Response Actions Loop](anexos/step-by-step-response-actions-loop.md) · [Scope](anexos/step-by-step-scope.md) · [Contain](anexos/step-by-step-contain.md) · [Eradicate](anexos/step-by-step-eradicate.md) · [Recover](anexos/step-by-step-recover.md) · [Debrief](anexos/step-by-step-debrief.md)

## Qué es DAIR, en una línea

Un modelo de respuesta a incidentes construido sobre cinco *waypoints* (Prepare, Detect, Verify and Triage, Response Actions Loop, Debrief) donde el núcleo — Scope, Contain, Eradicate, Recover — se trata como un ciclo iterativo (inspirado en el ciclo OODA de Boyd), no como una secuencia lineal tipo PICERL. Ver desarrollo completo en [04-dair-modelo.md](capitulos/04-dair-modelo.md).

## Alcance de esta guía

No es exhaustiva palabra por palabra — es una extracción técnica densa: tesis, conceptos definidos, procedimientos, ejemplos, herramientas, advertencias y preguntas de estudio por capítulo, con referencia exacta a la fuente. Para el texto completo e íntegro, usar el PDF o HTML oficial (enlaces arriba).
