# Índice de herramientas y técnicas

Herramientas, plataformas, protocolos y estándares mencionados en el libro, organizados por capítulo de esta guía.

## Detección y threat hunting ([06-detect.md](capitulos/06-detect.md))
- **SentinelOne** — plataforma EDR con hunting y dashboard integrado.
- **SIEM / SOAR** — integración genérica de detección, reporte y orquestación.
- **Sigma rules** — formato de reglas de detección (mencionado sin desarrollo).
- **MITRE ATT&CK** — framework de mapeo de TTPs del adversario.
- **Pyramid of Pain** — marco de priorización de indicadores (Faan Rossouw, citado en el capítulo).

## Verificación / CTI ([07-verify-triage.md](capitulos/07-verify-triage.md))
- **VirusTotal** — base de reputación multi-vendor.
- **AlienVault OTX** — plataforma comunitaria de inteligencia de amenazas.
- **Shodan** — motor de búsqueda de dispositivos conectados a internet.

## Scope ([09-scope.md](capitulos/09-scope.md))
- SIEM / sistemas de agregación de logs / EDR (hunting a nivel empresa).
- **Dragos**, **Malcolm** (Idaho National Laboratory), **Zeek + ICSNPP** — específicas de entornos OT.
- APIs de proveedor cloud, herramientas de seguridad de runtime de contenedores, logging cloud-native.

## Contain ([10-contain.md](capitulos/10-contain.md))
- **WinPMEM**, **Linpmem** — adquisición de memoria.
- **EDR** — aislamiento de sistema con preservación de conexión forense.
- **Microsoft Intune** — MDM, mencionado en el caso Stryker (también como vector de ataque cuando se compromete).
- VLANs privadas, listas de control de acceso, security groups cloud, SDN (software-defined networking).
- Honeypots / tecnologías de engaño.

## IA en IR ([15-ir-con-ia.md](capitulos/15-ir-con-ia.md))
- **OpenAI, Anthropic, Google, Microsoft** — modelos comerciales de frontera.
- **DeepSeek, Llama (Meta), Phi (Microsoft)** — modelos de pesos abiertos.
- **RFC 5737** (rangos de documentación) y **RFC 1918** (rangos privados) — para sanitización de datos.
- **Git** — versionado de librerías de prompts.
- **Model Context Protocol (MCP)** — integración de workflow avanzada.

## Ransomware ([16-ir-ransomware.md](capitulos/16-ir-ransomware.md))
- **ScreenConnect, AnyDesk, TeamViewer** — herramientas legítimas abusadas como infraestructura de ataque.
- **VMware ESXi** — hipervisor, objetivo prioritario.
- **Chainalysis 2026 Crypto Crime Report** — fuente de inteligencia sobre flujos de pago.
- Panel de afiliados de **LockBit** (filtración de mayo 2025) — ejemplo real de infraestructura RaaS.

## Cloud ([17-ir-cloud.md](capitulos/17-ir-cloud.md))
- **Amazon GuardDuty** — detección gestionada, escaneo de malware sin agente.
- **Azure Microsoft Defender for Cloud** — monitoreo y alertas.
- **Azure Entra ID** — identidad y acceso; logs de auditoría/sign-in.
- **Azure PIM**, **AWS IAM Identity Center**, **Google Cloud IAM Conditions** — elevación just-in-time.
- **Snapshots EBS** — preservación de evidencia forense.
- Policies gestionadas: **AWS SecurityAudit**, **Azure Security Reader**, **Google Cloud Security Reviewer**.

## OT ([18-ir-ot.md](capitulos/18-ir-ot.md))
- **Protocolos**: Modbus, DNP3, EtherNet/IP, PROFINET, ICCP.
- **Estándares**: ISA/IEC 62443, ISA-95.
- **Activos típicos**: HMIs, estaciones de ingeniería, historians, servidores SCADA, RTUs, relés de protección.

## Prepare ([05-prepare.md](capitulos/05-prepare.md))
- Matrices RACI.
- CISA severity levels (árbol de decisión).
- Matriz de priorización tipo InvGate (3×3 urgencia/impacto).

## Marcos y estándares transversales
- **PICERL** (Schultz, 1990) — ver [01-historia-ir.md](capitulos/01-historia-ir.md) y [03-modelos-existentes.md](capitulos/03-modelos-existentes.md).
- **NIST SP 800-61** (Rev. 2 y Rev. 3) — ver [03-modelos-existentes.md](capitulos/03-modelos-existentes.md).
- **NIST CSF 2.0** — ver [14-integracion-csf.md](capitulos/14-integracion-csf.md).
- **DORA (Digital Operational Resilience Act)** — mencionado en [08-response-actions-loop.md](capitulos/08-response-actions-loop.md).
- **NIS2** — mencionado en [05-prepare.md](capitulos/05-prepare.md).

## Nota de cobertura

Este índice recoge lo nombrado explícitamente en las secciones del libro cubiertas por esta guía (ver [registro-cobertura.md](registro-cobertura.md)). No incluye herramientas que puedan aparecer en secciones del libro no cubiertas en esta síntesis (p. ej. sub-secciones extensas de "Accelerating Incident Response with AI" sobre casos de uso intermedios/avanzados, remitidas pero no desarrolladas en detalle acá).
