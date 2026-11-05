# Guía de estudio extensa

Rutas de lectura sugeridas y preguntas de estudio consolidadas (cada capítulo trae las suyas en detalle — este archivo las agrupa para repaso rápido).

## Rutas de lectura sugeridas (siguiendo el criterio del propio autor en el Prefacio)

**Si estás empezando en IR**: [Prefacio](capitulos/front-prefacio.md) → [Caso Supply Chain Calamity](capitulos/caso-supply-chain-calamity.md) → [Introducción](capitulos/00-introduccion.md) → [Historia](capitulos/01-historia-ir.md) → [Primeros pasos](capitulos/02-primeros-pasos.md) → [Modelos existentes](capitulos/03-modelos-existentes.md) → recién ahí entrar a DAIR.

**Si ya conocés PICERL/NIST y querés entender DAIR específicamente**: ir directo a [El modelo DAIR](capitulos/04-dair-modelo.md) y de ahí recorrer [Prepare](capitulos/05-prepare.md) → [Debrief](capitulos/13-debrief.md) en orden.

**Si tenés una preocupación puntual**: [IA](capitulos/15-ir-con-ia.md), [Ransomware](capitulos/16-ir-ransomware.md), [Cloud](capitulos/17-ir-cloud.md) u [OT](capitulos/18-ir-ot.md) — cada uno asume que ya leíste el modelo DAIR base (Parte 2) y solo agrega la capa de consideraciones específicas.

**Si necesitás justificar DAIR ante auditoría/compliance**: [Integrando DAIR con NIST CSF 2.0](capitulos/14-integracion-csf.md) + [Análisis crítico](analisis-critico.md).

## Preguntas de estudio por bloque (resumen — el detalle completo está en cada capítulo)

### Fundamentos (capítulos 00-03)
- ¿Qué paso falta sistemáticamente entre "contención" y "cierre" en los casos narrativos del libro (NovaRise, Supply Chain Calamity)?
- ¿Qué modelo histórico (Schultz 1990 → SANS 1998 → PICERL) es el antecesor directo de tu proceso actual de IR, aunque nunca lo hayas llamado así?

### El modelo DAIR (capítulos 04-13)
- Para cada waypoint, identificá: ¿qué artefacto de documentación produce, y quién lo consume después?
- ¿En qué parte de tu proceso actual ya hacés *scoping* iterativo sin llamarlo así, y dónde todavía tratás la respuesta como lineal?
- Tomá un cierre de incidente reciente: ¿existe el registro escrito de "quién decidió salir del loop, con qué evidencia, aceptando qué riesgo residual"? Si no existe, ¿por qué?

### Consideraciones especiales (capítulos 14-18)
- Elegí un dominio (IA, ransomware, cloud, OT) relevante para tu organización y mapeá sus advertencias específicas contra un incidente real que hayas vivido. ¿Cuántas de esas advertencias se cumplieron?

### Análisis crítico
- Ver [analisis-critico.md](analisis-critico.md): ¿qué aporte de DAIR es genuino y cuál es más bien reempaquetado retórico de una práctica ya existente?

## Materiales de referencia rápida

- [Glosario bilingüe](glosario.md)
- [Índice de herramientas y técnicas](indice-herramientas.md)
- [Matriz de procedimientos operativos](matriz-procedimientos.md)
- [Matriz de decisiones y condiciones](matriz-decisiones.md)
- [Registro de cobertura y fuentes](registro-cobertura.md) — qué se cubrió, qué quedó pendiente, y cómo retomar.
