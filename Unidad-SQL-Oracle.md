---
layout: default
title: "Oracle SQL Developer"
parent: "Unidad 3: Oracle SQL"
nav_order: 1
permalink: /Unidad-SQL-Oracle/
---

# 🏛️ Oracle SQL Developer — Entorno Principal MYSD
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **Modelos y Servicios de Datos (MYSD)** 🎓

{: .note }
> **Resultados de Aprendizaje:** Al finalizar esta sub-unidad, estarás en capacidad de configurar Oracle SQL Developer para acceder al servidor remoto de la Escuela y a una instalación local de Oracle XE, así como aplicar el protocolo de trabajo responsable en recursos compartidos.

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

### 🛠️ Configuración en Oracle SQL Developer

1. Inicia la aplicación y localiza el panel izquierdo.
2. Haz clic en el ícono verde **Nueva Conexión (+)**.
3. Ingresa un nombre descriptivo (ej. `"Granate-Remoto"`).
4. Completa los campos según la tabla anterior.
5. Haz clic en **Test**. Si visualizas `Status: Success`, presiona **Connect**.

{: .important }
> Si la prueba de conexión falla, verifica que no tengas espacios en el campo **Usuario** y que la **Contraseña** esté en minúsculas. Si el problema persiste, consulta la sección de Troubleshooting al final de esta página.

---

## 🏠 B. Trabajo en Local (Oracle XE)

Si deseas realizar prácticas privadas o no dispones de conexión a red de la Escuela, puedes utilizar **Oracle Express Edition (XE)** instalado en tu propia máquina como laboratorio personal.

### Parámetros de Conexión Local

| Campo | Valor |
| :--- | :--- |
| **Hostname** | `localhost` |
| **Port** | `1521` |
| **SID** | `xe` |
| **Usuario** | Tu usuario local de Oracle XE |
| **Contraseña** | La que asignaste durante la instalación |

### Configuración en Oracle SQL Developer

Los pasos son idénticos a la conexión remota. Solo cambian los valores:
1. Crea una **Nueva Conexión (+)** con nombre descriptivo (ej. `"Local-XE"`).
2. Completa con los parámetros de la tabla anterior.
3. Haz clic en **Test** → `Status: Success` → **Connect**.

---

## ✅ C. Protocolo de Vaciado y Buenas Prácticas

{: .important }
> **Protocolo de Vaciado:** El servidor `granate` es un recurso compartido entre todos los estudiantes. Al finalizar cada sesión de trabajo, es **responsabilidad del estudiante** ejecutar el vaciado de tablas temporales para evitar la saturación del espacio en disco de la base de datos común.

### Gestión de Scripts con Control de Versiones

Todos tus scripts `.sql` deben estar bajo control de versiones siguiendo las prácticas de la [Unidad 1: CVS](../Unidad-CVS/). Recuerda que el `.gitignore` estándar del curso ya incluye `!*.sql` para que tus scripts queden rastreados.

### Problemas Frecuentes (Troubleshooting)

| Problema | Causa probable | Solución |
| :--- | :--- | :--- |
| No conecta a Granate | Parámetros incorrectos | Verifica hostname, puerto y SID exactamente como indica la tabla |
| Usuario no reconocido | Espacios extra o mayúsculas | El usuario es `bd` + número, sin espacios, todo en minúscula |
| No conecta a XE local | Servicios detenidos | Abre `services.msc` y verifica que `OracleServiceXE` y el `Listener` estén iniciados |
| Error "Listener not found" | Listener no iniciado | En `services.msc`, inicia `OracleOraDB21HomeXETNSListener` |

---

## 🖼️ Material de Apoyo Visual

Para una explicación visual detallada sobre la instalación y los tipos de conexión, consulta las diapositivas interactivas diseñadas para esta sub-unidad:

{: .highlight }
> 🚀 **Diapositivas de la Unidad:** [Presentación Interactiva - Oracle SQL Developer](https://fis-eci.github.io/software-foundations-eci-slides/OracleSQL-presentation.html#1)

---

## 🎥 Práctica Guiada: Videos para MYSD — Oracle

Para evidenciar el logro del objetivo, revisa estos tutoriales donde configuramos los entornos de Oracle SQL paso a paso.

### 🛠️ Instalación y Configuración de Oracle SQL Developer
¿Cómo dejar lista la herramienta principal del curso desde cero? En este tutorial instalamos y configuramos Oracle SQL Developer en cualquier sistema operativo.

* **Herramienta:** Oracle SQL Developer (versión de escritorio).
* **Conceptos aplicados:** Descarga, instalación y primera ejecución en entornos Windows, Mac y Linux.

📺 **Ver el Video:** [Cómo instalar y configurar Oracle SQL Developer (Multiplataforma)](https://youtu.be/ThTLYnKWSAY)

### 🌐 Conexión al Servidor Granate Oracle DB (Sin VPN)
¿Cómo acceder al servidor de la Escuela sin necesidad de VPN? En este tutorial establecemos la conexión remota al servidor **Granate** con los parámetros correctos.

* **Caso de estudio:** Configuración de nueva conexión con Hostname, Port y SID de la Escuela.
* **Conceptos aplicados:** Parámetros de red, prueba de conexión (`Status: Success`) y resolución de errores frecuentes.

📺 **Ver el Video:** [Conexión al Servidor Granate Oracle DB (Sin VPN)](https://youtu.be/zBnge96jiqE)

### 🏠 Oracle Database Express Edition (XE): Tu Laboratorio Local
¿Cómo practicar sin depender del servidor de la Escuela? En este tutorial configuramos Oracle XE como entorno local para sesiones de trabajo autónomas.

* **Caso de estudio:** Conexión local con `localhost`, puerto `1521` y SID `xe`.
* **Conceptos aplicados:** Instalación de Oracle XE, verificación de servicios (`OracleServiceXE` y `Listener`) y conexión desde SQL Developer.

📺 **Ver el Video:** [Oracle Database Express Edition (XE): Tu Laboratorio Local](https://youtu.be/cLklOvlBNaM)

---

## 📚 Verificación y Recursos Adicionales

{: .warning }
> **Pregunta de Verificación:** ¿Cuál es la diferencia principal entre el SID `ORCL` (servidor Granate) y el SID `xe` (local) en términos de la ubicación física de los datos y del contexto de uso?

**Recursos:**
* 📘 [Descarga de Oracle SQL Developer](https://www.oracle.com/database/sqldeveloper/)
* 📦 [Oracle Database Express Edition (XE)](https://www.oracle.com/database/technologies/xe-downloads.html)
