# Documento de Diseño Técnico (DTI) - Borrador

## §0. Metadatos
* **Sistema:** Talento Digital (Portal Integral de RRHH)
* **Autores:** Daniel Ojalvo Canedo
* **Fecha:** Mayo 2026
* **Estado:** Borrador inicial
* **Propósito:** Definir la arquitectura de alto nivel y las decisiones técnicas para la plataforma de reclutamiento y capacitación de Colquechaca Mining.

---

## §1. Contexto Arquitectónico (C4 Nivel 1)

El sistema "Talento Digital" actúa como el núcleo central para la gestión del talento. Se aísla de la nómina y pagos (que seguirán en el ERP actual), pero debe comunicarse con proveedores externos para la emisión de correos y catálogos de cursos.

### Diagrama de Contexto (C4 Nivel 1)

```mermaid
flowchart TD
    %% Estilos C4
    classDef person fill:#08427b,color:#fff,stroke:#052e56,stroke-width:2px,rx:5px,ry:5px
    classDef system fill:#1168bd,color:#fff,stroke:#0b4884,stroke-width:2px,rx:5px,ry:5px
    classDef external fill:#999999,color:#fff,stroke:#6b6b6b,stroke-width:2px,rx:5px,ry:5px

    %% Personas
    empleado["👤 Empleado / Candidato\n[Persona]\n\nPostula a vacantes, rinde\nexámenes y ve su plan de carrera."]:::person
    rrhh["👤 Especialista RRHH\n[Persona]\n\nAdministra el ciclo de vida del\ntalento y genera reportes."]:::person
    jefe["👤 Jefatura Operativa\n[Persona]\n\nValida perfiles técnicos y\nsolicita ascensos para su equipo."]:::person

    %% Sistema Central
    talento_digital["💻 Sistema Talento Digital\n[Sistema de Software]\n\nPlataforma central para gestión\nde talento, capacitación y méritos."]:::system

    %% Sistemas Externos
    erp["🗄️ ERP Colquechaca\n[Sistema Externo]\n\nFuente maestra de datos de\nempleados y estructura orgánica."]:::external
    smtp["✉️ Servidor SMTP\n[Sistema Externo]\n\nEnvía alertas de vacantes y\nnotificaciones de resultados."]:::external
    auth["🔐 Active Directory / LDAP\n[Sistema Externo]\n\nGestión de identidades y acceso\núnico (SSO) para empleados."]:::external

    %% Relaciones
    empleado -- "Consulta y postula" ---> talento_digital
    rrhh -- "Gestiona y supervisa" ---> talento_digital
    jefe -- "Aprueba y valida" ---> talento_digital

    talento_digital -- "Sincroniza datos de" ---> erp
    talento_digital -- "Notifica vía" ---> smtp
    talento_digital -- "Autentica usuarios con" ---> auth