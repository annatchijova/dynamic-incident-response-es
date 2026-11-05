# Una breve historia de la respuesta a incidentes

> Guía de estudio en español — síntesis propia, no traducción. Basado en "A Short History of Incident Response", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/historyofir.html

## Tesis

Entender de dónde vienen los marcos formales de IR —y qué restricciones puntuales atendían en su momento— explica tanto su valor duradero como sus límites frente a las amenazas actuales.

## Conceptos clave

- **Incidente de ciberseguridad**: evento de seguridad discreto que exige respuesta coordinada, desde la explotación individual de un hacker hasta la propagación de un worm que afecta miles de sistemas.
- **Respuesta a incidentes**: enfoque estructurado y metódico frente a emergencias de seguridad, distinto de la resolución de problemas ad-hoc por administradores de sistema.
- **Vulnerabilidad**: debilidad técnica explotable (puerta trasera DEBUG de Sendmail, buffer overflow, autenticación débil).

## Línea de tiempo de incidentes fundacionales (según el capítulo)

| Año | Incidente | Relevancia |
|---|---|---|
| 1982 | The 414s | Adolescentes de Milwaukee comprometen 60+ sistemas, incluido Los Alamos |
| 1984 | Chaos Computer Club — hackeo BTX | Expone vulnerabilidades de sistemas bancarios alemanes |
| 1986 | Cuckoo's Egg / espionaje KGB | Primer caso documentado de ciberespionaje; popularizado luego por el libro de Clifford Stoll |
| 1987 | Intrusión de señal "Max Headroom" | Secuestro de transmisión televisiva; autores nunca identificados |
| 1988 | Morris Worm | ~6.000 computadoras infectadas (~10% de internet de la época) |
| 1992 | Virus Michelangelo | Activación programada (6 de marzo) genera alarma pública |
| 1994-95 | Persecución de Mitnick por Shimomura | Termina en arresto en febrero de 1995 |
| 1998 | Moonlight Maze | Campaña prolongada, sospechada de origen ruso, contra redes militares/gubernamentales de EE.UU. |
| 1999 | Virus Melissa | Propagación rápida por correo; ~80 millones de dólares en daños |

## El Morris Worm como punto de inflexión

**Vector de ataque** — tres vías contra sistemas UNIX:
- Ejecución remota de código vía la vulnerabilidad DEBUG de Sendmail.
- Buffer overflow en el servicio Finger.
- Explotación de contraseñas débiles vía el servicio RSH.

**Error de propagación**: un error de programación hizo que el worm se replicara mucho más agresivamente de lo previsto, reinfectando las mismas máquinas repetidamente hasta volverlas inutilizables — una falla de control que amplificó el impacto más allá de la intención del propio autor.

**Impacto económico**: según documentos judiciales, el costo de limpieza fue de USD 200 a USD 53.000 por máquina infectada (≈ USD 558 a USD 148.000 en dólares de 2026 según el ajuste que hace el libro).

**Consecuencia legal**: Robert Morris fue condenado bajo la Computer Fraud and Abuse Act (CFAA): tres años de probation, 400 horas de servicio comunitario y una multa de USD 10.050.

El capítulo incluye pseudocódigo del mecanismo real del exploit DEBUG de Sendmail (Listing 1 en el original) para anclar la discusión en detalle técnico verificable, no solo en narrativa.

## Respuestas institucionales

**CERT (17 de noviembre de 1988)**
- Creado por DARPA en el Software Engineering Institute de Carnegie Mellon.
- A solo dos semanas del Morris Worm.
- Misión: punto central de coordinación para emergencias de seguridad en internet, divulgación de vulnerabilidades y distribución de parches.

**CIAC (1989)**
- Iniciativa del Departamento de Energía de EE.UU., en el Lawrence Livermore National Laboratory.
- Fundador: Dr. E. Eugene Schultz Jr.
- Alcance más acotado que el de CERT: protección de investigación clasificada e infraestructura crítica (investigación de armas nucleares, redes eléctricas).

## Formalización metodológica

**Schultz et al., 1990** — *"Responding to Computer Security Incidents: Guidelines for Incident Handling"*, identificado por el capítulo como el documento fundacional. Establece:

**Jerarquía de prioridades en la respuesta:**
1. Proteger vidas humanas y su seguridad.
2. Proteger datos clasificados y sensibles.
3. Proteger otros datos.
4. Prevenir daño a los sistemas.
5. Minimizar la disrupción de recursos de cómputo.

**Modelo de al menos seis etapas** de respuesta (el capítulo no detalla las seis explícitamente en esta fuente).

**Desarrollos posteriores:**
- 1996 — US Navy, *"Computer Incident Response Guidebook P-5239-19"*: amplía el marco de Schultz con procedimientos específicos militares.
- 1998 — SANS Institute, liderado por Stephen Northcutt: *"Computer Security Incident Handling: Step-by-Step"* (v1.5), compilando prácticas de más de 50 organizaciones.

**Modelo de seis pasos de SANS** (el antecesor directo de PICERL):
1. Preparation
2. Identification
3. Containment
4. Eradication
5. Recovery
6. Follow-up

La guía SANS incluía enunciados de problema estructurados, acciones numeradas, "Emergency Action Cards" (tarjetas de referencia de una página) y secciones específicas por tipo de incidente (malware, denegación de servicio, espionaje, hoaxes, acceso no autorizado).

## Herramientas y tecnologías nombradas

Sendmail (agente de transferencia de correo UNIX con la vulnerabilidad DEBUG) · servicio Finger (con buffer overflow explotable) · Remote Shell / RSH (explotado vía contraseñas débiles) · ARPANET (red precursora de internet, financiada por DARPA).

## Advertencias y límites implícitos

El capítulo no lo dice de forma explícita pero lo deja planteado como gancho hacia el resto del libro: los marcos nacidos de la era del Morris Worm pueden no cubrir el panorama de amenazas actual. El título de cierre de la sección ("From These Foundations") funciona como puente hacia el capítulo siguiente, que cuestiona los modelos lineales heredados de esta historia.

## Relación con otros capítulos

- Continúa directamente del capítulo "Introduction" ([00-introduccion.md](00-introduccion.md)).
- Es el antecedente histórico directo del capítulo "Incident Response Models and Their Limitations", donde PICERL (herencia explícita del modelo de seis pasos de SANS descripto acá) se somete a crítica.
- El modelo DAIR, presentado más adelante, se posiciona explícitamente como evolución de esta línea histórica, no como ruptura total.

## Preguntas de estudio

1. ¿Por qué el error de propagación del Morris Worm es un buen ejemplo de "falla de control" más que de "éxito del ataque según lo planeado"?
2. Compará la jerarquía de prioridades de Schultz et al. (1990) con la jerarquía implícita en tu propia organización. ¿Coinciden?
3. El modelo de seis pasos de SANS (1998) es el ancestro directo de PICERL. ¿Qué paso del modelo original creés que es más difícil de sostener frente a un atacante que regresa tras la contención?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "A Short History of Incident Response". CC BY 4.0. https://dynamicincidentresponse.com/chapters/historyofir.html
