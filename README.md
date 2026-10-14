
# Plan Integral de Seguridad de la Información (Auditoría ISO 27001 / GDPR)

Este repositorio documenta un caso práctico de relevamiento de activos, análisis de riesgos e implementación de controles físicos y lógicos, alineado con los marcos de trabajo ISO/IEC 27001 y los principios de GDPR. El proyecto se gestionó ágilmente mediante metodologías Kanban (simulando el flujo de trabajo original en Trello).

## 🎯 Objetivo
El objetivo principal de esta auditoría fue establecer una línea base de seguridad para una infraestructura corporativa, identificando vulnerabilidades en la gestión de PII (Información de Identificación Personal), segmentación de red y continuidad del negocio, para luego aplicar controles de mitigación (hardening).

## 🛠️ Fases de la Auditoría

### Fase 1: Inventario de Activos (ISO 27001 A.5 y A.8)
Se realizó un relevamiento exhaustivo de la infraestructura para clasificar los activos y determinar la ubicación y uso de datos sensibles.
* **Identificación:** Listado de hardware (Servidores, PCs), software y mapa básico de red.
* **Gestión de PII:** Identificación de listados de datos sensibles, ubicaciones de almacenamiento y flujos de acceso ("Quién usa qué").

### Fase 2: Roles, Accesos y Permisos (GDPR + ISO A.9)
Auditoría de los controles lógicos de acceso y aplicación del principio de Mínimo Privilegio.
* Revisión de roles de usuario, acceso a carpetas compartidas y sistemas críticos.
* Evaluación de la aplicación de políticas de contraseñas y existencia de MFA (Autenticación Multifactor).
* Verificación de la revocación de accesos para ex-empleados.

### Fase 3: Controles Físicos (ISO A.11)
Evaluación de las barreras físicas que protegen los activos críticos.
* Controles de acceso al servidor (Llaves, cámaras) y seguridad de las estaciones de trabajo (PCs bloqueadas, política de escritorio limpio para documentos con datos personales).
* Revisión de condiciones ambientales (Temperatura, UPS).
* Custodia de Evidencia Legal.

### Fase 4: Red y Segmentación (ISO A.13)
Análisis de la topología de red para prevenir movimientos laterales.
* Revisión de VLANs, WiFi protegida y separación administrativa (Usuarios vs. Invitados).
* Análisis de accesos a dispositivos de red (Router/Switch).

### Fase 5: Riesgos sobre PII y Continuidad (ISO A.17)
* **Riesgos PII:** Evaluación del ciclo de vida de los datos personales (almacenamiento, acceso, respaldo, cifrado, transmisión por correo) y elaboración de una Matriz de Riesgos (Probabilidad x Impacto).
* **Continuidad:** Desarrollo de un Plan de Respuesta ante Incidentes (IRP) y Plan de Continuidad de Negocio (BCP) para escenarios como incendios o robos.

## 🛡️ Implementación y Hardening (Resultados)

A partir del relevamiento, se ejecutaron las siguientes acciones de mejora:

* **Hardening del Perímetro:** Se deshabilitaron servicios inseguros (Telnet, FTP, SSH, HTTP), migrando la administración a HTTPS (LAN). Se configuró el firewall en nivel Medium (SPI) y se activó el Modo Sigilo (Stealth) bloqueando respuestas ICMP (Ping) desde la WAN.
* **Segmentación Inalámbrica (Capa 2):** Se implementó Dual-SSID. Una red administrativa (WPA3-SAE) y una red de invitados aislada (AP Isolation activo) para prevenir movimientos laterales. Se implementó Bitwarden para la gestión de credenciales de alta entropía.
* **Protección de Infraestructura Física:** Instalación de estabilizadores de tensión para Gateway y Switch, junto con el tendido de red LAN estructurado.

## 📋 Próximos Pasos (Backlog)
* Ejecutar escaneos con Nmap para mapeo de MAC addresses e implementar MAC Filtering.
* Implementar un SSID dedicado (aislado) para dispositivos IoT (Cámaras/DVR) para mitigar riesgos de vulnerabilidades de hardware de terceros.
* Desplegar un SIEM (Splunk o Syslog server) para la recolección y monitoreo de eventos de red en tiempo real.

## 📊 Informe Ejecutivo y Gestión de Riesgos (C-Level)

Como parte de la auditoría, se elaboró y presentó un **Informe Ejecutivo de Seguridad (Fase 1: Diagnóstico y Hardening)** dirigido a la alta dirección, utilizando como base los marcos ISO 27001, GDPR / Ley 25.326 y NIST CSF.

*(👉 [Ver Informe Ejecutivo PDF en la carpeta /docs](./docs/Caso%20Práctico_%20Auditoría%20ISO%2027001%20y%20Hardening-2.pdf))*

### Puntos Clave del Reporte:
* **Traducción de Riesgos Técnicos a Negocio:** Identificación de hallazgos críticos como la exposición de más de 200 documentos de identidad (PII) en la nube sin cifrar y el uso de endpoints obsoletos (Windows 7).
* **Mapa de Calor de Riesgos:** Clasificación de amenazas (ej. Pérdida de Datos / Ransomware) evaluando el impacto vs. probabilidad.
* **Cultura y Procesos:** Identificación de la resistencia organizacional al uso de MFA y la falta de *sponsorship* directivo como bloqueadores principales para la remediación de la capa de datos.
* **Responsabilidad Legal y Cumplimiento:** Notificación formal a la gerencia sobre el marco legal (Ley 25.326 - Habeas Data), documentando la aceptación del riesgo ("Riesgo Aceptado") por parte del negocio ante la negativa de asignar recursos para backups.
* **Roadmap Estratégico (Fase 2):** Propuesta de remediación priorizada, incluyendo la implementación de copias de seguridad (Regla 3-2-1), higiene de contraseñas (IAM) y cifrado de discos.

### El Tablero Kanban como "Audit Trail"
Toda la gestión operativa documentada en el tablero ágil sirvió como prueba técnica y **descargo de responsabilidad** del auditor, demostrando que las vulnerabilidades fueron identificadas, categorizadas y comunicadas formalmente en tiempo y forma.
