# Introducción

> Guía de estudio en español — **no** es traducción del capítulo. Es una síntesis técnica propia, en mis palabras, basada en el capítulo "Introduction" de *Dynamic Incident Response: A Framework for Security Teams* de Joshua Wright. Obra original bajo **CC BY 4.0**: https://dynamicincidentresponse.com/ · Fuente de este capítulo: https://dynamicincidentresponse.com/chapters/introduction.html

## Tesis

La calidad de la respuesta a un incidente depende más de la calidad de las decisiones tomadas bajo presión que de la sofisticación de las herramientas o la complejidad del ataque. El libro no busca entregar un guion rígido sino desarrollar criterio (*judgment*) para adaptar la respuesta a las circunstancias particulares de cada incidente.

## Conceptos clave

- **Incidente (*incident*)**: evento adverso en un sistema de información o red — o la amenaza de tal evento — que implica daño o intento de daño.
- **Interdicción de la cadena de suministro (*supply chain interdiction*)**: riesgo que surge de integrar código, librerías, paquetes, frameworks o SDKs de terceros en el desarrollo de software propio.
- **TTPs (Tactics, Techniques, and Procedures)**: marco de referencia para catalogar el comportamiento de atacantes y preparar la organización frente a su evolución.

## Estructura del argumento

1. **La calidad de las decisiones determina el resultado.** El capítulo abre mostrando que un *scoping* incompleto, una contención mal cronometrada o demasiado estrecha, una erradicación apurada, o fallas de comunicación empeoran directamente el incidente. Un ejemplo puntual: actuar en contención demasiado pronto o de forma demasiado acotada puede revelar al atacante que fue detectado.
2. **Los modelos tradicionales (lineales) no alcanzan.** Un modelo que omite pasos iterativos de *scoping* y verificación tiende a producir respuestas incompletas — se investiga a fondo un síntoma puntual (p. ej. una estación de trabajo) sin disparar la pregunta de alcance más amplio que hubiera revelado un compromiso organizacional completo.
3. **Las exigencias actuales piden un enfoque adaptativo.** El capítulo enumera unos diez factores que elevan la exigencia sobre la respuesta a incidentes hoy (ver abajo).

## Caso ilustrativo: NovaRise (resumen, no reproducción)

El libro presenta un caso narrativo para fijar el argumento: un desarrollador ("Jordan") en la empresa ficticia NovaRise detecta listeners no documentados y código ofuscado en un SDK de un proveedor ("Gilded Freight"). Jordan mata los procesos sospechosos y remueve el SDK — una respuesta de contención/erradicación insuficiente porque no incluyó verificación de alcance. Un actor de amenaza ("Pyrix") ya había usado credenciales y claves SSH robadas para moverse lateralmente, pivotar hacia AWS y exfiltrar datos de clientes y algoritmos propios. La investigación posterior nunca dispara el *scoping* más amplio que hubiera revelado la extensión real del compromiso.

**Función pedagógica del caso:** mostrar en forma concreta por qué contención/erradicación sin verificación y *scoping* iterativos es la falla sistemática que el libro busca corregir con DAIR (ver capítulo "A Dynamic Approach to Incident Response").

## Responsabilidades del respondedor (según el capítulo)

- Observar, orientar, detectar y actuar (eco directo del ciclo OODA de Boyd — desarrollado en el capítulo de modelo DAIR).
- Aplicar triage, verificación, *scoping*, contención, erradicación y recuperación.
- Revisar las acciones tomadas antes y durante el incidente.
- Usar métricas para evaluar la efectividad de la respuesta.
- Aplicar lecciones aprendidas.

Cada uno de estos puntos se desarrolla en capítulos posteriores dedicados, con secciones "Step-by-Step" que traducen el concepto en procedimiento accionable.

## Factores que elevan la exigencia sobre IR moderno

- Mayor dependencia digital → mayor severidad de los incidentes.
- Aumento en complejidad y volumen de amenazas (de malware simple a actores estado-nación).
- Obligaciones regulatorias de protección de datos y notificación de brechas.
- Participación esperada en intercambio de inteligencia de amenazas.
- Sofisticación creciente de ransomware y extorsión.
- Riesgo de nube y terceros: configuraciones erróneas, modelo de responsabilidad compartida.
- Desafíos de seguridad del trabajo remoto.
- Expectativas de rendición de cuentas ante stakeholders.
- Adopción de SIEM/XDR/SOAR para identificación rápida.
- Ataques automatizados/asistidos por IA que requieren detección y respuesta no convencionales.

## Herramientas y tecnologías nombradas

SDK (Software Development Kit) · SIEM (Security Information and Event Management) · XDR (Extended Detection and Response) · SOAR (Security Orchestration, Automation, and Response) · AWS (como entorno cloud en el caso NovaRise).

## Límites explícitos que el propio libro declara

- No pretende ser una guía exhaustiva de herramientas de recolección y análisis forense de evidencia.
- No es un tratado de gestión estratégica de incidentes (nivel ejecutivo/negocio), sino un libro operativo para quien responde.
- Advierte que la respuesta efectiva exige aprendizaje continuo, tolerancia a la incertidumbre y resiliencia para sostener el foco cuando el resultado no está completamente bajo control del respondedor.

## Relación con otros capítulos

- Precedido por el caso de estudio "Supply Chain Calamity".
- Sigue "A Short History of Incident Response" (ver [01-historia-ir.md](01-historia-ir.md)), que traza el origen de los modelos formales que este capítulo cuestiona.
- Los capítulos de la Parte 2 (Prepare → Debrief) son el desarrollo operativo punto por punto de la lista de responsabilidades enumerada arriba.

## Preguntas de estudio

1. ¿Por qué una contención demasiado temprana o demasiado acotada puede ser contraproducente? Dar un ejemplo distinto al de NovaRise.
2. En el caso NovaRise, ¿qué paso faltó entre "erradicación" y "cierre del incidente" que hubiera revelado el compromiso real?
3. De los diez factores que elevan la exigencia sobre IR, ¿cuáles aplican directamente a tu organización y cuáles no?

## Referencia de origen

Dynamic Incident Response, Joshua Wright (SANS Institute / autoeditado), capítulo "Introduction". CC BY 4.0. https://dynamicincidentresponse.com/chapters/introduction.html
