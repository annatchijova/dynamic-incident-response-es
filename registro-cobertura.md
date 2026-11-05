# Registro de cobertura y fuentes

Manifiesto de progreso — permite retomar el trabajo si la sesión se corta. Última actualización: 2026-11-05.

## Estado general

**Todos los capítulos del índice oficial fueron procesados.** 22 archivos de síntesis en `capitulos/` + 6 materiales complementarios propios + 9 anexos oficiales descargados sin modificar.

## Tabla de cobertura

| Fuente (HTML oficial) | Archivo de esta guía | Estado | Notas |
|---|---|---|---|
| chapters/foreword.html | capitulos/front-prologo.md | ✅ Completo | — |
| chapters/preface.html | capitulos/front-prefacio.md | ✅ Completo | — |
| chapters/supplychaincalamity.html | capitulos/caso-supply-chain-calamity.md | ✅ Completo | Personaje "Sam" mencionado en el índice del libro, sin detalle sustancial accesible en esta extracción — señalado explícitamente como vacío |
| chapters/introduction.html | capitulos/00-introduccion.md | ✅ Completo | — |
| chapters/historyofir.html | capitulos/01-historia-ir.md | ✅ Completo | El modelo de "al menos seis etapas" de Schultz et al. 1990 no se detalla paso a paso en la fuente disponible — señalado como vacío en el propio capítulo |
| chapters/gettingstarted.html | capitulos/02-primeros-pasos.md | ✅ Completo | — |
| chapters/existingmodels.html | capitulos/03-modelos-existentes.md | ✅ Completo | — |
| chapters/dynamicapproach.html | capitulos/04-dair-modelo.md | ✅ Completo | La conexión explícita con OODA se tomó de la FAQ del sitio, no del cuerpo del capítulo — señalado en el texto |
| chapters/prepare.html | capitulos/05-prepare.md | ✅ Completo | Capítulo largo (531 líneas en su anexo step-by-step); esta síntesis cubre lo conceptual, no cada sub-sección de playbook |
| chapters/detect.html | capitulos/06-detect.md | ✅ Completo | — |
| chapters/verifytriage.html | capitulos/07-verify-triage.md | ✅ Completo | El escenario completo "Third-Party Vendor Breach" referenciado en el capítulo no se extrajo en detalle — señalado como vacío |
| chapters/responseactionsloop.html | capitulos/08-response-actions-loop.md | ✅ Completo | — |
| chapters/scope.html | capitulos/09-scope.md | ✅ Completo | — |
| chapters/contain.html | capitulos/10-contain.md | ✅ Completo | — |
| chapters/eradicate.html | capitulos/11-eradicate.md | ✅ Completo | — |
| chapters/recover.html | capitulos/12-recover.md | ✅ Completo | — |
| chapters/debrief.html | capitulos/13-debrief.md | ✅ Completo | — |
| chapters/considerations-ai.html | capitulos/15-ir-con-ia.md | ✅ Completo (parcial por diseño) | El capítulo remite a sub-secciones propias ("Foundational/Intermediate/Advanced Use Cases") no desarrolladas en el detalle operativo completo en esta guía — señalado explícitamente |
| chapters/considerations-ransomware.html | capitulos/16-ir-ransomware.md | ✅ Completo | — |
| chapters/considerations-cloud.html | capitulos/17-ir-cloud.md | ✅ Completo | — |
| chapters/considerations-ot.html | capitulos/18-ir-ot.md | ✅ Completo | — |
| chapters/integration.html | capitulos/14-integracion-csf.md | ✅ Completo | — |
| chapters/afterward.html | capitulos/zz-epilogo.md | ✅ Completo | — |

## Método de extracción

Cada capítulo HTML oficial se procesó con una herramienta de fetch+resumen (no lectura directa del PDF completo), seguida de síntesis propia en español escrita desde cero a partir de esa extracción — nunca copiando ni traduciendo literalmente el resultado intermedio. El PDF oficial (`~/Downloads/dynamicir.pdf`) se usó como referencia de respaldo para verificar la licencia y la estructura general, no se procesó página por página para contrastar figuras/tablas con el detalle que pedía la consigna original — **esa verificación visual de figuras contra el PDF queda pendiente** si se quiere llevar esta guía a un nivel de fidelidad mayor.

## Pendientes explícitos (no se afirma cobertura donde no la hay)

1. **Verificación visual de figuras/diagramas contra el PDF**: las descripciones de figuras (p. ej. Figuras 1-5 de "A Dynamic Approach to Incident Response") se basan en la descripción textual que dio la herramienta de extracción, no en inspección directa del PDF. Recomendado antes de publicar: abrir el PDF y confirmar cada descripción.
2. **Vacíos señalados en la tabla de arriba** (modelo de seis etapas de Schultz 1990, escenario "Third-Party Vendor Breach", sub-secciones avanzadas del capítulo de IA).
3. **Cifras y estadísticas citadas por el libro** (ransomware, cloud threat reports) — ver advertencia explícita en [analisis-critico.md](analisis-critico.md), sección 5: no verificadas contra la fuente primaria original.
4. **Errata oficial del libro** (`errata.html`) no se revisó — si el PDF en Downloads tiene una edición con erratas corregidas o pendientes, valdría la pena cotejar antes de publicar.

## Próximo paso si se retoma esta sesión

Si hace falta profundizar más allá de esta guía de estudio, los pasos pendientes en orden de prioridad serían: (1) revisar errata.html, (2) confirmar figuras contra el PDF, (3) decidir si se publica el repo en GitHub bajo `annatchijova` (ya acordado con el usuario) o si se queda como material de estudio local.
