---
layout: default
title: "Análisis en VS Code"
parent: "Unidad 4: Análisis de Software"
nav_order: 2
permalink: /Unidad-Analisis-VSC/
---

# 💻 S3 & S4: Análisis de Software en Visual Studio Code
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **DOPO (Desarrollo Orientado por Objetos)** 🎓

{: .note }
> **Prerrequisitos:** (1) Haber estudiado la teoría y el ejemplo de la [Unidad 4 — Página Principal](../Unidad-Analisis/). (2) Tener VS Code configurado según la **[Guía VS Code Vainilla](../VSCode-Vanila/)** — ahí encontrarás la instalación de extensiones y el `settings.json` completo para DOPO.

---

## 🔌 Extensiones Necesarias para esta Unidad

Asegúrate de tener instaladas las siguientes extensiones antes de continuar. Si no las tienes, sigue los pasos de la [Guía VS Code Vainilla](../VSCode-Vanila/):

| Extensión / Herramienta | Propósito en esta Unidad |
| :--- | :--- |
| **Extension Pack for Java** | Compilación, ejecución y gestión del proyecto Java |
| **Java Test Runner** | Ejecución de pruebas JUnit desde VS Code |
| **JaCoCo** | Generación del reporte de cobertura |
| **Coverage Gutters** | Visualización de la cobertura en el editor |
| **PMD** | Análisis estático de calidad del código |
| **SonarLint** | Análisis de diseño en tiempo real |

---

## 🔬 S3: Los Cuatro Análisis en VS Code

### 🔵 Análisis 1: SonarLint — Análisis de Diseño

SonarLint analiza el código en tiempo real y muestra los problemas directamente en el editor al escribir y guardar, sin necesidad de ejecutar ningún comando adicional.

**Cómo interpretarlo:**
1. Los problemas aparecen subrayados en el editor con distintos colores según severidad.
2. Abre la vista **Problems** con `Ctrl+Shift+M` para ver todos los incidentes agrupados por archivo.
3. Haz clic sobre cualquier incidente para navegar a la línea afectada.
4. El panel inferior de SonarLint describe la regla violada y ofrece ejemplos de corrección.

**Flujo de resolución:**

| Paso | Acción |
| :---: | :--- |
| 1 | Identifica el incidente de mayor severidad en la vista **Problems** |
| 2 | Navega a la línea afectada y lee la descripción de la regla violada |
| 3 | Documenta: *¿Por qué es relevante? ¿Qué principio viola?* |
| 4 | Aplica la corrección y verifica que el subrayado desaparece al guardar |

**Actividad mientras ves el video:** Pausa cuando SonarLint subraye el primer incidente e intenta escribir la corrección antes de ver la solución aplicada.

### 🟠 Análisis 2: PMD — Análisis de Calidad

**Cómo ejecutarlo:**
1. Abre la paleta de comandos con `Ctrl+Shift+P`.
2. Escribe `PMD: Run` y selecciona el archivo o carpeta a analizar.
3. Los resultados aparecen en la vista **Problems** (`Ctrl+Shift+M`), clasificados por severidad.

**Flujo de resolución:**

| Paso | Acción |
| :---: | :--- |
| 1 | Ordena los problemas por severidad (mayor a menor) |
| 2 | Selecciona el incidente más relevante |
| 3 | Documenta: *¿Por qué es relevante? ¿Qué principio viola?* |
| 4 | Aplica la corrección en el código fuente |
| 5 | Re-ejecuta PMD y confirma que el incidente desapareció |

**Actividad mientras ves el video:** Antes de ver la solución, escribe en papel tu propuesta de corrección para el incidente de mayor severidad que aparezca en pantalla.

### 🟢 Análisis 3: JaCoCo + Coverage Gutters — Pruebas de Cobertura

JaCoCo en VS Code requiere dos pasos: generar el reporte ejecutando las pruebas y luego visualizarlo con Coverage Gutters.

**Cómo ejecutarlo:**
1. Ejecuta las pruebas desde el panel de Testing (ícono de beaker 🧪 en la barra lateral) → **Run All Tests**.
2. JaCoCo genera automáticamente un archivo `jacoco.xml` en la carpeta `target/` o `coverage/`.
3. Abre la paleta de comandos (`Ctrl+Shift+P`) → `Coverage Gutters: Display Coverage`.
4. El editor coloreará las líneas:

| Color | Significado |
| :---: | :--- |
| 🟢 Verde | Línea ejecutada por las pruebas |
| 🔴 Rojo | Línea **no** ejecutada — cobertura pendiente |

{: .highlight }
> Si Coverage Gutters no encuentra el reporte automáticamente, verifica en sus ajustes que `Coverage Gutters: Coverage Base Dir` apunte a la carpeta donde se generó el `jacoco.xml`.

**Flujo de resolución:**
1. Identifica el método con más líneas en rojo.
2. Diseña el caso de prueba faltante con la nomenclatura `shouldXWhenY`.
3. Agrega la prueba, re-ejecuta y verifica que la línea cambia a verde.

**Actividad mientras ves el video:** Cuando aparezca la cobertura en pantalla, identifica las líneas rojas antes de que el monitor las señale y escribe el caso de prueba que las cubriría.

### 🔴 Análisis 4: PIT — Pruebas de Mutación

PIT en VS Code se ejecuta como herramienta externa mediante Maven, ya que no existe un plugin nativo equivalente a Pitclipse.

**Cómo configurarlo:** Agrega el plugin PIT en tu archivo `pom.xml`:

```xml
<plugin>
    <groupId>org.pitest</groupId>
    <artifactId>pitest-maven</artifactId>
    <version>1.15.0</version>
    <configuration>
        <targetClasses>
            <param>com.tupackage.*</param>
        </targetClasses>
        <targetTests>
            <param>com.tupackage.*Test</param>
        </targetTests>
    </configuration>
</plugin>
```

**Cómo ejecutarlo:**
1. Abre la terminal integrada con `Ctrl+\``.
2. Ejecuta: `mvn pitest:mutationCoverage`
3. PIT genera un reporte HTML en `target/pit-reports/`. Abre `index.html` en el navegador.

**Cómo interpretar el reporte:**

| Indicador | Color | Significado |
| :--- | :---: | :--- |
| **Killed** | 🟢 Verde | Mutante detectado — prueba eficaz |
| **Survived** | 🔴 Rojo | Mutante no detectado — prueba débil |
| **No coverage** | ⚪ Gris | Línea sin ninguna prueba asociada |

**Flujo de resolución:**
1. Identifica los mutantes **Survived** (rojo) en el reporte HTML.
2. Para cada uno, determina: ¿qué cambio exacto hizo PIT en tu código?
3. Diseña una prueba que falle cuando ese cambio esté presente.
4. Re-ejecuta PIT y verifica que el Mutation Score mejoró.

**Actividad mientras ves el video:** Cuando aparezca un mutante superviviente, pausa el video y escribe la prueba que lo eliminaría antes de ver la solución.

---

## 🖼️ Material de Apoyo Visual

{: .highlight }
> 🚀 **Diapositivas de la Unidad:** [Presentación Interactiva - Análisis en VS Code](https://fis-eci.github.io/software-foundations-eci-slides/Analisis-VSC-presentation.html#1)

---

## 🎥 Práctica Guiada: Análisis Completo en VS Code

### 🔬 Los Cuatro Análisis en Acción sobre `CuentaBancaria`
¿Cómo ejecutar SonarLint, PMD, JaCoCo y PIT sobre tu proyecto Java en VS Code? En este tutorial ejecutamos el ciclo completo de análisis y resolvemos los incidentes encontrados.

* **Caso de estudio:** Clase `CuentaBancaria` con incidentes reales de los cuatro análisis.
* **Conceptos aplicados:** Lectura de reportes, selección y justificación de incidentes, solución y análisis comparativo final.

📺 **Ver el Video:** [Análisis de Software en VS Code: SonarLint, PMD, JaCoCo y PIT en Acción](https://youtu.be/N29OODjHMUE)

---

## 📋 S4: Práctica — Cierre del Proyecto Inicial en VS Code

### Paso 1: Abrir el Proyecto en VS Code

1. `File → Open Folder` → selecciona la carpeta raíz de tu proyecto.
2. VS Code detectará automáticamente el proyecto Java con **Extension Pack for Java** instalado.
3. Verifica que no haya errores en la vista **Problems** (`Ctrl+Shift+M`).

{: .important }
> Si VS Code no detecta el proyecto, asegúrate de que la carpeta raíz contenga los archivos `.java` o la estructura de paquetes (`src/com/tupackage/`). El Extension Pack for Java necesita ver la estructura de carpetas para construir el proyecto.

### Paso 2: Compilación, Documentación y Ejecución

| Acción | Cómo hacerlo en VS Code |
| :--- | :--- |
| **Compilar** | Automático al guardar (con `java.autobuild.enabled: true`) |
| **Documentar** | Terminal integrada: `javadoc -d docs src/*.java` |
| **Ejecutar** | Clic en `▶ Run` sobre el método `main`, o presiona `F5` |
| **Probar (JUnit)** | Panel de Testing (🧪) → **Run All Tests** |

Si tu proyecto no tiene un método `main`, agrégalo en la clase `Contest` (o equivalente):

```java
public static void main(String[] args) {
    Contest contest = new Contest();
    contest.simular();
}
```

### Paso 3: Ciclo de Análisis para cada Herramienta

Para cada uno de los cuatro análisis, sigue el protocolo de cinco etapas:

| Etapa | Actividad |
| :--- | :--- |
| **(i) Análisis inicial** | Ejecuta la herramienta y registra la lista completa de incidentes |
| **(ii) Interpretación** | Lee cada incidente y clasifícalo por prioridad o impacto |
| **(iii) Selección** | Elige el incidente más relevante y justifica tu elección por escrito |
| **(iv) Solución** | Aplica la corrección y documenta el razonamiento detrás de ella |
| **(v) Análisis final** | Re-ejecuta la herramienta y compara el estado inicial vs. el final |

{: .highlight }
> **Entregable esperado:** Para cada análisis, documenta: tabla de incidentes inicial, incidente seleccionado con justificación, código antes y después de la corrección, y tabla de incidentes final.

---

## 📚 Verificación y Recursos Adicionales

{: .warning }
> **Pregunta de Verificación:** Tienes la configuración Vainilla activa pero VS Code sigue mostrando sugerencias de métodos Java. ¿Qué ajuste en `settings.json` es específico para Java y va más allá de la configuración general del editor? ¿Por qué existe una configuración separada para Java y no basta con desactivar `editor.quickSuggestions`?

**Recursos:**
* 💻 [Guía VS Code Vainilla — Configuración completa](../VSCode-Vanila/)
* 📘 [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)
* 📘 [Coverage Gutters](https://marketplace.visualstudio.com/items?itemName=ryanluker.vscode-coverage-gutters)
* 📘 [PMD para VS Code](https://marketplace.visualstudio.com/items?itemName=chuckjonas.apex-pmd)
* 📘 [PIT Mutation Testing](https://pitest.org/)
* 📘 [JaCoCo — Java Code Coverage](https://www.jacoco.org/)
