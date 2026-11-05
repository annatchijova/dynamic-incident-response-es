# Prepare

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Prepare Activity", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/prepare.html — ver también el anexo oficial [step-by-step-prepare.md](../anexos/step-by-step-prepare.md).

## Propósito

Construir la capacidad organizacional de respuesta *antes* de que ocurra el incidente: políticas, entrenamiento, capacidades preventivas/detectivas desplegadas. Es la fase cuyo valor es más difícil de justificar económicamente, precisamente porque su éxito se mide por incidentes que no escalan.

## Conceptos clave

- **Políticas**: directivas de alto nivel de la organización (pagar o no un rescate, cuándo involucrar a legales, procedimientos de divulgación) — las fija el liderazgo, no el equipo técnico.
- **Planes**: estructuras operativas que traducen la política en práctica — roles, rutas de escalamiento, flujos de comunicación, típicamente documentados en una matriz RACI.
- **Playbooks**: guía táctica paso a paso para responder a un tipo específico de incidente con las herramientas designadas — responden "¿cómo respondemos, concretamente?".
- **Clasificación de riesgo**: umbrales de severidad predefinidos (niveles 0 a 5) que mapean características del incidente a prioridad de respuesta, según sistemas afectados, sensibilidad de datos e impacto de negocio.
- **Niveles de autorización de contención**:
  - **Nivel 1 (SOC/IRT)**: endpoints individuales, cuentas de usuario, bloqueo de IP.
  - **Nivel 2 (dueño del servicio)**: aislamiento de servidores, cuentas de servicio, reglas de firewall funcionales.
  - **Nivel 3 (ejecutivo)**: apagado de producción, segmentación de red, notificaciones regulatorias.

## Procedimientos descriptos

**Desarrollo de políticas** en colaboración con stakeholders, cubriendo: alineación con la misión y objetivos del programa, protocolos de involucramiento de management (GRC, legales, prensa), postura frente a ransomware/extorsión y comunicación con el atacante, retención de evidencia y cadena de custodia, políticas de contacto con fuerzas de seguridad y divulgación pública, criterios de involucramiento de terceros.

**Construir apoyo de management**: mostrar el valor de la IR con ejemplos de la industria, briefings regulares sobre desarrollos regulatorios/de amenazas, buscar el expertise de management al redactar políticas, asignar responsabilidades concretas (ejercicios de mesa, participación en guardias), y presentar opciones ya pensadas en vez de preguntas abiertas.

**Evaluación de riesgo**: criterios de severidad claros, vía matrices amplias (impacto vs. urgencia) o árboles de decisión detallados (clasificación por flowchart).

**Preparación del equipo**: habilidades técnicas, relaciones ya establecidas, procedimientos documentados, acceso al toolset, ejercicios de entrenamiento colaborativo.

**Prevención y detección proactiva**: gestión de vulnerabilidades, monitoreo de seguridad e integración de inteligencia de amenazas cibernéticas, para reducir la frecuencia de incidentes y mejorar la identificación temprana.

## Ejemplos del capítulo

**Comunicación de políticas — mal vs. bien** (parafraseado):
- Mal: preguntar abiertamente "¿cuándo querés que involucremos a legales?" sin proponer nada.
- Bien: proponer un criterio concreto — por ejemplo, involucrar a legales ante incidentes confirmados con potencial divulgación pública, reclamo a la aseguradora cyber, o coordinación con fuerzas de seguridad — y preguntar si eso coincide con la expectativa del management.

**Niveles de severidad CISA**: citados como ejemplo de árbol de decisión que guía al respondedor desde criterios de impacto hasta una clasificación.

**Matriz de priorización tipo InvGate**: grilla simple 3×3 que cruza urgencia contra alcance del impacto para determinar prioridad del incidente.

## Advertencias y límites

- **La paradoja de la preparación**: una organización que invierte fuerte en preparación puede nunca sufrir un incidente mayor, lo que hace difícil justificar el ROI. El libro propone encuadrar la inversión como reducción de riesgo, no como prevención de incidentes, y medir con métricas como MTTD y desempeño en ejercicios de mesa.
- **Parálisis de escalamiento**: sin niveles de autorización predefinidos, los respondedores dudan antes de contener, y esa demora cuesta caro. Los niveles de autorización resuelven esto mapeando la aprobación requerida al *impacto* de la acción, no a la antigüedad del respondedor.
- **Consideraciones regulatorias**: organizaciones sujetas a NIS2 o DORA deben incorporar obligaciones de notificación y evaluación de impacto al definir sus niveles de autorización de contención.

## Herramientas y tecnologías nombradas

Matrices RACI · procedimientos de cadena de custodia y retención de evidencia · retainers de seguro cibernético · proveedores externos de respuesta a incidentes · plataformas de monitoreo de seguridad (mencionadas en general, sin marca específica).

## Relación con otros capítulos

Prepare es la base explícita sobre la que se apoyan Detect, Verify and Triage y el Response Actions Loop — en particular, la efectividad de Detect depende directamente de decisiones tomadas acá (qué se despliega, qué se entrena). El capítulo sitúa a DAIR junto a PICERL y NIST SP 800-61 como los tres modelos frente a los cuales Prepare es, en los tres, la fase fundacional.

## Preguntas de estudio

1. ¿Tu organización tiene niveles de autorización de contención definidos? Si el Nivel 2 y el Nivel 3 no están claros, ¿qué pasa en la práctica cuando hay que decidir rápido?
2. Redactá, para tu propio contexto, una propuesta de política de involucramiento de legales siguiendo el patrón "bien" del capítulo (opción concreta, no pregunta abierta).
3. ¿Cómo medirías el ROI de la preparación en una organización que lleva dos años sin un incidente mayor?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Prepare". CC BY 4.0. https://dynamicincidentresponse.com/chapters/prepare.html
