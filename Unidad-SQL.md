---
layout: default
title: "Unidad 3: Oracle SQL"
nav_order: 5
permalink: /Unidad-SQL/
has_children: true
---

# 🗄️ Unidad 3: Gestión de Bases de Datos
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **Modelos y Servicios de Datos (MYSD)** 🎓

{: .note }
> **Resultados de Aprendizaje:** Al finalizar esta unidad, estarás en capacidad de configurar tu entorno de desarrollo, establecer conexiones estables con los servidores de la Escuela, ejecutar consultas de forma consciente y gestionar eficientemente tus scripts de base de datos en ambientes remotos y locales.

---

## 🧭 Propósito de la Unidad

En MYSD trabajarás con bases de datos relacionales en dos entornos distintos, cada uno con sus propias herramientas y flujos de trabajo. Esta unidad te prepara para dominar ambos:

| Entorno | Motor de BD | Herramienta principal | Sub-unidad |
| :--- | :---: | :--- | :---: |
| **Servidor de la Escuela y local** | Oracle | Oracle SQL Developer (app nativa) | [Oracle SQL Developer](../Unidad-SQL-Oracle/) |
| **VS Code + PostgreSQL** | PostgreSQL | VS Code con SQLTools | [PostgreSQL en VS Code](../Unidad-SQL-Postgre-VSC/) |

{: .important }
> Ambos entornos siguen la filosofía de **trabajo consciente**: las consultas se escriben y ejecutan manualmente, sin depender de asistentes automáticos ni generadores de código. Para VS Code, esto se logra con la configuración Vainilla documentada en la **[Guía VS Code Vainilla](../VSCode-Vanila/)**.

---

## 🧠 Conceptos Transversales

Independientemente del entorno que uses, estos conceptos aplican en cualquier motor de base de datos relacional:

### ¿Qué es un sistema gestor de bases de datos (SGBD)?

Un SGBD es el software que permite crear, administrar y consultar bases de datos. En este curso trabajamos con dos de los más usados en la industria:

* **Oracle Database:** Sistema robusto, muy presente en entornos empresariales y en la academia. El servidor de la Escuela (**Granate**) corre Oracle.
* **PostgreSQL:** Sistema de código abierto, ampliamente adoptado en la industria moderna y en proyectos de software libre. Se integra naturalmente con VS Code mediante SQLTools.

### Parámetros de Conexión — ¿Qué significan?

Cualquier cliente de base de datos necesita estos datos para establecer una conexión:

| Parámetro | Descripción |
| :--- | :--- |
| **Hostname** | Dirección del servidor donde vive la base de datos |
| **Port** | Puerto de red por el que escucha el SGBD (Oracle: `1521`, PostgreSQL: `5432`) |
| **SID / Database** | Identificador de la instancia o base de datos específica dentro del servidor |
| **Usuario** | Cuenta con la que se accede al esquema personal |
| **Contraseña** | Credencial de autenticación |

### El `.gitignore` en proyectos de MYSD

Cuando combines scripts SQL con un proyecto Java bajo control de versiones, asegúrate de incluir el `.gitignore` estándar de la línea (ver [Unidad 1: CVS](../Unidad-CVS/)):

```text
*
!*/
!*.doc
!*.java
!*.asta
!*.sql
```

---

## 🛠️ Elige tu Entorno

{: .highlight }
> ### 🏛️ [Oracle SQL Developer — Entorno Principal](../Unidad-SQL-Oracle/)
> Conexión al servidor Granate de la Escuela, instalación de Oracle XE para trabajo local, protocolo de vaciado y troubleshooting. Herramienta: Oracle SQL Developer (app nativa).

{: .highlight }
> ### 💻 [PostgreSQL en VS Code — Entorno Moderno](../Unidad-SQL-Postgre-VSC/)
> Conexión a bases de datos PostgreSQL desde VS Code con SQLTools, bajo la configuración Vainilla de programación consciente. Requiere tener VS Code configurado según la [Guía VS Code Vainilla](../VSCode-Vanila/).

---

## 📚 Verificación y Recursos Adicionales

{: .warning }
> **Pregunta de Verificación:** ¿Cuál es la diferencia fundamental entre Oracle Database y PostgreSQL en términos de licenciamiento, puerto de red predeterminado y modelo de identificación de la base de datos (SID vs nombre de base de datos)?

**Recursos generales:**
* 📘 [Descarga de Oracle SQL Developer](https://www.oracle.com/database/sqldeveloper/)
* 📦 [Oracle Database Express Edition (XE)](https://www.oracle.com/database/technologies/xe-downloads.html)
* 📘 [PostgreSQL — Documentación Oficial](https://www.postgresql.org/docs/)
* 📘 [SQLTools — VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools)
