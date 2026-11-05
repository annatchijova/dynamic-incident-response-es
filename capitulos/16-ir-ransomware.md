# Respuesta a incidentes para ransomware

> Guía de estudio en español — síntesis propia, no traducción. Basado en "Incident Response for Ransomware", *Dynamic Incident Response* de Joshua Wright. CC BY 4.0. Fuente: https://dynamicincidentresponse.com/chapters/considerations-ransomware.html

## Tesis

El capítulo complementa DAIR con guía específica para ransomware. El ransomware moderno evolucionó de cifrado simple a operaciones de extorsión multi-etapa que combinan robo de datos con amenaza de cifrado.

## Tipos de ransomware (taxonomía del capítulo)

- **Ransomware operado por humanos (HumOR)**: operadores capacitados hacen reconocimiento, escalada de privilegios y movimiento lateral antes de desplegar el cifrado. La adopción de IA/LLM acelera la sofisticación del ataque mientras baja la barrera técnica para afiliados menos capacitados.
- **Ransomware automatizado/de distribución masiva**: campañas de alto volumen vía adjuntos maliciosos o exploits, se ejecuta de inmediato sin reconocimiento previo. La recuperación suele ser más simple por el alcance limitado del compromiso.
- **Extorsión sin cifrado**: el robo de datos solo ya sirve como palanca de presión, eliminando la complejidad del cifrado — tendencia creciente a medida que los operadores reconocen que la amenaza de exposición alcanza para cobrar el rescate.
- **Pseudo-ransomware / wipers**: aparentan ser ransomware pero no ofrecen ninguna vía real de recuperación — o no tienen clave de descifrado, o usan técnicas destructivas que impiden recuperar el dato aunque se pague.
- **Ransomware-as-a-Service (RaaS)**: el operador mantiene el payload, la infraestructura y la plataforma; los afiliados ejecutan el ataque concreto. El modelo de reparto de ingresos democratiza el ataque para actores de amenaza menos capaces.

## Vectores de ataque y acceso inicial

- **Compromiso de credenciales**: el vector principal, explotando VPN, RDP y servicios de gestión remota. El capítulo nombra el "problema de la credencial no rastreable": una credencial robada por phishing, malware infostealer, o comprada en un mercado clandestino no deja evidencia del lado de la víctima — la organización no puede determinar con confianza ni el origen ni el momento del compromiso.
- **Initial Access Brokers (IABs)**: se especializan en comprometer la red y venden el acceso a afiliados. El tiempo extendido entre compromiso y cifrado (semanas o meses) habilita reconocimiento sofisticado antes de desplegar el payload.
- **Herramientas legítimas como infraestructura de ataque**: ScreenConnect, AnyDesk, TeamViewer se mezclan sin fricción con el uso legítimo de IT, lo que complica distinguirlas de una actividad normal.
- **Objetivos de infraestructura crítica**: hipervisores (VMware ESXi) y sistemas de backup son priorizados para eliminar opciones de recuperación *antes* de desplegar el cifrado.

## Datos financieros y de tendencia (2025, según el capítulo)

Aproximadamente USD 820 millones en pagos on-chain en 2025 (caída del 8% interanual respecto de 2024). Sin embargo, las publicaciones en sitios de filtración de datos subieron 50% interanual (2024-2025), mientras que la tasa real de pago de rescate cayó por debajo del 30% — lo que indica una proliferación de intentos de extorsión pese a una tasa de éxito de cobro en caída.

## Procedimientos específicos de IR para ransomware

**Consideraciones de negociación de extorsión**: negociar solo después de determinar la sensibilidad de los datos y la exposición regulatoria; entender que pagar no garantiza recibir la clave de descifrado ni que el atacante borre los datos; documentar todas las comunicaciones para fuerzas de seguridad y la aseguradora.

**Estrategia de recuperación**: priorizar la evaluación de integridad del sistema de backup antes de que se amplíe la detección del cifrado; determinar el alcance del cifrado para identificar segmentos no cifrados aptos para un reinicio operativo; validar la clave de descifrado antes de la restauración completa, para evitar reinfección.

**Respuesta a extorsión multi-vector**: atender el robo de datos vía notificación de brecha, presentación de cumplimiento regulatorio y monitoreo de crédito, mientras se maneja en paralelo la recuperación del cifrado — el panorama actual exige contención simultánea en múltiples vectores de daño.

## Herramientas y tecnologías nombradas

**Chainalysis 2026 Crypto Crime Report** (inteligencia de amenazas sobre flujos de pago) · base de datos MySQL del panel de afiliados de **LockBit** filtrada en mayo de 2025 (revela la infraestructura operativa de un RaaS real) · ESXi/VMware como objetivo primario · RDP, herramientas RMM, concentradores VPN como vectores de acceso remoto.

## Advertencias y límites

1. **Brecha de atribución de credenciales**: el respondedor puede nunca identificar con certeza cómo se comprometió una credencial, cuando el acceso inicial ocurre fuera de la telemetría organizacional. La recomendación del capítulo es enfocarse en controles que reducen el valor de una credencial robada sin importar cómo se obtuvo: MFA en todas partes, políticas de acceso condicional, gestión de acceso privilegiado.
2. **Vulnerabilidad a Attacker-in-the-Middle (AitM)**: un MFA simple no alcanza — actores de amenaza sofisticados lo evaden con ataques AitM.
3. **Ambigüedad de "es ransomware o es un wiper"**: hay que distinguir entre cifrado real y sabotaje destructivo — un descifrado fallido puede ser sabotaje intencional, no cifrado legítimo mal implementado.
4. **Eficacia del pago**: no hay garantía de que pagar habilite la recuperación — el atacante puede no tener una clave viable, o retenerla a propósito.

## Relación con el resto del framework DAIR

El capítulo aclara que estas son consideraciones de riesgo específicas de ransomware que se superponen al framework general, no un reemplazo de la metodología estándar de IR — remite explícitamente a Prepare, Verify/Triage, Scope, Eradicate, Recover y Debrief (Parte 2 del libro) como el lugar donde vive el procedimiento operativo detallado.

## Preguntas de estudio

1. Ante el "problema de la credencial no rastreable", ¿qué controles de tu organización reducen el *valor* de una credencial robada, más allá de intentar rastrear cómo se robó?
2. Si tu backup más reciente se hizo horas antes de detectar el cifrado, ¿cómo validarías su integridad antes de restaurar?
3. Diseñá un criterio simple para distinguir, en los primeros minutos, si estás frente a ransomware real o frente a un wiper disfrazado de ransomware.

## Referencia de origen

Dynamic Incident Response, Joshua Wright. Capítulo "Incident Response for Ransomware". CC BY 4.0. https://dynamicincidentresponse.com/chapters/considerations-ransomware.html
