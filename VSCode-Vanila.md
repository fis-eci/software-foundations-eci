---
layout: default
title: "Guía: VS Code Vainilla"
nav_order: 7
permalink: /VSCode-Vanila/
---

# 💻 Guía de Configuración: VS Code Vainilla
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Aplicable a **DOPO (Desarrollo Orientado por Objetos)** y **MYSD (Modelos y Servicios de Datos)** 🎓

{: .note }
> **Propósito de esta guía:** Esta página centraliza toda la configuración necesaria para usar VS Code en la línea IS-FUNDAMENTOS, tanto para Java (DOPO) como para SQL (MYSD). Consúltala antes de empezar a trabajar en cualquier proyecto del curso en este entorno.

---

## 🧭 ¿Por Qué VS Code?

VS Code es una excelente opción como entorno de desarrollo para este curso porque:

* **Es moderno y ampliamente usado en la industria** — aprenderlo tiene valor directo más allá del curso.
* **Es atractivo y motivador** — cuenta con extensiones visuales que hacen el desarrollo más agradable.
* **Es integrador** — permite trabajar con Java, SQL y control de versiones en un único entorno.
* **Es configurable** — permite establecer un espacio de aprendizaje controlado que favorezca la comprensión profunda de la programación.

{: .important }
> **Filosofía "Vainilla":** En IS-FUNDAMENTOS, VS Code se configura deliberadamente para **desactivar la asistencia automática de IA y las sugerencias agresivas**. El objetivo es que el estudiante aprenda a programar de forma consciente, comprendiendo cada línea que escribe, sin depender de herramientas que generen código por él. La madurez de esta configuración puede evolucionar a medida que avanza el semestre.

---

## 🔌 Extensiones por Curso

### ☕ Para DOPO — Desarrollo Orientado por Objetos (Java)

| Extensión / Herramienta | Tipo | Propósito |
| :--- | :---: | :--- |
| **Extension Pack for Java** | Base | Soporte completo para Java: edición, compilación, depuración y gestión de proyectos |
| **Java Test Runner** | Complemento | Ejecución de pruebas unitarias con JUnit directamente desde VS Code |
| **JaCoCo** | Herramienta externa | Cálculo de cobertura de pruebas y generación de reportes |
| **Coverage Gutters** | Complemento | Visualización de la cobertura generada por JaCoCo en el propio editor |
| **PMD** | Complemento | Análisis estático para verificar el cumplimiento de reglas de calidad |

### 🗄️ Para MYSD — Modelos y Servicios de Datos (SQL)

| Extensión | Tipo | Propósito |
| :--- | :---: | :--- |
| **SQLTools** | Base | Gestión general de bases de datos, ejecución de consultas y exploración de esquemas |
| **SQLTools PostgreSQL Driver** | Complemento | Habilita la conexión específica con bases de datos PostgreSQL |

### Cómo instalar las extensiones

1. Abre VS Code y accede al panel de extensiones con `Ctrl+Shift+X`.
2. Busca cada extensión por su nombre exacto tal como aparece en la tabla.
3. Haz clic en **Install**.
4. Reinicia VS Code después de instalar el **Extension Pack for Java** para que todos sus componentes queden activos.

---

## ⚙️ Configuración Vainilla — Paso a Paso

Aplica estos ajustes abriendo el archivo `settings.json` con `Ctrl+Shift+P` → **"Open User Settings (JSON)"** y añadiendo las claves indicadas.

### Configuración General — Aplica a Todo Estudiante

| Nombre | Objetivo | Cómo configurarlo |
| :--- | :--- | :--- |
| **Extensiones de IA** | Evitar generación automática de código | Ir a **Extensions** → buscar **GitHub Copilot** → **Disable** |
| **Sugerencias en línea** | Desactivar predicciones automáticas | `"editor.inlineSuggest.enabled": false` |
| **Autocompletado rápido** | Evitar sugerencias mientras se escribe | `"editor.quickSuggestions": false` |
| **Snippets** | Evitar autocompletar estructuras completas | `"editor.snippetSuggestions": "none"` |
| **Disparo de sugerencias** | Evitar sugerencias al escribir caracteres especiales | `"editor.suggestOnTriggerCharacters": false` |
| **Ayuda de parámetros** | Evitar pistas sobre argumentos de funciones | `"editor.parameterHints.enabled": false` |
| **Hover (tooltips)** | Evitar ventanas emergentes informativas | `"editor.hover.enabled": false` |
| **Linting automático** | Evitar advertencias y correcciones constantes | Deshabilitar extensiones de linting automático no requeridas |
| **Formato automático** | Evitar que el código se formatee solo | `"editor.formatOnSave": false`, `"editor.formatOnType": false` |
| **Acciones automáticas** | Evitar correcciones automáticas al guardar | `"editor.codeActionsOnSave": {}` (vacío) |
| **Lightbulb (quick fix)** | Evitar sugerencias de corrección automática | `"editor.lightbulb.enabled": false` |
| **Minimapa** | Reducir distracciones visuales | `"editor.minimap.enabled": false` |
| **Breadcrumbs** | Simplificar la navegación visual | `"breadcrumbs.enabled": false` |

### Configuración Adicional para MYSD (PostgreSQL)

| Nombre | Objetivo | Cómo configurarlo |
| :--- | :--- | :--- |
| **Autocompletado SQL avanzado** | Evitar dependencia de sugerencias automáticas | Deshabilitar autocompletado avanzado en la extensión SQLTools |
| **Asistentes visuales SQL** | Evitar generación automática de consultas | No usar generadores visuales de consultas |
| **Ejecución de consultas** | Favorecer control explícito del estudiante | Ejecutar consultas siempre de forma manual |

### Configuración Adicional para DOPO (Java)

| Nombre | Objetivo | Clave en `settings.json` |
| :--- | :--- | :--- |
| **Autocompletado de métodos** | Evitar sugerencias automáticas de métodos | `"editor.suggest.showMethods": false` |
| **Autocompletado de funciones** | Evitar sugerencias automáticas de funciones | `"editor.suggest.showFunctions": false` |
| **Autocompletado de atributos** | Evitar completado automático de campos | `"editor.suggest.showFields": false` |
| **Auto-imports** | Fomentar comprensión de dependencias | Deshabilitar importaciones automáticas de Java |
| **Refactorización automática** | Evitar soluciones automáticas del IDE | Limitar el uso de herramientas de refactorización automática |

---

## 📋 Archivo `settings.json` Completo

Copia y pega este bloque en tu `settings.json` para aplicar toda la configuración Vainilla de una vez. Luego ajusta según el curso que estés tomando.

```json
{
    "editor.inlineSuggest.enabled": false,
    "editor.quickSuggestions": false,
    "editor.snippetSuggestions": "none",
    "editor.suggestOnTriggerCharacters": false,
    "editor.parameterHints.enabled": false,
    "editor.hover.enabled": false,
    "editor.formatOnSave": false,
    "editor.formatOnType": false,
    "editor.codeActionsOnSave": {},
    "editor.lightbulb.enabled": false,
    "editor.minimap.enabled": false,
    "breadcrumbs.enabled": false,
    "editor.suggest.showMethods": false,
    "editor.suggest.showFunctions": false,
    "editor.suggest.showFields": false,
    "java.completion.enabled": false,
    "java.autobuild.enabled": true
}
```

{: .warning }
> `java.autobuild.enabled` se mantiene en `true` para que VS Code compile el proyecto automáticamente al guardar. Solo las *sugerencias y asistencias* se desactivan, no el proceso de compilación.

---

## 🔗 ¿A Dónde ir Después?

Con VS Code configurado, dirígete a la unidad que corresponda a tu curso:

* ☕ **DOPO — Análisis de Software:** [Unidad 4 — Análisis en VS Code](../Unidad-Analisis-VSC/)
* 🗄️ **MYSD — Bases de Datos:** [Unidad 3 — PostgreSQL en VS Code](../Unidad-SQL-Postgre-VSC/)

---

## 📚 Recursos

* 💻 [**Descarga de Visual Studio Code**](https://code.visualstudio.com/)
* 📘 [**Extension Pack for Java**](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)
* 📘 [**Coverage Gutters**](https://marketplace.visualstudio.com/items?itemName=ryanluker.vscode-coverage-gutters)
* 📘 [**PMD para VS Code**](https://marketplace.visualstudio.com/items?itemName=chuckjonas.apex-pmd)
* 📘 [**SQLTools**](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools)
* 📘 [**SQLTools PostgreSQL Driver**](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools-driver-pg)
