# Primeros pasos (Getting Started)

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Getting Started", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/gettingstarted.html

## Propósito

Capítulo de vocabulario fundacional: fija los términos y métricas que el resto del libro da por sabidos, para que un equipo pueda comunicarse sin ambigüedad sobre qué es (y qué no es) un incidente.

## Conceptos definidos

- **Incidente**: evento adverso en un sistema o red, o la amenaza de que ese evento ocurra. Se clasifica en tres tipos:
  - **Malicioso**: acción deliberada de un actor de amenaza (explotación de vulnerabilidad, abuso de credenciales, despliegue de malware).
  - **Accidental**: daño no intencional (borrado de datos, errores de configuración, exposición de credenciales).
  - **Ambiental**: fallas naturales o de infraestructura (cortes de energía, inundaciones, caídas de un proveedor cloud).
- **Evento (*event*)**: cualquier ocurrencia observable en un sistema o red — entradas de log, mensajes de error, tickets de mesa de ayuda, incluso reportes no digitales.
- **Evento de interés (EOI, *Event of Interest*)**: evento que amerita investigación, según criterios de significancia definidos por la organización.
- **MTTD (Mean Time To Detect)**: métrica de velocidad de detección.
- **MTTR (Mean Time To Respond)**: métrica de velocidad de respuesta.

## Estructura del argumento

El capítulo construye en cascada: primero define los componentes atómicos (incidente, evento, EOI) y recién después los integra. Usa la analogía de una "cascada" (*waterfall*) de eventos que fluyen desde la detección hasta la recolección, para dejar claro que sin un mecanismo de filtrado el volumen de eventos desborda la capacidad de cualquier analista.

## Procedimientos descriptos

1. Clasificar eventos por tipo de fuente y contexto.
2. Filtrar EOIs usando criterios propios de la organización.
3. Evaluar el incidente durante una fase de investigación "pre-incidente".
4. Distinguir con claridad entre la declaración formal de un incidente y el inicio de actividades de respuesta — no son lo mismo y no siempre ocurren en ese orden.

## Ejemplos usados

Logs de registro de dispositivo en un firewall Fortinet · errores PHP en un servidor Apache · tickets de soporte por problemas de rendimiento · Windows Event ID 104 (borrado de log del sistema) · logs de autenticación Linux · accesos de administrador a dispositivos de red · cuentas de usuario no reconocidas en sistemas de seguridad.

## Advertencias

No toda organización declara un incidente de inmediato: las obligaciones regulatorias de notificación hacen que muchas operen primero en un "estado investigativo pre-incidente", donde ya hay actividad de respuesta sin que exista todavía una declaración formal. El libro aclara que su foco principal son los incidentes **maliciosos**, aunque los marcos que describe también aplican —con otro énfasis, una vez determinada la causa raíz— a incidentes accidentales y ambientales.

## Relación con otros capítulos

Este vocabulario (incidente/evento/EOI/MTTD/MTTR) es la base terminológica que reaparece sin redefinirse en todo el resto del libro, en particular en "Detect" y "Verify and Triage".

## Preguntas de estudio

1. Pensá un evento real de tu entorno que sea "observable" pero que tu organización nunca clasificaría como EOI. ¿Por qué no?
2. ¿Tu organización mide MTTD y MTTR? Si no, ¿qué tendría que instrumentarse primero?
3. ¿Qué implica operar en "estado investigativo pre-incidente" para las obligaciones de notificación regulatoria que te apliquen?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Getting Started". CC BY 4.0. https://dynamicincidentresponse.com/chapters/gettingstarted.html
