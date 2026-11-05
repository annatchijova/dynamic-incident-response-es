# Contain

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Contain Activity", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/contain.html — ver también el anexo oficial [step-by-step-contain.md](../anexos/step-by-step-contain.md).

## Propósito

La transición crítica de entender el incidente (Scope) a actuar defensivamente. La contención tiene un doble objetivo: frenar al atacante antes de que cause más daño, *y* preservar evidencia para la investigación. Ese balance entre acción agresiva y preservación cuidadosa exige tanto sofisticación técnica como pensamiento estratégico.

## Objetivos de la contención

1. **Frenar la actividad del atacante**: aislamiento de red, restricción de cuentas, terminación de procesos — sin alertar a un adversario sofisticado que, al detectar la medida defensiva, puede acelerar su cronograma.
2. **Recolección y preservación de evidencia**: capturar datos volátiles antes de que se pierdan, priorizando por velocidad de degradación. La adquisición de memoria, en particular, captura datos volátiles que se perderían si el sistema se apaga o reinicia.

## Estrategias de contención (espectro)

- **Pasiva**: limitar el daño sin alertar al atacante de que hay acciones defensivas en curso — vía monitoreo y tecnologías de engaño como honeypots.
- **Activa**: acción decisiva para frenar al atacante, aceptando que puede darse cuenta.
- **Adaptativa**: transición entre pasiva y activa según evoluciona la inteligencia sobre la amenaza.

## Procedimientos y métodos

**Aislamiento de red y sistema**: segmentación vía reglas de firewall, listas de control de acceso, y desconexión física cuando los controles de software fallan. El aislamiento a nivel sistema remueve el equipo comprometido de la red manteniendo integridad forense y acceso de gestión para la investigación — el capítulo recomienda preferir las funciones de aislamiento del EDR por sobre controles basados puramente en red.

**Gestión de credenciales**: deshabilitar o limitar cuentas comprometidas, idealmente sin alertar al atacante. Coordinar el reseteo de credenciales con cuidado para no disparar la detección del atacante mientras se logra la contención.

**Control de procesos y servicios**: la terminación de procesos frena operaciones maliciosas identificadas, pero exige cautela — adversarios avanzados pueden implementar procesos *watchdog* que reinician el malware terminado, y se han observado grupos de ransomware acelerando el cronograma de cifrado al detectar acciones defensivas. La disrupción de servicios exige coordinación con stakeholders para entender el impacto operativo.

**Preservación de evidencia**:
- Adquisición de memoria con herramientas como **WinPMEM** y **Linpmem**, que permiten una captura rápida con impacto mínimo en el sistema.
- Imaging forense selectivo de sistemas críticos o directorios específicos, valioso para investigación detallada.
- Reenvío inmediato de logs a una ubicación centralizada y segura apenas se descubre el compromiso, para evitar que el atacante borre o modifique los logs locales.

## Marco de decisión: terminar vs. monitorear

El capítulo presenta una tabla comparativa de factores:

- **Favorecen terminación inmediata**: destrucción activa de datos en curso, datos regulados con plazos de cumplimiento, sistemas críticos de seguridad en riesgo.
- **Favorecen monitoreo extendido**: *dwell time* extendido con monitoreo maduro, entornos de engaño controlados.
- **Favorecen un enfoque mixto**: alcance desconocido y sofisticación incierta del atacante.

Punto central: estas decisiones deben guiarse por **criterios acordados de antemano**, no por el criterio del momento bajo presión.

## Herramientas y tecnologías nombradas

WinPMEM y Linpmem (adquisición de memoria) · EDR (aislamiento de sistema manteniendo conexión forense) · **Microsoft Intune** (MDM, mencionado en el caso Stryker) · VLANs privadas, listas de control de acceso, security groups cloud · *software-defined networking* para restringir el movimiento del atacante · honeypots y tecnologías de engaño.

## Caso real citado: el compromiso de Stryker (marzo de 2026)

El capítulo describe el ataque de marzo de 2026 contra Stryker: atacantes comprometieron el entorno Microsoft Intune de la empresa y lo usaron para borrar remotamente dispositivos en toda la organización — laptops, teléfonos y otros endpoints inscriptos en la plataforma. El grupo (identificado como Handala/Void Manticore) habría borrado más de 200.000 servidores, dispositivos móviles y otros sistemas, forzando cierres en 79 países. La respuesta de Stryker incluyó instruir a los empleados a desconectarse de la red y remover por completo los perfiles de gestión de dispositivo — un ejemplo de contención reactiva bajo condiciones extremas.

## Advertencias críticas

- **Riesgos de una contención agresiva**: grupos de ransomware operados por humanos han acelerado el cronograma de cifrado al detectar acciones defensivas; procesos *watchdog* pueden reiniciar malware terminado o disparar payloads destructivos.
- **La contención pasiva es poco común en incidentes modernos**: atacantes capaces detectan rápido el monitoreo defensivo, y o bien aceleran su cronograma o queman deliberadamente su acceso.
- **Trade-offs operativos**: la disrupción de servicio debe balancear necesidad de seguridad contra continuidad de negocio; la terminación inmediata puede dañar la capacidad de investigación.

## Relación con otros capítulos

Las decisiones de contención dependen de lo que ya se entendió en Scope ([09-scope.md](09-scope.md)). La evidencia recolectada durante la contención se usa después, durante Eradicate ([11-eradicate.md](11-eradicate.md)), para entender las TTPs del atacante, y potencialmente para sostener una acción legal futura. El capítulo insiste en que la contención no es un ejercicio puramente técnico: exige coordinación con stakeholders de negocio, comprensión de la tolerancia al riesgo organizacional, y decisiones probabilísticas bajo incertidumbre, con información incompleta.

## Preguntas de estudio

1. En el caso Stryker, ¿qué hubiera cambiado si la contención agresiva (borrado remoto por parte del atacante) no hubiera sido posible porque Intune tenía segmentación de privilegios más estricta?
2. Armá tu propia tabla de "terminar vs. monitorear" para un escenario de tu organización, antes de que ocurra — ¿quién la aprueba?
3. ¿Qué tan preparado está tu entorno para reenviar logs a una ubicación centralizada *antes* de que el atacante pueda borrarlos localmente?

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Contain Activity". CC BY 4.0. https://dynamicincidentresponse.com/chapters/contain.html
