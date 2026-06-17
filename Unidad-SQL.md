---
layout: default
title: "Unidad 3: Oracle SQL"
nav_order: 5
permalink: /Unidad-SQL/
---

# 🗄️ Unidad 3: Entornos de Trabajo Oracle SQL
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **Modelos y Servicios de Datos (MYSD)** 🎓

{: .note }
> **Resultados de Aprendizaje:** Al finalizar esta unidad, estarás en capacidad de configurar tu entorno de desarrollo, establecer conexiones estables con los servidores de la Escuela y gestionar eficientemente tus scripts de base de datos en ambientes remotos y locales.

---

## 🌐 A. Trabajo con el Servidor de la Escuela (Remoto)

Para interactuar con la base de datos centralizada de la universidad, es fundamental configurar correctamente los parámetros de red.

### Parámetros de Conexión Críticos
Utiliza la siguiente tabla para configurar tu acceso al servidor **Granate**:

| Campo | Valor |
| :--- | :--- |
| **Hostname** | `granate.is.escuelaing.edu.co` |
| **Port** | `1521` |
| **SID** | `ORCL` |
| **Usuario** | `bd` + tu número de identificación |
| **Contraseña** | Igual al usuario (en minúscula) |

### 🛠️ Configuración en Oracle SQL Developer (App Nativa)
1. Inicia la aplicación y localiza el panel izquierdo.
2. Haz clic en el icono verde **Nueva Conexión (+)**.
3. Ingresa un nombre descriptivo (ej. "Escuela-Remoto").
4. Completa los datos según la tabla anterior.
5. Haz clic en **Test**. Si visualizas `Status: Success`, presiona **Connect**.

---

## ⚡ B. Alternativa Moderna: SQL Developer para VS Code

Para los estudiantes que prefieren un flujo de trabajo integrado, es posible utilizar Visual Studio Code mediante la extensión oficial de Oracle, pero para este curso no se recomienda por el uso de herramientas de IA para generar el código.

### Pasos para la configuración:
1. Desde el Marketplace de VS Code, instala: **"Oracle SQL Developer Extension for VSCode"**.
2. Dirígete al panel de la extensión y selecciona **Create Connection**.
3. Los parámetros de red (Hostname, Puerto y SID) son **idénticos** a los de la versión de escritorio.

{: .highlight }
> **Ventaja:** Esta extensión permite gestionar tus scripts `.sql` junto a tu código de aplicación en un único entorno, facilitando el desarrollo por pares y el control de versiones.



---

## 🏠 C. Trabajo en Local (Oracle XE)

Si deseas realizar prácticas privadas o no dispones de conexión a internet (VPN), puedes utilizar **Oracle Express Edition (XE)** instalado en tu propia máquina.

* **Hostname:** `localhost`
* **Hostname:** `localhost`
* **Hostname:** `localhost`
* **Port:** `1521`
* **SID:** `xe`

---

## ✅ D. Protocolo de Vaciado y Buenas Prácticas

{: .important }
> **Protocolo de Vaciado:** El servidor `granate` es un recurso compartido. Al finalizar tu sesión, es responsabilidad del estudiante ejecutar el vaciado de tablas temporales para evitar la saturación del espacio en disco de la base de datos común.

### Problemas Frecuentes (Troubleshooting)
* **En local:** Verifica que los servicios `OracleServiceXE` y el `Listener` estén iniciados en `services.msc`.
* **En servidor:** Verifica que tu usuario `bd` no tenga espacios adicionales y que la contraseña esté en minúsculas.

---

## 🖼️ Material de Apoyo Visual

Para una explicación visual detallada sobre la instalación y los tipos de conexión, consulta las diapositivas interactivas diseñadas para esta unidad:

{: .highlight }
> 🚀 **Diapositivas de la Unidad:** [Presentación Interactiva - Oracle SQL Developer (Canva)](https://heliogen.my.canva.site/oracle-sql-developer-mysd)

---

## 📚 Verificación y Recursos Adicionales

{: .warning }
> **Pregunta de Verificación:** ¿Cuál es la diferencia principal entre el SID `ORCL` y el SID `xe` en términos de la ubicación física de los datos?

**Enlaces de interés:**
* 📘 [Descarga de Oracle SQL Developer](https://www.oracle.com/database/sqldeveloper/)
* 📦 [Oracle Database Express Edition (XE)](https://www.oracle.com/database/technologies/xe-downloads.html)
