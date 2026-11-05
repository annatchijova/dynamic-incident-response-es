# Análisis crítico: DAIR vs. PICERL / NIST SP 800-61 / NIST CSF 2.0

**Nota de encuadre**: este análisis es una observación propia, separada del contenido del autor. DAIR es el framework propuesto por Joshua Wright en este libro — no es un estándar universal, no tiene el mismo estatus institucional que NIST SP 800-61 o PICERL, y no fue sometido (hasta donde esta guía puede verificar) al mismo proceso de revisión pública que un documento NIST. Tratarlo como "el" estándar de la industria sería un error de categoría.

## 1. Qué coincide

- **Las cuatro/seis fases centrales son las mismas**, solo organizadas distinto. Preparación, detección/identificación, contención-erradicación-recuperación, y revisión posterior aparecen en los cuatro marcos (PICERL, NIST SP 800-61 Rev. 2, NIST CSF 2.0, DAIR). Ver [03-modelos-existentes.md](capitulos/03-modelos-existentes.md) y [04-dair-modelo.md](capitulos/04-dair-modelo.md).
- **Los cuatro reconocen que la preparación es la base**, aunque la midan distinto (PICERL y DAIR la tratan como fase/waypoint; CSF 2.0 la distribuye en Govern+Protect).
- **DAIR y NIST SP 800-61 Rev. 3 comparten la idea de integrar la IR con la gestión de riesgo organizacional** — ambos alejan la IR de ser un proceso puramente técnico aislado. DAIR formaliza esto con la capa de "coordinación con decision-makers"; CSF 2.0 lo hace distribuyendo la IR entre sus seis funciones. Ver [14-integracion-csf.md](capitulos/14-integracion-csf.md).

## 2. Qué aporta DAIR que los otros no tienen (según el propio libro)

- **Un ciclo explícito con disparadores nombrados.** PICERL y NIST SP 800-61 Rev. 2 permiten iteración en la práctica, pero no la documentan como parte formal del modelo — por eso el libro los acusa de "linealidad artificial". DAIR nombra los cinco disparadores de re-entrada (IOC nuevo, expansión de alcance, erradicación incompleta, revelación de evidencia, cambio de prioridad de negocio) como parte constitutiva del modelo, no como excepción. Esto es un aporte real de **organización explícita**, no necesariamente de contenido nuevo: cualquier respondedor experimentado ya "sabe" que a veces hay que volver a Scope — DAIR le pone nombre y procedimiento a esa intuición.
- **Verify and Triage como waypoint separado de Detect.** NIST SP 800-61 funde detección y análisis en una sola fase. DAIR separa "detectar un EOI" de "confirmar que es un incidente real y priorizarlo" — una distinción útil operativamente, en particular para organizaciones con alto volumen de falsos positivos.
- **La capa de "coordinación con decision-makers" como elemento persistente, no puntual.** Es el aporte más distintivo del libro: convierte algo que en otros marcos aparece disperso (comunicación a stakeholders, aprobación de contención) en una capa explícita que envuelve todo el proceso.

## 3. Qué es simplificación retórica, no aporte real

- **La crítica a PICERL como "modelo lineal" es parcialmente una caricatura.** El propio PICERL incluye "Lessons Learned" que retroalimenta "Preparation" — es decir, PICERL ya es cíclico a nivel macro (entre incidentes), aunque no lo sea explícitamente *dentro* de un mismo incidente. DAIR ataca sobre todo la linealidad *intra-incidente*, que es un blanco más preciso — pero el libro a veces habla de "modelos lineales" en general, sin esa distinción, lo cual sobre-simplifica el objetivo real de la crítica.
- **DAIR no resuelve, solo nombra, varias de las tensiones que señala en NIST Rev. 2** — por ejemplo, "falta de guía específica de recuperación" (ver [03-modelos-existentes.md](capitulos/03-modelos-existentes.md)). El propio capítulo "Recover" de DAIR ([12-recover.md](capitulos/12-recover.md)) sí da un checklist de 9 pasos, que es más específico que NIST — en esto el aporte es real y verificable, no solo retórico.

## 4. Limitaciones del propio DAIR que el libro no discute a fondo

- **Costo de coordinación**: la capa de "decision-maker coordination" asume que la organización ya tiene decision-makers disponibles, informados y con autoridad clara en el momento del incidente — exactamente la misma precondición que Prepare ([05-prepare.md](capitulos/05-prepare.md)) reconoce como difícil de lograr ("paradoja de la preparación"). El modelo no resuelve ese problema, lo traslada a Prepare.
- **Sin aval institucional externo**: a diferencia de NIST SP 800-61 (sometido a revisión pública y adoptado por agencias federales), DAIR es un modelo de autor, publicado por SANS/autoeditado. Eso no lo invalida — pero una organización que necesita demostrar cumplimiento regulatorio específico ("usamos un marco reconocido") probablemente siga necesitando mapear DAIR hacia NIST CSF 2.0 para fines de auditoría, que es justamente lo que el capítulo de integración ([14-integracion-csf.md](capitulos/14-integracion-csf.md)) hace explícito — DAIR se apoya en la autoridad de NIST, no la reemplaza.
- **La crítica a "linealidad" de PICERL podría aplicarse en parte al propio DAIR**: los cinco waypoints (Prepare→Detect→Verify/Triage→Response Actions Loop→Debrief) siguen teniendo un orden macro bastante lineal — la no-linealidad real de DAIR vive *adentro* del Response Actions Loop, no en la estructura completa del modelo. Es una distinción importante que el libro no siempre deja clara cuando promociona DAIR como "no lineal" sin más calificación.

## 5. Afirmaciones del libro que requieren verificación externa

- Las cifras del capítulo de ransomware (USD 820 millones en pagos on-chain en 2025, tasa de pago por debajo del 30%, atribuidas al "Chainalysis 2026 Crypto Crime Report") no se verificaron de forma independiente en esta guía — provienen de una fuente citada por el libro, no confirmada directamente contra el reporte original.
- Las estadísticas de Google Threat Horizons y Mandiant M-Trends 2025 citadas en el capítulo de cloud (47,1% credenciales débiles, 66% robo de datos en compromisos cloud) tampoco se verificaron contra el reporte fuente — se transcriben acá como "lo que el libro afirma que dicen esos reportes", no como hecho confirmado de forma independiente.
- El caso Stryker (marzo de 2026, Handala/Void Manticore, +200.000 dispositivos borrados) es reciente respecto de la fecha de esta guía — vale la pena contrastarlo contra cobertura periodística independiente antes de citarlo como ejemplo en un contexto profesional.

## Conclusión

DAIR es una reorganización útil y bien argumentada de prácticas ya existentes en la industria, con dos aportes genuinamente nuevos (la formalización del ciclo con disparadores nombrados, y la capa persistente de coordinación con decision-makers). No es un reemplazo de NIST CSF 2.0 para fines de cumplimiento — es, como el propio capítulo de integración reconoce, una capa operativa que se mapea *hacia* NIST para ese propósito. Tratarlo como un estándar de la industria al mismo nivel que NIST sería, en este momento, una sobre-extensión de su estatus real.
