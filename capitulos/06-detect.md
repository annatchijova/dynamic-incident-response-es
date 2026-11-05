# Detect

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Detect Activity", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/detect.html — ver también el anexo oficial [step-by-step-detect.md](../anexos/step-by-step-detect.md).

## Propósito

Identificar incidentes potenciales mediante metodologías estructuradas y análisis de datos. El capítulo parte de la observación de que buena parte del tiempo de un analista de IR se va en actividades de detección — buscar señales de compromiso entre el ruido.

## Las cuatro metodologías de detección

- **Basada en firmas (*signature-based*)**: coincidencia de patrones conocidos (hashes de archivo, secuencias de bytes, dominios maliciosos, indicadores de red). Eficiente y con baja tasa de falsos positivos, pero reactiva por naturaleza: falla contra amenazas nuevas hasta que alguien crea la firma correspondiente. Límite señalado explícitamente: un atacante que hace ingeniería inversa de la firma puede modificar su herramienta para evitar la coincidencia.
- **Basada en comportamiento (*behavioral*)**: monitorea acciones, no indicadores estáticos — establece una línea base de actividad normal y marca desvíos. Es fuerte para detectar cifrado masivo tipo ransomware, patrones de acceso inusuales, técnicas *living-off-the-land* (abuso de herramientas legítimas) y amenazas internas. Exige calibración cuidadosa para balancear cobertura contra falsos positivos.
- **Machine learning**: modelos supervisados (entrenados con ejemplos etiquetados) y no supervisados (aprenden el patrón normal sin etiquetas). Límites: *model drift* (degradación gradual de precisión a medida que el atacante cambia de técnica), calidad de los datos de entrenamiento, y evasión (adversarios que diseñan entradas específicamente para esquivar la clasificación del modelo).
- **Híbrida**: combina las tres — firmas para lo conocido, comportamiento para técnicas nuevas, ML para patrones en volúmenes altos de datos.

## Detección activa vs. pasiva

- **Pasiva**: la organización recibe la notificación del incidente — observación de personal interno, socios externos, alertas automáticas. Postura reactiva, con tiempos de detección más largos.
- **Activa (*threat hunting*)**: búsqueda proactiva de EOIs en el entorno. Reduce de forma significativa el MTTD. El capítulo enfatiza que una detección más rápida típicamente se correlaciona con menor impacto del incidente.

## La "tiranía de la elección infinita"

Lo que distingue IR de *threat hunting*: la respuesta a incidentes arranca con un indicador definido (sonó una alerta, un usuario reportó algo). El *hunting* no — el analista enfrenta millones de entradas de log en miles de sistemas sin ninguna anomalía evidente, lo que obliga a priorizar entre posibilidades de investigación prácticamente infinitas. El término —citado del investigador Faan Rossouw— es "the tyranny of infinite choice".

**Pyramid of Pain**: marco para resolver esa parálisis, ordenando los artefactos del adversario según cuánto "dolor" le cuesta cambiarlos:
- Nivel inferior (trivial de cambiar): hashes, direcciones IP.
- Niveles medios (cada vez más costoso cambiar): dominios, artefactos de red, artefactos de host, herramientas.
- Nivel superior (operacionalmente costoso de cambiar): TTPs (tácticas, técnicas y procedimientos).

El consejo del capítulo es subir en la pirámide hacia indicadores de comportamiento — patrones de *beaconing* que sugieren comunicación con C2, cadenas sospechosas de creación de procesos, técnicas de movimiento lateral que exponen el *procedimiento* real del adversario, no solo su herramienta del momento.

## Líneas base por unidad de negocio

Una organización grande no puede aplicar una sola línea base global de forma efectiva. El ejemplo del capítulo es un contratista de defensa: la división de aeronáutica genera transferencias CAD/CAM pesadas, los sistemas de misión operan en redes clasificadas con conectividad externa mínima, y IT corporativo corre aplicaciones de negocio estándar. Una línea base unificada terminaría marcando transferencias de investigación rutinarias como anómalas, o directamente no detectando un acceso inusual en el entorno más sensible. La solución: acotar las líneas base a unidades de negocio o grupos funcionales, lo que produce definiciones más ajustadas de "normal" y reduce falsos positivos.

## Human-in-the-loop (HITL) en detección por ML

Advertencia central: no tratar la salida de un modelo de ML como una determinación definitiva. Un programa de detección efectivo usa ML para exponer señales de alta prioridad para revisión humana — aprovechando el contexto que el analista tiene y el modelo no (cambios organizacionales, proyectos en curso, experiencia investigativa). Los flujos HITL crean un loop de feedback: las decisiones del analista sobre eventos marcados se convierten en datos etiquetados para reentrenar el modelo.

## Fuentes de datos de detección

**EDR (Endpoint Detection and Response)**: visibilidad a nivel de host — revela patrones de ataque complejos (inyección de procesos, *credential dumping*, despliegue de mecanismos de persistencia, relaciones padre-hijo de procesos sospechosas). El capítulo nombra **SentinelOne** como ejemplo de plataforma EDR que integra detección, alertas y *hunting* en un dashboard, usualmente conectado a SIEM y SOAR.

**Entornos cloud-native**: el capítulo los menciona pero remite a guías específicas de plataforma para el detalle de implementación — está fuera del alcance de esta sección del libro.

## MITRE ATT&CK

La lógica de detección mapea cada vez más las TTPs del atacante al framework MITRE ATT&CK. Al enfocarse en comportamientos del adversario en vez de en indicadores puntuales, las reglas de detección siguen siendo efectivas aunque el atacante cambie de herramienta.

## Herramientas y tecnologías nombradas

SentinelOne (EDR) · SIEM y SOAR (integración de detección, reporte y orquestación) · Sigma rules (mencionadas como metodología de detección, sin desarrollo detallado en esta sección) · MITRE ATT&CK.

## Advertencias

- Depender solo de detección basada en firmas implica, casi con certeza, perderse amenazas nuevas.
- La detección basada en comportamiento requiere calibración cuidadosa de la línea base; cambios organizacionales pueden degradar esa precisión con el tiempo.
- ML: drift por evolución de las técnicas del atacante y del entorno; contaminación de datos de entrenamiento con ejemplos mal etiquetados; ataques de evasión que explotan debilidades del modelo.
- La capacidad de *hunting* es limitada: el analista tiene que priorizar hipótesis de alto impacto (TTPs) por sobre indicadores de bajo nivel (hashes, IPs) precisamente porque esos indicadores son los más fáciles de cambiar para el atacante.

## Relación con otros capítulos

Depende directamente de las decisiones tomadas en Prepare (qué infraestructura de detección se desplegó y cómo se configuró). El capítulo remite explícitamente a secciones posteriores "Detect: Step-by-Step" y "Detect Activity Examples" (procedimiento operativo concreto, cubierto en el anexo oficial correspondiente).

## Preguntas de estudio

1. Tomá un indicador que uses hoy para detectar (hash, IP, dominio, TTP) y ubicalo en la Pyramid of Pain. ¿Qué tan arriba está?
2. ¿Tu organización tiene una sola línea base o líneas base por unidad de negocio? Si es una sola, ¿qué falso positivo o falso negativo típico genera?
3. Describí un flujo HITL concreto para un alerta de ML que recibas hoy: ¿quién revisa, qué decide, cómo vuelve esa decisión al modelo?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Detect Activity". CC BY 4.0. https://dynamicincidentresponse.com/chapters/detect.html
