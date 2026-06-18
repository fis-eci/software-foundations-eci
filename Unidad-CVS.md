---
layout: default
title: "Unidad 1: CVS"
nav_order: 3
permalink: /Unidad-CVS/
---

# 📦 Unidad 1: Control de Versiones (CVS)
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **DOPO (Desarrollo Orientado por Objetos)** y **Modelos y Servicios de Datos (MYSD)** 🎓

{: .note }
> **Resultados de Aprendizaje:** Al finalizar esta unidad, comprenderás los conceptos de un CVS, aplicarás buenas prácticas de programación por pares y utilizarás Git de forma fluida en tus proyectos de **MYSD (Modelos y Servicios de Datos)** y **DOPO (Desarrollo Orientado por Objetos)**.

---

## 🧠 S1: Teoría (El corazón del CVS)

### ¿Qué problema resuelve un sistema de control de versiones?
Un CVS resuelve un conjunto de problemas fundamentales que aparecen cuando los archivos cambian con el tiempo, especialmente en proyectos que crecen o involucran a varias personas:

* 💥 **Pérdida del historial:** Sin un registro estructurado, no se sabe qué cambió ni cuándo.
* 🛑 **Sobrescritura de trabajo:** Los cambios de una persona pueden borrar accidentalmente los de otra.
* ⏪ **Imposibilidad de deshacer errores:** No hay una forma segura de volver a un estado anterior estable.
* 🌪️ **Desorden en la colaboración:** No existe una versión común y clara para coordinarse.
* 🛤️ **Falta de líneas de trabajo paralelas:** No se pueden probar ideas sin afectar el trabajo estable.

> **Definición Core:** El control de versiones es un conjunto de principios y métodos que permiten registrar, organizar y recuperar los cambios realizados sobre uno o varios archivos a lo largo del tiempo.

### ¿Cuál es la estructura de control?
La estructura de control es un **Grafo Dirigido Acíclico (DAG)**.
* **Vértices (Versiones):** Son estados completos del proyecto. Una versión, una vez creada, nunca se modifica; solo se crean nuevas versiones a partir de ella.
* **Arcos:** Indican que una versión surge de otra.
* **El Tronco (`main` / `master`):** Es la rama principal que sirve como eje central del historial y como punto de referencia para el desarrollo estable del proyecto.
* **Las Ramas (Branches):** Son líneas independientes de versiones que se separan del historial principal para permitir que el desarrollo de nuevas ideas evolucione en paralelo. Nacen de un vértice existente y pueden abandonarse o fundirse (merge).

### Componentes de un CVS
1. **Repositorio Local:** El espacio privado donde se crean y prueban versiones.
2. **Repositorio Remoto:** El espacio compartido donde se consolidan y organizan.

---

## 🛡️ S2: Buenas Prácticas (Desarrollo por pares)

El éxito en **DOPO** y **MYSD** depende de cómo interactúas con tu equipo. Sigue estas reglas inquebrantables:

### 1. El archivo `.gitignore` es obligatorio
Nunca subas archivos binarios, compilados o temporales del IDE. En la raíz de tu proyecto, tu `.gitignore` debe verse así:
```text
*
!*/
!*.doc
!*.java
!*.asta
!*.sql
```

### 2. Mensajes de Commit Significativos
Un commit debe explicar qué hace y por qué.
```diff
- git commit -m "cambios"
- git commit -m "terminé la clase"
+ git commit -m "feat: añade clase Vehiculo con métodos base"
+ git commit -m "fix: corrige error de sobrescritura en esquema.sql"
```

### 3. Ramas por Desarrollador o Funcionalidad
Nunca trabajes en `main` al mismo tiempo que tu compañero. Creen ramas con sus apellidos (ej. `rama-perez`, `rama-gomez`).

---

## 💻 S3: Herramienta (Git en acción)

Git es el CVS más utilizado en el mundo. Aquí están las acciones básicas mapeadas a nuestro modelo teórico:

### En un Repositorio Local

| Acción | Comando Git | Descripción Teórica |
|---|---|---|
| Crear repo | `git init` | Establece el historial inicial del usuario. |
| Crear versiones | `git commit` | Agrega nuevos vértices al repositorio. |
| Crear ramas | `git branch <nombre>` | Abre líneas de desarrollo en el repositorio. |
| Ubicar versión | `git checkout <rama>` | Se mueve entre ramas o vértices. |
| Fusionar líneas | `git merge <rama>` | Combina historias paralelas. |

### Interacción Remoto ↔ Local

| Flujo | Acción | Comando Git | Descripción |
|---|---|---|---|
| Local a Remoto | Publicar | `git push` | Envía versiones y ramas al servidor. |
| Remoto a Local | Clonar | `git clone` | Copia el repositorio remoto completo a tu máquina. |
| Remoto a Local | Transmitir | `git pull` | Trae la evolución oficial del proyecto. (¡Paso clave antes de trabajar!) |

---

## 🖼️ Material de Apoyo Visual

Para facilitar el seguimiento de la teoría y los pasos técnicos, puedes consultar las diapositivas interactivas diseñadas para esta unidad:

{: .highlight }
> 🚀 **Diapositivas de la Unidad:** [Presentación Interactiva - Control de Versiones](https://fis-eci.github.io/software-foundations-eci-slides/CVS-presentation.html#1)

---

## 🎥 Práctica Guiada: Videos para DOPO y MYSD

Para evidenciar el logro del objetivo, revisa estos tutoriales donde resolvemos problemas reales paso a paso.

### ☕ Para DOPO (Desarrollo Orientado por Objetos)
¿Cómo trabajar en el mismo archivo Java con un compañero sin borrar sus cambios? En este tutorial gestionamos el ciclo de vida de un proyecto colaborativo.

* **Caso de estudio:** Conflicto en `sistema.java`.
* **Conceptos aplicados:** Creación de ramas por apellido, simulación de conflicto y resolución (Merge).

📺 **Ver el Video:** [Control de Versiones en Java: Git + GitHub](https://youtu.be/turysdDQJRI)

### 🗄️ Para MYSD (Modelos y Servicios de Datos)
¿Cómo editar el mismo script SQL sin arruinar la base de datos de tu compañero?

* **Caso de estudio:** Edición paralela de `esquema.sql`.
* **Conceptos aplicados:** `git init`, `remote add`, el paso clave del `git pull` y resolución de conflictos.

📺 **Ver el Video:** [Control de Versiones en SQL: Git + GitHub](https://youtu.be/t5W_g_uRRAE)

---

## 📚 Verificación y Recursos Adicionales

{: .warning }
> **Pregunta de Verificación:** Si tú y tu compañero modifican la misma línea de código en ramas distintas y ambos intentan fusionarla a `main`, ¿qué sucede y cómo se resuelve basándote en la teoría de grafos?

**Enlaces de interés:**
* 🌐 [Learn Git Branching (Interactivo)](https://learngitbranching.js.org/)
* 📘 [Documentación oficial de Git](https://git-scm.com/doc)