# Respuesta a incidentes para tecnología operacional (OT)

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Incident Response for Operational Technology", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/considerations-ot.html

## Tesis

La IR en OT no puede tratarse como una extensión de las prácticas de respuesta empresarial de IT. Tiene que ejecutarse con contexto de ingeniería y conciencia operacional. El propósito va más allá de eliminar la amenaza: busca preservar procesos físicos seguros y confiables, manteniendo la visibilidad y el control del operador durante toda la investigación.

## Conceptos clave

- **Tecnología operacional (OT)**: sistemas que monitorean y controlan dispositivos físicos, procesos e infraestructura — abarca ICS (Industrial Control Systems), SCADA, DCS (Distributed Control Systems) y PLCs (Programmable Logic Controllers).
- **Modelo Purdue**: arquitectura de red jerárquica que separa la operación empresarial del control industrial en cinco niveles (0 a 5), con el Nivel 3.5 como la DMZ industrial que marca el límite entre ambos mundos.
- **Prioridad de seguridad física (*safety*)**: en OT, proteger al personal y mantener el control del proceso está por encima de la confidencialidad de los datos — invierte la prioridad típica de IT (donde la confidencialidad suele ir primero).
- **Contexto de ingeniería**: conocimiento específico del dominio sobre cómo operan los sistemas industriales, cómo se comunican (protocolos como Modbus, EtherNet/IP) y cómo interactúan con el proceso físico real.

## Procedimientos específicos de OT/ICS

**Verificar y hacer triage antes de contener**: actuar sobre un evento sin verificar puede disrupción las operaciones, comprometer visibilidad crítica, comprometer la seguridad física, o interrumpir el control del proceso. Por eso se exige involucrar al equipo de ingeniería para validar el evento antes de tomar cualquier acción restrictiva — a diferencia de IT, donde contener rápido suele ser la prioridad por defecto.

**Respuesta informada por ingeniería**: cada acción de respuesta tiene que evaluar su impacto potencial sobre el comportamiento del sistema de control, la visibilidad del operador y la estabilidad del proceso, antes de ejecutarse.

**Prioridad del monitoreo pasivo**: los entornos OT tienden a priorizar monitoreo pasivo, validación informada por ingeniería, y acciones de respuesta estrechamente coordinadas, por sobre modelos de respuesta fuertemente automatizados — otra inversión respecto de la lógica habitual de IT.

**Contención y remediación por etapas**: acciones que requieren downtime del sistema tienen que coordinarse cuidadosamente con ingeniería y operaciones, en particular en sectores como oil/gas o energía eléctrica, donde una parada puede durar horas o días.

## Caso del capítulo: malware en una refinería

Una HMI (Human-Machine Interface) con Windows recibe malware genérico vía USB. El malware no podía alcanzar servidores C2 (bloqueado por la arquitectura de red), no representaba riesgo operativo real, y ya se estaba gestionando vía monitoreo y remoción programada en el próximo mantenimiento. Pero un técnico de IT desconectó el sistema sin consultar — eliminando al instante la visibilidad del operador y obligando a reubicar personal in situ para controlar el proceso de forma manual. La acción de contención causó más disrupción que la amenaza misma.

**Lo que ilustra el caso**: las prácticas de contención agresiva típicas de IT introducen riesgo operacional y de seguridad física inaceptable en un entorno industrial.

## Abuso de protocolos industriales

Muchos ataques a OT explotan herramientas de ingeniería legítimas, credenciales válidas y vías de acceso remoto permitidas — no malware. El respondedor tiene que distinguir uso autorizado de abuso adversarial sin tener, muchas veces, el contexto completo para hacerlo con certeza.

## Herramientas, tecnologías y estándares nombrados

**Protocolos**: Modbus, DNP3, EtherNet/IP, PROFINET, ICCP. **Tipos de activo**: HMIs, estaciones de trabajo de ingeniería, historians, servidores SCADA, RTUs (Remote Terminal Units), relés de protección y control. **Estándares**: ISA/IEC 62443 (seguridad de automatización industrial), ISA-95 (integración empresa-control). **Enfoque de monitoreo**: comprensión de la arquitectura de red y observación pasiva, por sobre sistemas de respuesta automatizada.

## Advertencias y límites críticos

- **Ciclos de vida de activo muy largos**: el equipo industrial opera sin cambios durante décadas, lo cual limita los tiempos de parcheo y actualización comparado con hardware empresarial (que se renueva cada pocos años).
- **Dependencia del proveedor**: la remediación depende fuertemente del soporte del proveedor, ventanas de mantenimiento, certificaciones y requisitos regulatorios — no está disponible bajo demanda como en IT.
- **Intolerancia a falsos positivos**: los entornos OT tienen muy baja tolerancia a falsos positivos — aislar un sistema por una alerta incorrecta puede interrumpir lazos de control, degradar visibilidad, o afectar la calidad del producto.
- **Logging limitado**: los sistemas OT en general carecen de las capacidades extensas de logging propias de las redes IT modernas, lo que limita la profundidad de la investigación forense posible.
- **Sin exposición directa a internet**: los modelos de amenaza típicos de IT, que asumen acceso amplio de usuarios a internet, no aplican a redes OT segmentadas — cambia por completo la superficie de ataque asumida.

## El "modelo de engranajes": seis áreas interconectadas

El capítulo ilustra seis áreas que se afectan mutuamente en cada decisión de respuesta OT: seguridad física (*safety*), habilidades requeridas, diseño del sistema, soporte del proveedor, controles de ciberseguridad, y respuesta a incidentes de seguridad. Una decisión en un área impacta directamente en todas las demás — elegir una acción de contención afecta simultáneamente las habilidades disponibles, las restricciones del sistema, las implicancias de seguridad física, los requisitos de soporte, y las dependencias de la arquitectura de control.

## Comparación IT vs. OT (impacto potencial)

| Dimensión | IT | OT |
|---|---|---|
| Alcance | Impacto de negocio local | Disrupción de infraestructura a escala regional |
| Integridad de datos | Corrupción digital | Manipulación del proceso físico |
| Pérdida | Pérdida de información | Seguridad del personal, riesgo de vida |

Esta comparación justifica por qué cada acción de respuesta debe validarse con ingeniería y operaciones antes de implementarse, para preservar la estabilidad del proceso durante toda la respuesta.

## Relación con otros capítulos

El capítulo remite a la Parte 2 (el modelo DAIR completo) para la guía general de cada actividad de respuesta, aplicando sobre esa base las modificaciones OT-específicas descriptas acá — el mismo patrón que siguen los capítulos de ransomware y cloud.

## Preguntas de estudio

1. En el caso de la refinería, ¿qué paso de "verificar antes de contener" hubiera evitado que el técnico de IT desconectara la HMI sin consultar?
2. Tomá el "modelo de engranajes" (seis áreas) y aplicalo a una decisión de contención real en tu entorno OT — ¿qué área se te suele pasar por alto?
3. ¿Cómo evaluarías la intolerancia a falsos positivos de tu entorno OT frente al costo de una contención innecesaria?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Incident Response for Operational Technology". CC BY 4.0. https://dynamicincidentresponse.com/chapters/considerations-ot.html
