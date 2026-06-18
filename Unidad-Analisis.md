---
layout: default
title: "Unidad 4: Análisis de Software"
nav_order: 6
permalink: /Unidad-Analisis/
has_children: true
---

# 🔬 Unidad 4: Análisis de Software
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **DOPO (Desarrollo Orientado por Objetos)** 🎓

{: .note }
> **Resultados de Aprendizaje:** Al finalizar esta unidad, podrás (1) explicar los conceptos y estrategias principales del análisis de software, (2) interpretar los resultados del análisis y resolver los incidentes evidenciados, y (3) utilizar herramientas profesionales para evaluar y mejorar la calidad del software.

---

## 🧭 Propósito de la Unidad

El análisis de software nos permite tomar decisiones informadas sobre la calidad de nuestro código, pero **no sustituye el juicio del ingeniero de software**. Existen dos grandes categorías:

* **Análisis estático:** Permite anticipar problemas estructurales *sin ejecutar el programa*.
* **Análisis dinámico:** Valida el comportamiento real del software *durante su ejecución*.

Juntos, responden cuatro preguntas fundamentales sobre tu proyecto:

| # | Pregunta | Herramienta | Tipo |
| :---: | :--- | :---: | :---: |
| 1 | ¿El software cumple los principios básicos de buen diseño? | **SonarLint** | Estático |
| 2 | ¿El código no presenta defectos potenciales ni malas prácticas? | **PMD** | Estático |
| 3 | ¿Qué código está realmente siendo probado? | **JaCoCo** | Dinámico |
| 4 | ¿Las pruebas realmente detectan errores? | **PIT (Mutación)** | Dinámico |

---

## 🧠 S1: Teoría — Los Cuatro Pilares del Análisis

### ¿Qué problema resuelve el análisis de software?

Un código que compila y parece funcionar puede esconder graves problemas: acoplamiento excesivo, baja cobertura de pruebas, o bugs que solo aparecen bajo condiciones específicas. El análisis de software provee mecanismos sistemáticos para **detectar, medir y resolver** estos problemas antes de que lleguen a producción.

### Análisis Estático

El análisis estático examina el código fuente *sin ejecutarlo*. Actúa como un revisor experto que lee tu código y señala problemas estructurales o de estilo.

#### 🔵 Análisis de Diseño — SonarLint

SonarLint evalúa si el código respeta principios de buen diseño orientado a objetos.

**Indicadores clave:**

| Indicador | Descripción | Riesgo si se ignora |
| :--- | :--- | :--- |
| **Code Smells** | Patrones de código que no son errores pero dificultan el mantenimiento | Deuda técnica acumulada |
| **Duplicación** | Bloques de código repetidos en diferentes lugares | Cambios inconsistentes al refactorizar |
| **Complejidad Cognitiva** | Métodos difíciles de entender por su estructura anidada | Dificultad para depurar y mantener |
| **Acoplamiento excesivo** | Dependencias innecesarias entre clases | Fragilidad ante cualquier cambio |

#### 🟠 Análisis de Calidad — PMD

PMD detecta defectos potenciales y malas prácticas conocidas que SonarLint podría pasar por alto.

**Indicadores clave:**

| Indicador | Descripción | Ejemplo |
| :--- | :--- | :--- |
| **Variables no utilizadas** | Variables declaradas pero nunca referenciadas | `int temp = 0;` sin usar |
| **Catch vacío** | Excepciones capturadas pero no manejadas | `catch(Exception e) {}` |
| **Comparación con `==`** | Uso de `==` en vez de `.equals()` para objetos String | `if (nombre == "Juan")` |
| **Constructores innecesarios** | Constructor por defecto explícito cuando no se necesita | Código redundante y confuso |

### Análisis Dinámico

El análisis dinámico observa el comportamiento del software *durante su ejecución real*, apalancándose en la suite de pruebas unitarias ya construida.

#### 🟢 Pruebas de Cobertura — JaCoCo

JaCoCo mide qué porcentaje del código es efectivamente ejecutado por las pruebas.

**Indicadores clave:**

| Indicador | Descripción | Meta recomendada |
| :--- | :--- | :---: |
| **Line Coverage** | % de líneas ejecutadas al menos una vez | > 80% |
| **Branch Coverage** | % de ramas (`if`/`else`) probadas en ambas direcciones | > 70% |
| **Method Coverage** | % de métodos invocados durante las pruebas | > 90% |

{: .warning }
> **¡Cuidado con la trampa!** Una cobertura del 100% no garantiza pruebas de calidad. El código puede ejecutarse sin que las aserciones detecten errores reales. Es solo el punto de partida.

#### 🔴 Pruebas de Mutación — PIT

PIT va un paso más allá: introduce errores artificiales ("mutantes") en el código para verificar que las pruebas los detecten.

**¿Cómo funciona?**
1. PIT modifica automáticamente tu código: cambia `>` por `>=`, suma por resta, `true` por `false`, etc.
2. Ejecuta la suite de pruebas contra cada versión mutada.
3. Si una prueba **falla**, el mutante fue "matado" ✅ — las pruebas son eficaces.
4. Si **ninguna prueba falla**, el mutante "sobrevivió" ❌ — hay un hueco en la suite de pruebas.

**Indicadores clave:**

| Indicador | Descripción |
| :--- | :--- |
| **Mutation Score** | % de mutantes eliminados sobre el total generado |
| **Survived Mutants** | Mutantes no detectados — revelan pruebas débiles |
| **Killed Mutants** | Mutantes detectados por al menos una prueba |

---

## 🧪 S2: Práctica por Ejemplo — El Caso `CuentaBancaria`

Usamos la clase `CuentaBancaria` (familiar de la [Unidad 2: Pruebas](../Unidad-Pruebas/)) para ilustrar los cuatro análisis en acción. El flujo siempre sigue el mismo patrón: **indicadores → selección de incidente → justificación → solución → análisis final**.

### El código bajo análisis

```java
public class CuentaBancaria {
    private double saldo;
    private String tipo = "ahorros";

    public void consignar(double monto) {
        if (monto > 0) {
            saldo = saldo + monto;
        }
    }

    public void retirar(double monto) {
        if (monto > 0 & monto <= saldo) {   // Bug sutil: '&' en vez de '&&'
            saldo = saldo - monto;
        }
    }

    public double getSaldo() { return saldo; }

    public String getTipo() { return tipo; }

    private void metodoInterno() {           // Método privado nunca llamado
        System.out.println("debug");
    }
}
```

### 🔵 Análisis 1: SonarLint — Incidente Seleccionado

El método `retirar` usa `&` (AND bit a bit) en lugar de `&&` (AND lógico).

* **¿Por qué es relevante?** Ilustra cómo un error de diseño sutil pasa la compilación pero viola las convenciones del lenguaje y puede generar comportamientos inesperados.
* **¿Qué principio ilustra?** Claridad de intención en operadores lógicos (Code Smell de nivel mayor).
* **Alternativa de solución:** Reemplazar `&` por `&&` en la condición de `retirar`.

### 🟠 Análisis 2: PMD — Incidente Seleccionado

El método privado `metodoInterno()` nunca es referenciado desde ninguna parte de la clase.

* **¿Por qué es relevante?** El código muerto aumenta el tamaño del proyecto y confunde a quien lo mantiene.
* **¿Qué principio ilustra?** YAGNI (*You Aren't Gonna Need It*) — no mantener código que no cumple ninguna función.
* **Alternativa de solución:** Eliminar `metodoInterno()` por completo.

### 🟢 Análisis 3: JaCoCo — Incidente Seleccionado

El bloque implícito "no se retira" de `retirar` (cuando `monto <= 0`) nunca es cubierto por las pruebas actuales.

* **¿Por qué es relevante?** Sin probar el rechazo de montos negativos, un bug en esa rama pasaría desapercibido.
* **¿Qué principio ilustra?** Branch coverage — toda decisión lógica debe tener pruebas en ambos sentidos.
* **Alternativa de solución:** Agregar el caso `shouldNotRetirarWhenMontoNegativo()`.

### 🔴 Análisis 4: PIT — Incidente Seleccionado

PIT genera el mutante `monto > 0` → `monto >= 0` en `consignar`, y la prueba existente **no lo detecta** porque nunca prueba el caso `monto == 0`.

* **¿Por qué es relevante?** Revela que la cobertura de líneas puede ser alta pero las pruebas siguen siendo débiles ante variaciones límite.
* **¿Qué principio ilustra?** La diferencia entre *código ejecutado* (JaCoCo) y *comportamiento realmente verificado* (PIT).
* **Alternativa de solución:** Agregar `shouldNotConsignarWhenMontoCero()`.

---

## 🛠️ Elige tu Entorno de Desarrollo

Los cuatro análisis se pueden ejecutar tanto en **Eclipse** como en **Visual Studio Code**. Selecciona el entorno que corresponde a tu configuración:

{: .highlight }
> ### ☕ [Eclipse — Entorno Principal DOPO](../Unidad-Analisis-Eclipse/)
> Instalación de Eclipse IDE, plugins SonarLint, PMD, EclEmma y Pitclipse. Flujo completo desde la importación del proyecto BlueJ hasta el análisis final.

{: .highlight }
> ### 💻 [Visual Studio Code — Alternativa Moderna](../Unidad-Analisis-VSC/)
> Configuración VS Code según la [Guía VS Code Vainilla](../VSCode-Vanila/) con extensiones. Para estudiantes que prefieren un entorno integrado moderno con programación consciente.

---

## 📚 Verificación y Recursos Adicionales

{: .warning }
> **Pregunta de Verificación:** Un compañero tiene 95% de cobertura de líneas (JaCoCo) pero solo 40% de Mutation Score (PIT). ¿Qué concluyes sobre la calidad de sus pruebas? ¿Qué tipo de casos de prueba le recomendarías agregar y por qué?

**Principio para recordar:** Los resultados del análisis apoyan la toma de decisiones, pero **no sustituyen el juicio del ingeniero de software**. Siempre pregúntate: ¿este incidente realmente importa en el contexto de mi proyecto?

**Recursos de referencia:**
* 📘 [Documentación SonarLint](https://www.sonarsource.com/products/sonarlint/)
* 📘 [Reglas PMD para Java](https://pmd.github.io/latest/pmd_rules_java.html)
* 📘 [JaCoCo — Java Code Coverage](https://www.jacoco.org/)
* 📘 [PIT Mutation Testing](https://pitest.org/)
