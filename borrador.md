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
*(Nota: El siguiente diagrama está en formato Mermaid. Si usas GitHub o un visor Markdown compatible, se renderizará automáticamente como un gráfico).*

```mermaid
C4Context
    title Diagrama de Contexto de Sistema (Nivel 1) - Talento Digital

    Person(empleado, "Empleado / Candidato", "Busca ascender, rinde exámenes y toma cursos.")
    Person(rrhh, "Especialista RRHH", "Gestiona vacantes, revisa casos prácticos y asigna cursos.")

    System(talento_digital, "Sistema Talento Digital", "Plataforma central de reclutamiento, planes de carrera y capacitación.")

    System_Ext(mail_server, "Servidor de Correo (SMTP)", "Envía notificaciones, invitaciones masivas y resultados de exámenes.")
    System_Ext(erp_legacy, "ERP / Sistema Contable", "Provee la base de datos maestra de empleados activos (solo lectura).")
    System_Ext(proveedor_cursos, "API Proveedor E-Learning", "Plataformas como Udemy/Coursera para sincronizar catálogo de cursos externos.")

    Rel(empleado, talento_digital, "Usa para postularse y capacitarse")
    Rel(rrhh, talento_digital, "Usa para gestionar vacantes y talento")
    
    Rel(talento_digital, mail_server, "Envía emails transaccionales usando")
    Rel(talento_digital, erp_legacy, "Consulta empleados activos desde")
    Rel(talento_digital, proveedor_cursos, "Obtiene catálogo de cursos de")