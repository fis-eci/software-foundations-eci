---
layout: default
title: "PostgreSQL en VS Code"
parent: "Unidad 3: Oracle SQL"
nav_order: 2
permalink: /Unidad-SQL-Postgre-VSC/
---

# 💻 PostgreSQL en VS Code — Entorno Moderno MYSD
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **Modelos y Servicios de Datos (MYSD)** 🎓

{: .note }
> **Prerrequisitos:** (1) Tener VS Code instalado y configurado según la **[Guía VS Code Vainilla](../VSCode-Vanila/)** — ahí encontrarás la configuración Vainilla general y específica para MYSD. (2) Haber revisado la [Unidad 3 — Página Principal](../Unidad-SQL/) para los conceptos transversales de conexión.

---

## 🧭 ¿Por Qué PostgreSQL con VS Code?

PostgreSQL es uno de los motores de bases de datos relacionales más adoptados en la industria moderna. Usarlo desde VS Code con la filosofía Vainilla ofrece ventajas claras:

* **Entorno unificado:** Gestiona tus scripts `.sql`, tu código Java y tu control de versiones desde una sola ventana.
* **Integración con Git:** Los archivos `.sql` conviven con el resto del proyecto y se versionan con las prácticas de la [Unidad 1: CVS](../Unidad-CVS/).
* **Aprendizaje consciente:** SQLTools está configurado para ejecutar consultas manualmente, sin asistentes ni generadores automáticos.
* **Portabilidad:** PostgreSQL corre en cualquier sistema operativo y tiene una versión local gratuita equivalente a Oracle XE.

{: .important }
> **Filosofía Vainilla en MYSD:** Las consultas SQL se escriben manualmente, se entienden línea a línea y se ejecutan de forma explícita. No se usan asistentes visuales de construcción de consultas ni generadores automáticos. Ver configuración completa en la [Guía VS Code Vainilla](../VSCode-Vanila/).

---

## 🔌 Extensiones Requeridas

Instala estas extensiones desde el panel de extensiones de VS Code (`Ctrl+Shift+X`):

| Extensión | Tipo | Propósito |
| :--- | :---: | :--- |
| **SQLTools** | Base | Gestión de conexiones, escritura y ejecución de consultas SQL |
| **SQLTools PostgreSQL Driver** | Complemento | Habilita la conexión específica con bases de datos PostgreSQL |

### Instalación paso a paso

1. Abre VS Code y presiona `Ctrl+Shift+X`.
2. Busca `SQLTools` → instala la extensión de **Matheus Teixeira**.
3. Busca `SQLTools PostgreSQL/Cockroach Driver` → instala el driver oficial.
4. Recarga VS Code cuando lo solicite.

{: .highlight }
> Si aún no has aplicado la configuración Vainilla general (desactivar sugerencias, IA, tooltips), hazlo ahora siguiendo la **[Guía VS Code Vainilla](../VSCode-Vanila/)** antes de continuar.

---

## 🌐 A. Conexión a la Base de Datos PostgreSQL

### Parámetros de Conexión

Los parámetros exactos dependen del servidor asignado por el profesor. Utiliza la siguiente estructura como referencia:

| Campo | Valor |
| :--- | :--- |
| **Connection Name** | Nombre descriptivo (ej. `"Escuela-Postgre"`) |
| **Server / Host** | Dirección del servidor PostgreSQL (proporcionada por el profesor) |
| **Port** | `5432` (puerto estándar de PostgreSQL) |
| **Database** | Nombre de la base de datos asignada |
| **Username** | Tu usuario de acceso |
| **Password** | Tu contraseña de acceso |

{: .important }
> En PostgreSQL no existe el concepto de **SID** como en Oracle. La base de datos se identifica directamente por su **nombre** (campo `Database`). Cada estudiante trabaja dentro de su propio esquema dentro de esa base de datos.

### Crear la Conexión en SQLTools

1. Haz clic en el ícono de **SQLTools** en la barra lateral de VS Code (ícono de base de datos).
2. Selecciona **Add New Connection**.
3. Elige **PostgreSQL** como tipo de conexión.
4. Completa los campos con los parámetros de la tabla anterior.
5. Haz clic en **Test Connection**. Si aparece `Connected successfully`, guarda con **Save Connection**.

---

## 🏠 B. Trabajo en Local (PostgreSQL Local)

Si no tienes acceso al servidor de la Escuela o quieres practicar de forma autónoma, puedes instalar PostgreSQL localmente.

### Parámetros de Conexión Local

| Campo | Valor |
| :--- | :--- |
| **Server / Host** | `localhost` |
| **Port** | `5432` |
| **Database** | `postgres` (base de datos por defecto) o la que hayas creado |
| **Username** | `postgres` (usuario administrador por defecto) |
| **Password** | La que asignaste durante la instalación |

### Instalación de PostgreSQL Local

1. Descarga PostgreSQL desde [postgresql.org/download](https://www.postgresql.org/download/).
2. Ejecuta el instalador y sigue los pasos. Anota la contraseña del usuario `postgres`.
3. Verifica que el servicio esté activo: en Windows, abre `services.msc` y confirma que `postgresql-x64-XX` está en estado **Running**.
4. Crea la conexión en SQLTools usando los parámetros de la tabla anterior.

---

## 💾 C. Flujo de Trabajo con SQL en VS Code

### Escribir y Ejecutar Consultas

1. En el panel de SQLTools, expande tu conexión para explorar tablas y esquemas.
2. Abre un archivo `.sql` existente o crea uno nuevo (`Ctrl+N` → guarda con extensión `.sql`).
3. Escribe la consulta manualmente.
4. Para ejecutarla: selecciona el texto de la consulta y presiona `Ctrl+Shift+E`, o haz clic derecho → **Run Selected Query**.

{: .warning }
> **Recuerda la filosofía Vainilla:** ejecuta siempre las consultas de forma manual y explícita. No uses el botón de "ejecutar todo" sin revisar línea por línea lo que va a correr.

### Gestión de Scripts con Control de Versiones

Todos tus scripts `.sql` deben vivir dentro de la carpeta de tu proyecto y estar bajo control de versiones:

```text
mi-proyecto/
├── src/
│   └── *.java
├── scripts/
│   ├── esquema.sql      ← Definición de tablas (DDL)
│   └── datos.sql        ← Datos de prueba (DML)
└── .gitignore
```

El `.gitignore` estándar del curso ya incluye `!*.sql` para que tus scripts queden rastreados. Sigue las prácticas de mensajes de commit de la [Unidad 1: CVS](../Unidad-CVS/):

```diff
+ git commit -m "feat: añade esquema inicial de tablas con claves foráneas"
+ git commit -m "fix: corrige restricción NOT NULL en tabla cliente"
- git commit -m "cambios sql"
```

### Buenas Prácticas al Trabajar en Servidor Compartido

* **No ejecutes `DROP TABLE` sin confirmación del equipo** — el servidor es compartido.
* **Vacía tus tablas temporales al finalizar la sesión** — protocolo heredado de la sub-unidad Oracle.
* **Prefiere `TRUNCATE` sobre `DELETE` sin `WHERE`** para limpiar datos de prueba de forma eficiente.
* **Cierra la conexión al terminar** — SQLTools mantiene conexiones activas; desconéctate desde el panel lateral.

---

## 🖼️ Material de Apoyo Visual

Para una explicación visual detallada sobre la configuración de VS Code con SQLTools y el flujo de trabajo con PostgreSQL, consulta las diapositivas interactivas diseñadas para esta sub-unidad:

{: .highlight }
> 🚀 **Diapositivas de la Unidad:** [Presentación Interactiva - PostgreSQL en VS Code](https://fis-eci.github.io/software-foundations-eci-slides/SQL-PostgreVSC-presentation.html#1)

---

## 🎥 Práctica Guiada: Videos para MYSD — PostgreSQL

### 💻 Configuración de VS Code con SQLTools para PostgreSQL
¿Cómo dejar VS Code listo para trabajar con PostgreSQL desde cero? En este tutorial instalamos las extensiones, aplicamos la configuración Vainilla para MYSD y establecemos la primera conexión.

* **Herramientas:** VS Code, SQLTools, SQLTools PostgreSQL Driver.
* **Conceptos aplicados:** Instalación de extensiones, configuración Vainilla para MYSD, creación de conexión y prueba de acceso.

📺 **Ver el Video:** *(Próximamente)*

### 🗄️ Flujo de Trabajo SQL en VS Code: Consultas Conscientes
¿Cómo escribir, organizar y ejecutar scripts SQL en VS Code de forma profesional? En este tutorial trabajamos con un esquema real, gestionamos los scripts con Git y ejecutamos consultas manualmente.

* **Caso de estudio:** Creación y consulta de un esquema de base de datos relacional.
* **Conceptos aplicados:** DDL y DML manuales, exploración del esquema en SQLTools, versionado de scripts `.sql`.

📺 **Ver el Video:** *(Próximamente)*

---

## 📚 Verificación y Recursos Adicionales

{: .warning }
> **Pregunta de Verificación:** En PostgreSQL, un compañero ejecuta `DELETE FROM clientes;` sin cláusula `WHERE` en el servidor compartido. ¿Qué consecuencia tiene esto para el resto del equipo? ¿Cómo se podría haber evitado con un buen uso de control de versiones y commits atómicos?

**Recursos:**
* 💻 [Guía VS Code Vainilla — Configuración completa para MYSD](../VSCode-Vanila/)
* 📘 [SQLTools — VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools)
* 📘 [SQLTools PostgreSQL Driver — Marketplace](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools-driver-pg)
* 📘 [PostgreSQL — Documentación Oficial](https://www.postgresql.org/docs/)
* 📦 [Descarga PostgreSQL Local](https://www.postgresql.org/download/)
