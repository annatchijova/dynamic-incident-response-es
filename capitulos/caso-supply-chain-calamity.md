# Caso de estudio: Supply Chain Calamity

> Guía de estudio en español — síntesis propia, no traducción. Basado en el caso de estudio inicial de *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/supplychaincalamity.html

## Función del caso

Narrativa de apertura del libro: un compromiso de cadena de suministro a nivel de SDK, pensado para instalar en el lector la sensación de "esto puede pasar en cualquier integración de proveedor legacy", antes de entrar en teoría.

## Actores

- **Jordan** — arquitecta de soluciones cloud en NovaRise, responsable de infraestructura backend e integraciones de terceros.
- **Pyrix** — actor de amenaza que compromete al proveedor del SDK e inserta malware stealer en la distribución.
- **Sam** — mencionado en el índice del libro, sin detalle sustancial en esta sección.

## Qué pasa (resumen, no reproducción línea por línea)

La jornada de Jordan arranca con problemas de MFA y un standup apurado sobre integrar a Gilded Freight, un proveedor logístico legacy. Al intentar levantar un contenedor Docker en el puerto 8080, aparece un error de binding. Al investigar, encuentra dos procesos inesperados que vienen de la instalación del SDK de Gilded: `ms`, escuchando en `127.0.0.1:8080`, y `ssupd`, escuchando en `0.0.0.0:9150`.

**Cómo comprometió Pyrix el SDK**: acceso VPN vía *credential stuffing*, explotación de vulnerabilidades en Jenkins para llegar a los repositorios fuente, e inserción de bash ofuscado en el script instalador. Ese script agrega dos componentes maliciosos:

- **MiniServe**: un servidor web mínimo que expone el sistema de archivos como raíz web.
- **Un cliente Tor renombrado como `ssupd`**: acceso remoto anónimo.

El script avisaba al C2 de Pyrix vía Tor, usando `curl` con proxy SOCKS5. El detalle crítico: el listener SOCKS de Tor estaba *bindeado a todas las interfaces* (`0.0.0.0`), no solo a localhost — eso es lo que le permitía a Pyrix pivotar desde la estación de trabajo comprometida hacia la red interna.

## La decisión de Jordan

Al reconocer la actividad sospechosa, Jordan mata los tres procesos relacionados y borra todo el directorio `/opt/gilded/`, sin escalar formalmente pese a la presión de tiempo de los project managers — pragmatismo por encima del procedimiento.

## Función pedagógica

El caso muestra en carne propia varias ideas que el libro va a formalizar después:

- Un mecanismo de persistencia puede correr en silencio sin que el desarrollador lo note.
- Una integración de proveedor legacy es, en sí misma, superficie de ataque.
- Una ofuscación simple (del tipo `bash-obfuscate`) alcanza para pasar una inspección casual.
- La elección de *binding* de red (`127.0.0.1` vs `0.0.0.0`) determina directamente el alcance real de un compromiso: un mismo malware es mucho menos peligroso en localhost que en todas las interfaces.

## Lección implícita (la que retoma el resto del libro)

Contención inmediata por encima de atribución exhaustiva. La reacción rápida de Jordan evitó exfiltración adicional, a costa de un análisis forense más profundo que nunca se hizo — exactamente el patrón de "erradicación sin *scoping*" que el capítulo "Introduction" usa como advertencia (ver [00-introduccion.md](00-introduccion.md), donde este mismo patrón reaparece bajo el nombre NovaRise/Pyrix con consecuencias peores: ahí la contención incompleta permite exfiltración vía AWS).

## Relación con otros capítulos

Funciona como el ancla narrativa para todo el libro: DAIR, presentado más adelante, está diseñado explícitamente para responder sin información perfecta, tratando la respuesta como iterativa y no como un ejercicio forense completo desde el primer momento.

## Preguntas de estudio

1. Si Jordan hubiera escalado formalmente antes de borrar `/opt/gilded/`, ¿qué evidencia se hubiera preservado que ahora se perdió?
2. ¿Qué hubiera revelado un *scoping* posterior sobre si Pyrix ya había pivotado a otras estaciones antes de que Jordan actuara?
3. Comparando este caso con el de NovaRise (capítulo "Introduction"): en ambos hay contención sin verificación de alcance. ¿Qué variable explica que acá el daño quede acotado y en NovaRise no?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Caso de estudio "Supply Chain Calamity". CC BY 4.0. https://dynamicincidentresponse.com/chapters/supplychaincalamity.html
