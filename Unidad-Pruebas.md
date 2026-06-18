---
layout: default
title: "Unidad 2: Pruebas"
nav_order: 4
permalink: /Unidad-Pruebas/
---

# 🧪 Unidad 2: Pruebas Unitarias (JUnit)
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **DOPO (Desarrollo Orientado por Objetos)** 🎓

{: .note }
> **Resultados de Aprendizaje:** Al finalizar esta unidad, comprenderás los conceptos principales de las pruebas de unidad, aplicarás buenas prácticas de diseño de pruebas y utilizarás **JUnit** dentro del entorno **BlueJ** para asegurar la calidad de tus proyectos.

---

## 📖 R1: Fundamentos y Conceptos

### ¿Qué es una prueba de unidad?
Una prueba de unidad es un fragmento de código diseñado para evaluar la porción más pequeña e independiente de un sistema (generalmente un **método** de una clase). El objetivo es verificar que esa unidad funcional opere exactamente como se espera, aislada del resto del sistema.

### ¿Por qué son vitales en la ingeniería de software?
* 🛡️ **Previenen regresiones:** Aseguran que el código nuevo no rompa el código viejo.
* 📝 **Documentación viva:** Una buena prueba explica cómo debe usarse una clase mejor que cualquier manual.
* 🧘 **Confianza al refactorizar:** Permiten mejorar el código interno sin miedo a introducir errores ocultos.

### Nomenclatura Profesional: El Estándar del Curso
Para que las pruebas sean legibles, en **DOPO** utilizamos estrictamente la convención de nombres basada en acciones y condiciones:
* `shouldXWhenY` (Debería hacer [X] cuando ocurra [Y])
* `shouldNotXWhenY` (NO Debería hacer [X] cuando ocurra [Y])

> **Ejemplo:** `shouldAumentarSaldoWhenConsignarMontoValido()`

### Introducción a BDD (Behavior-Driven Development)
BDD se enfoca en el *comportamiento* esperado del usuario. Estructuramos el interior de nuestras pruebas en tres pasos lógicos:
1. **Given (Dado):** El estado inicial (Ej. *Dado un saldo de 0*).
2. **When (Cuando):** La acción o estímulo (Ej. *Cuando consigno 100*).
3. **Then (Entonces):** El resultado esperado (Ej. *Entonces el saldo es 100*).

### Tipos de Casos de Prueba
No basta con probar que el programa funciona cuando todo sale bien. Debemos contemplar:

| Tipo de Caso | Descripción | Ejemplo (`CuentaBancaria`) |
| :--- | :--- | :--- |
| **Feliz / Nominal** | Entradas válidas, el usuario hace lo correcto. | Consignar $100,000 COP. |
| **Caso de Borde** | Valores límite (ceros, máximos, mínimos). | Consignar exactamente $0 COP. |
| **Caso de Error** | Entradas inválidas que el sistema debe rechazar. | Consignar un monto negativo (-$50,000). |

---

## ✅ R2: Buenas Prácticas (Estándares de Diseño)

Para incluir pruebas unitarias en un proyecto profesional, seguimos **tres reglas de oro inquebrantables**:

{: .important }
> 1. **Code the unit test first (TDD):** Escribe la prueba *antes* que el código funcional. La prueba fallará primero (Rojo), luego escribes el código para que pase (Verde) y finalmente mejoras el código (Refactor).
> 2. **All code must have unit tests:** Ninguna clase de lógica de negocio se considera terminada si no tiene su respectiva clase `Test` que valide sus métodos.
> 3. **When a bug is found, tests are created:** Si un usuario reporta un error, **no lo arregles de inmediato**. Primero crea una prueba que replique el error, y luego modifica tu código hasta que esa prueba pase exitosamente.

---

## 💻 R3: Herramienta (JUnit en BlueJ)

### ¿Qué es JUnit?
Es el framework estándar de la industria para escribir y ejecutar pruebas repetibles en Java. Proporciona anotaciones (como `@Test`) y métodos de aserción (como `assertEquals`) para verificar resultados.

### Entorno: BlueJ
BlueJ tiene una integración visual excelente con JUnit. Las clases de prueba se identifican con un **color verde** y permiten ejecutar los casos con un solo clic, mostrando una barra de progreso que nos indica si nuestro código es seguro (Verde) o tiene fallos (Rojo).

---

## 🖼️ Material de Apoyo Visual

Refuerza los conceptos de TDD, BDD y el entorno de BlueJ con el siguiente material gráfico:

{: .highlight }
> 🚀 **Diapositivas de la Unidad:** [Presentación Interactiva - Pruebas Unitarias](https://fis-eci.github.io/software-foundations-eci-slides/PruebasUnitarias-presentation.html#1)

---

## 🎥 Práctica Guiada: El Reto de la Cuenta Bancaria

¿Tu código realmente hace lo que crees que hace? En este tutorial en video, aplicamos toda la teoría anterior utilizando el ejemplo de una `CuentaBancaria`.

📺 **Ver el Video Tutorial:** [Pruebas Unitarias con JUnit en BlueJ (DOPO)](https://youtu.be/UAhh8al2eo8)

### ⏳ Contenido del Video
* Configuración de JUnit en BlueJ: Creando nuestra primera "Test Class".
* **Paso 1:** TDD en acción (Escribiendo la prueba primero).
* **Paso 2:** El Caso Feliz — Probando una consignación válida.
* **Paso 3:** Casos de Borde — ¿Qué pasa si consignamos 0?
* **Paso 4:** Cazando un Bug — Replicando un error de monto negativo.
* Buenas prácticas: Manteniendo el código limpio y probado.

### 📝 Ejemplo de Código BDD (Visto en el video)
Así luce una prueba perfecta aplicando la nomenclatura y la estructura BDD:

```java
import static org.junit.Assert.*;
import org.junit.Test;

public class CuentaBancariaTest {

    @Test
    public void shouldAumentarSaldoWhenConsignarMontoValido() {
        // 1. Given (Dado un saldo inicial de 0)
        CuentaBancaria cuenta = new CuentaBancaria();
        
        // 2. When (Cuando consigno 100)
        cuenta.consignar(100.0);
        
        // 3. Then (Entonces el saldo debe ser 100)
        // Nota: 0.01 es el margen de error para comparar decimales (doubles)
        assertEquals(100.0, cuenta.getSaldo(), 0.01); 
    }
}
```

---

## 📚 Verificación y Recursos Adicionales

{: .highlight }
> **Reto Práctico:** Revisa el código del video y crea la prueba para el método `retirar()`. ¿Qué tipo de aserción usarías para el caso de error donde el usuario intenta retirar más dinero del que tiene en la cuenta?

**Enlaces de interés:**
* 📘 [Documentación oficial de JUnit 4/5](https://junit.org/)
* 🧩 [Guía de BlueJ para Unit Testing](https://www.bluej.org/)