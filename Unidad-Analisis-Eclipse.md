---
layout: default
title: "Análisis en Eclipse"
parent: "Unidad 4: Análisis de Software"
nav_order: 1
permalink: /Unidad-Analisis-Eclipse/
---

# ☕ S3 & S4: Análisis de Software en Eclipse IDE
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **DOPO (Desarrollo Orientado por Objetos)** 🎓

{: .note }
> **Prerrequisito:** Haber estudiado la teoría y el ejemplo de la [Unidad 4 — Página Principal](../Unidad-Analisis/). Esta página cubre exclusivamente la instalación del entorno y la ejecución de los cuatro análisis dentro de **Eclipse IDE**.

---

## 🔭 S3: El Entorno Profesional — Eclipse IDE

### ¿Qué es Eclipse?

Eclipse es un **IDE (Integrated Development Environment)** de código abierto, ampliamente usado en la industria y en la academia para el desarrollo de software en Java. A diferencia de BlueJ —orientado a la enseñanza introductoria—, Eclipse está diseñado para proyectos de escala real y ofrece integración directa con herramientas de análisis de software de nivel profesional.

**¿Por qué Eclipse para este curso?**
* Integra de forma nativa los plugins de análisis estático y dinámico requeridos.
* Fuerza al estudiante a comprender la estructura real de un proyecto Java (classpath, build path, dependencias).
* Es el entorno donde se ejecutan los proyectos finales de DOPO.

---

## ⚙️ Instalación y Configuración de Eclipse

### Paso 1: Instalar Eclipse IDE

1. Descarga **Eclipse IDE for Java Developers** desde [eclipse.org/downloads](https://www.eclipse.org/downloads/).
2. Ejecuta el instalador y selecciona **"Eclipse IDE for Java Developers"**.
3. Acepta la ruta predeterminada y completa la instalación.
4. En el primer lanzamiento, selecciona o crea un **Workspace** (carpeta donde vivirán tus proyectos).

### Paso 2: Instalar los Plugins de Análisis

Accede desde el menú: **Help → Eclipse Marketplace...**

| Plugin | Búsqueda en Marketplace | Propósito |
| :--- | :--- | :--- |
| **SonarLint** | `SonarLint` | Análisis de diseño en tiempo real |
| **PMD Eclipse Plugin** | `PMD Eclipse Plugin` | Análisis de calidad y malas prácticas |
| **EclEmma (JaCoCo)** | `EclEmma` | Pruebas de cobertura integradas |
| **Pitclipse (PIT)** | `Pitclipse` | Pruebas de mutación |

{: .important }
> Después de instalar cada plugin, Eclipse solicitará **reiniciarse**. Acepta siempre para que el plugin quede activo correctamente. Instala uno a uno para evitar conflictos.

---

## 🚀 Flujo de Trabajo Básico en Eclipse

Antes de analizar, es necesario dominar las operaciones fundamentales del entorno:

| Acción | Cómo hacerlo en Eclipse |
| :--- | :--- |
| **Compilar** | Automático al guardar. Manual: `Project → Build Project` |
| **Documentar** | `Project → Generate Javadoc...` → selecciona la carpeta de destino |
| **Ejecutar** | Clic derecho sobre la clase con `main` → `Run As → Java Application` |
| **Probar (JUnit)** | Clic derecho sobre la clase `Test` → `Run As → JUnit Test` |

---

## 🔬 S3: Los Cuatro Análisis en Eclipse

### 🔵 Análisis 1: SonarLint — Análisis de Diseño

SonarLint funciona **en tiempo real** dentro de Eclipse: subraya problemas directamente en el editor mientras escribes, sin necesidad de ejecutar ningún comando adicional.

**Cómo activar la vista:**
1. Menú `Window → Show View → Other → SonarLint → On-The-Fly Issues`.
2. La vista muestra cada incidente con: tipo, severidad, descripción y número de línea.

**Flujo de resolución:**

| Paso | Acción |
| :---: | :--- |
| 1 | Identifica el incidente con mayor severidad en la vista SonarLint |
| 2 | Haz clic en el incidente para navegar a la línea afectada |
| 3 | Lee la descripción de la regla violada y el ejemplo de corrección |
| 4 | Aplica la solución o justifica por escrito por qué no aplica en tu contexto |
| 5 | Verifica que el incidente desaparezca de la vista al guardar el archivo |

**Actividad mientras ves el video:** Pausa en el momento en que aparece el primer incidente de SonarLint e intenta predecir cuál será la solución antes de ver la corrección aplicada.

### 🟠 Análisis 2: PMD — Análisis de Calidad

**Cómo ejecutarlo:**
1. Clic derecho sobre el proyecto en el **Package Explorer**.
2. Selecciona **PMD → Check Code**.
3. Se abrirá la vista **PMD Violations** con todos los incidentes clasificados.

**Cómo interpretar la prioridad:**

| Prioridad | Color | Significado | Acción recomendada |
| :---: | :---: | :--- | :--- |
| **1** | 🔴 Rojo | Problema crítico — posible bug real | Resolver obligatoriamente |
| **2** | 🟠 Naranja | Problema importante de calidad | Resolver o justificar explícitamente |
| **3 – 5** | 🟡 Amarillo | Problema menor o de estilo | Evaluar según contexto del proyecto |

**Flujo de resolución:**

| Paso | Acción |
| :---: | :--- |
| 1 | Ordena la vista PMD Violations por columna **P** (Prioridad) |
| 2 | Selecciona el incidente de mayor prioridad |
| 3 | Documenta: *¿Por qué este incidente es relevante? ¿Qué principio viola?* |
| 4 | Aplica la corrección en el código |
| 5 | Re-ejecuta **PMD → Check Code** y confirma que el incidente desapareció |

**Actividad mientras ves el video:** Antes de ver la solución del monitor, escribe en papel tu propuesta de corrección para el incidente de mayor prioridad.

### 🟢 Análisis 3: EclEmma (JaCoCo) — Pruebas de Cobertura

**Cómo ejecutarlo:**
1. Clic derecho sobre la clase `Test` en el Package Explorer.
2. Selecciona **Coverage As → JUnit Test**.
3. Eclipse ejecuta las pruebas y colorea el código fuente automáticamente:

| Color | Significado |
| :---: | :--- |
| 🟢 Verde | Línea ejecutada completamente por las pruebas |
| 🔴 Rojo | Línea **no** ejecutada — cobertura pendiente |
| 🟡 Amarillo | Rama parcialmente cubierta (ej. solo el `if` pero no el `else`) |

**Cómo interpretar el reporte detallado:**
1. Abre la vista **Coverage** desde `Window → Show View → Other → Java → Coverage`.
2. Revisa los porcentajes de cobertura por clase y por método.
3. Identifica el método con menor cobertura de **ramas** (Branch Coverage).
4. Diseña y agrega la prueba faltante para cubrir la rama roja o amarilla.

**Actividad mientras ves el video:** Cuando aparezca el reporte de cobertura, identifica las líneas amarillas antes de que el monitor las señale. Propón mentalmente qué caso de prueba falta.

### 🔴 Análisis 4: Pitclipse (PIT) — Pruebas de Mutación

**Cómo ejecutarlo:**
1. Clic derecho sobre el proyecto en el Package Explorer.
2. Selecciona **PIT → PIT Mutation Test**.
3. El proceso tarda más que los otros análisis (varios minutos según el tamaño del proyecto).
4. Al finalizar, Eclipse abre un reporte HTML en el navegador interno y la vista **PIT Summary**.

**Cómo interpretar el reporte:**

| Indicador | Color | Significado |
| :--- | :---: | :--- |
| **Killed** | 🟢 Verde | Mutante detectado por al menos una prueba — prueba eficaz |
| **Survived** | 🔴 Rojo | Ninguna prueba detectó el cambio artificial — prueba débil |
| **No coverage** | ⚪ Gris | La línea mutada no tiene ninguna prueba asociada |

**Flujo de resolución:**

| Paso | Acción |
| :---: | :--- |
| 1 | Abre el reporte HTML y navega a los mutantes **Survived** (rojo) |
| 2 | Para cada mutante, identifica: ¿qué cambio hizo PIT en tu código? |
| 3 | Diseña una prueba que falle exactamente cuando ese cambio esté presente |
| 4 | Agrega la prueba a la clase `Test` con la nomenclatura `shouldXWhenY` |
| 5 | Re-ejecuta PIT y verifica que el nuevo Mutation Score mejoró |

**Actividad mientras ves el video:** Cuando aparezca un mutante superviviente en pantalla, pausa el video e intenta escribir la prueba que lo eliminaría antes de ver la solución.

---

## 🖼️ Material de Apoyo Visual

{: .highlight }
> 🚀 **Diapositivas de la Unidad:** [Presentación Interactiva - Análisis en Eclipse](https://fis-eci.github.io/software-foundations-eci-slides/Analisis-Eclipse-presentation.html#1)

---

## 🎥 Práctica Guiada: Análisis Completo en Eclipse

### ☕ Instalación y Configuración de Eclipse para DOPO
¿Cómo dejar Eclipse listo con todos los plugins necesarios desde cero? En este tutorial instalamos el IDE y configuramos SonarLint, PMD, EclEmma y Pitclipse paso a paso.

* **Herramientas:** Eclipse IDE, Marketplace, plugins de análisis.
* **Conceptos aplicados:** Gestión del workspace, instalación de plugins, verificación de entorno.

📺 **Ver el Video:** *(Próximamente)*

### 🔬 Los Cuatro Análisis en Acción sobre `CuentaBancaria`
¿Cómo pasar de BlueJ a Eclipse y ejecutar el ciclo completo de análisis? En este tutorial importamos el proyecto, ejecutamos los cuatro análisis y resolvemos los incidentes encontrados.

* **Caso de estudio:** Clase `CuentaBancaria` con incidentes reales de SonarLint, PMD, JaCoCo y PIT.
* **Conceptos aplicados:** Lectura de reportes, selección y justificación de incidentes, solución y análisis final comparativo.

📺 **Ver el Video:** *(Próximamente)*

---

## 📋 S4: Práctica — Cierre del Proyecto Inicial

Este es el flujo completo que seguirás al llevar tu proyecto de BlueJ a Eclipse para el análisis final de curso.

### Paso 1: Importar el Proyecto de BlueJ

1. En Eclipse: `File → Import → General → Existing Projects into Workspace`.
2. Selecciona **"Select root directory"** y navega a la carpeta raíz de tu proyecto BlueJ.
3. Marca el proyecto detectado y haz clic en **Finish**.
4. Verifica en la vista **Problems** que no haya errores de compilación en rojo.

{: .important }
> Si Eclipse muestra errores de compilación al importar, verifica que el **JDK** configurado sea compatible con el de BlueJ. Ve a `Window → Preferences → Java → Installed JREs` y añade el JDK 11 o 17.

### Paso 2: Compilación, Documentación y Ejecución

1. **Compilar:** Verifica que no haya errores en la vista **Problems** (pestaña inferior de Eclipse).
2. **Documentar:** Revisa que todas las clases tienen Javadoc en sus métodos públicos. Genera el Javadoc: `Project → Generate Javadoc → Finish`.
3. **Ejecutar:** Si tu proyecto no tiene método `main`, agrégalo en la clase `Contest` (o equivalente):

```java
public static void main(String[] args) {
    Contest contest = new Contest();
    contest.simular();
}
```

4. Clic derecho sobre la clase con `main` → `Run As → Java Application`. Verifica en la consola que el output es el esperado.

### Paso 3: Ciclo de Análisis para cada Herramienta

Para cada uno de los cuatro análisis, sigue este protocolo de cinco etapas:

| Etapa | Actividad |
| :--- | :--- |
| **(i) Análisis inicial** | Ejecuta la herramienta y registra la lista completa de incidentes |
| **(ii) Interpretación** | Lee cada incidente y clasifícalo por prioridad o impacto |
| **(iii) Selección** | Elige el incidente más relevante y justifica tu elección por escrito |
| **(iv) Solución** | Aplica la corrección y documenta el razonamiento detrás de ella |
| **(v) Análisis final** | Re-ejecuta la herramienta y compara el estado inicial vs. el final |

{: .highlight }
> **Entregable esperado:** Para cada análisis, documenta: tabla de incidentes inicial, incidente seleccionado con justificación, código antes y después de la corrección, y tabla de incidentes final. Este es el insumo principal de la entrega de cierre del proyecto.

---

## 📚 Verificación y Recursos Adicionales

{: .warning }
> **Pregunta de Verificación:** Después de ejecutar PIT, encuentras que el mutante `saldo > 0 → saldo >= 0` en el método `retirar()` sobrevivió. ¿Qué prueba unitaria exacta agregarías para eliminarlo? Escríbela completa siguiendo la nomenclatura `shouldXWhenY` y la estructura BDD (Given/When/Then).

**Recursos:**
* 📘 [Eclipse IDE Downloads](https://www.eclipse.org/downloads/)
* 🔌 [SonarLint para Eclipse — Marketplace](https://marketplace.eclipse.org/content/sonarlint)
* 🔌 [PMD Eclipse Plugin — Marketplace](https://marketplace.eclipse.org/content/pmd-eclipse-plugin)
* 🔌 [EclEmma (JaCoCo) — Marketplace](https://marketplace.eclipse.org/content/eclemma-java-code-coverage)
* 🔌 [Pitclipse (PIT) — Marketplace](https://marketplace.eclipse.org/content/pitclipse)
