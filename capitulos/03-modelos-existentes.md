# Modelos de respuesta a incidentes y sus límites

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Incident Response Models and Their Limitations", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/existingmodels.html

## Tesis

Los marcos de IR establecidos — lineales o cíclicos — no alcanzan para la complejidad de un incidente moderno. El capítulo revisa tres marcos y en cada uno señala su límite concreto, preparando el terreno para DAIR en el capítulo siguiente.

## Modelos revisados

### PICERL (Schultz, 1990; refinado por la US Navy, el SEI de Carnegie Mellon y SANS)

Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned.

Progresión lineal "de la preparación a la resolución". Es, en términos históricos, el descendiente directo del modelo de seis pasos de SANS (1998) descripto en el capítulo de historia.

**Límite señalado**: se presenta como una progresión lineal que puede simplificar de más la complejidad de un incidente real — en particular, no modela bien que un atacante contenido pueda regresar, o que el *scoping* deba repetirse a medida que aparece evidencia nueva.

### NIST SP 800-61 Revisión 2 (2012)

Ciclo de vida de cuatro fases:
1. Preparation
2. Detection and Analysis
3. Containment, Eradication, and Recovery
4. Post-Incident Activity

Diseño cíclico: las lecciones aprendidas retroalimentan una preparación mejorada.

**Límites señalados**:
1. Reducción sustancial del nivel de detalle táctico respecto de guías anteriores.
2. Falta notoria de orientación específica sobre cómo recuperar sistemas tras un incidente.
3. Rigidez: la estructura prescriptiva de cuatro fases no se adapta bien a contextos organizacionales diversos.

### NIST SP 800-61 Revisión 3 / integración con CSF 2.0

Reestructuración completa: elimina el modelo discreto de cuatro pasos y distribuye la respuesta a incidentes entre las seis funciones del NIST CSF 2.0:

- **Govern (GV)** — estrategia, expectativas, política.
- **Identify (ID)** — comprensión del riesgo de ciberseguridad vigente.
- **Protect (PR)** — implementación de salvaguardas.
- **Detect (DE)** — hallazgo y análisis de ataques/compromisos.
- **Respond (RS)** — acciones sobre incidentes detectados.
- **Recover (RC)** — restauración de activos y operaciones.

Reencuadra la IR como "un componente de un programa integral de ciberseguridad", no como una disciplina autónoma con pasos propios.

**Límites señalados**:
- Dependencia del framework completo: integrar la capacidad de IR exige alinear las seis funciones de CSF 2.0, lo cual es una carga mayor para organizaciones no alineadas a CSF.
- Pérdida de una metodología discreta y propia: al disolver los pasos específicos de manejo de incidentes dentro de funciones más amplias, se puede perder claridad sobre responsabilidades específicas de cada fase.
- Queda posicionado como "perfil de comunidad de CSF 2.0", lo que limita su aplicabilidad directa fuera del ecosistema CSF.

## Tabla resumen

| Modelo | Autor / año | Fases | Límite principal señalado por el libro |
|---|---|---|---|
| PICERL | Schultz, 1990 | 6 secuenciales | Progresión lineal que simplifica de más la complejidad real |
| NIST SP 800-61 Rev. 2 | NIST, 2012 | 4 cíclicas | Menos detalle táctico; sin guía específica de recuperación |
| NIST SP 800-61 Rev. 3 | NIST (revisión posterior) | 6 funciones de CSF 2.0 | Depende del framework completo; carga de integración organizacional |

## Visualizaciones usadas en el capítulo

El libro muestra PICERL con dos diagramas: uno lineal (fases de izquierda a derecha con flechas de progresión) y uno escalonado tipo cascada, con una flecha de retroceso que marca el carácter iterativo que el modelo en teoría permite pero rara vez documenta bien en la práctica.

## Lo que el capítulo NO hace

No menciona explícitamente modelos emergentes como el ciclo OODA o MITRE ATT&CK en esta sección (aparecen en capítulos posteriores, en particular el ciclo OODA como base de DAIR). Tampoco discute frameworks sectoriales (salud, finanzas, infraestructura crítica). El foco es exclusivamente en los estándares gubernamentales/SANS de uso más extendido.

## Relación con otros capítulos

Es la contraparte crítica directa del capítulo de historia ([01-historia-ir.md](01-historia-ir.md)): ahí se narra el origen de PICERL y acá se audita su límite. Prepara el terreno conceptual para "A Dynamic Approach to Incident Response", donde se presenta DAIR como evolución —no ruptura— de PICERL, incorporando además un *crosswalk* explícito hacia NIST CSF 2.0 (ver capítulo "Integrating DAIR with NIST CSF 2.0").

## Preguntas de estudio

1. ¿En qué escenario concreto fallaría PICERL por asumir que el atacante queda contenido tras la fase de "Containment"?
2. ¿Qué organización se beneficia más de NIST SP 800-61 Rev. 3 (alineada a CSF) y cuál se perjudica (no alineada)?
3. Compará el límite de "falta de guía de recuperación" de la Rev. 2 con lo que vas a encontrar en el capítulo "Recover" de DAIR. ¿DAIR realmente lo resuelve?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Incident Response Models and Their Limitations". CC BY 4.0. https://dynamicincidentresponse.com/chapters/existingmodels.html
