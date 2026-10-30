---
layout: default
title: "📝 Bitácora de Cambios"
nav_order: 10
permalink: /Changelog/
---

# 📝 Bitácora de Cambios (Changelog)
> **Seguimiento de Actualizaciones del Objeto de Aprendizaje**

Todos los cambios notables en este repositorio de monitoría serán documentados en esta página.

---

## [2.1.0] - 2026-10-30
### ✨ Añadido
- **Unidad 5: Diseño con Astah** con página principal y dos sub-unidades independientes con el mismo propósito:
  - **MYSD · Empresa comercializadora:** diseño conceptual (general y extendido), lógico (Modelo Mini, 9 tablas) y físico (datos, componentes `PC_` y actores `PA_`), con el script SQL de tablas y claves y las consultas operativa y gerencial.
  - **DOPO · Batalla N:** diagrama de paquetes, clases de presentación y dominio en cuatro versiones, mapa de memoria y un diagrama de secuencia con su código Java para cada método de `Flota`.
- **Presentaciones interactivas** de la unidad (17 y 22 diapositivas) con pausas de aprendizaje activo: *Reproduce en Astah* y *Resuelve y contrasta* (soluciones veladas).
- Diagramas UML en `assets/diagramas/`, listos para reproducir en Astah.

## [2.0.0] - 2026-10-29
### ✨ Añadido
- **Identidad visual institucional**: logo oficial de la Escuela Colombiana de Ingeniería Julio Garavito en la wiki, en la portada de cada presentación y como emblema en todas las diapositivas.
- **Modo claro y modo oscuro** en la wiki con botón de cambio; respeta la preferencia del sistema y recuerda la elección del estudiante.
- **Página de inicio renovada** con portada y tarjetas de acceso directo a las cuatro unidades.
- **Sistema de diseño de las presentaciones** (`design-system/` en el repositorio de diapositivas): tipografía unificada (Inter + JetBrains Mono), animaciones de entrada, esfera 3D en las portadas, vista general de diapositivas (`G`), modo inmersivo y navegación táctil.
- **Nota sobre mutantes equivalentes** en la Unidad 4 (PIT).

### 🔧 Modificado
- Rediseño visual completo de las 75 diapositivas de las seis presentaciones, conservando su contenido.
- Tema de la wiki: tipografía, tablas, bloques de código, callouts y navegación lateral rediseñados.
- La sección de navegación de la Unidad 3 se llama ahora **"Unidad 3: Bases de Datos"** (antes "Oracle SQL"), ya que agrupa Oracle y PostgreSQL.

### 🐛 Corregido
- **Unidad 4 (PIT):** el mutante de ejemplo `monto > 0 → monto >= 0` en `consignar` es equivalente (ninguna prueba puede matarlo). Se reemplazó por `monto <= saldo → monto < saldo` en `retirar`, que sí se elimina con `shouldDejarSaldoEnCeroWhenRetirarTodoElSaldo()`.
- **PostgreSQL en VS Code:** el atajo de SQLTools para ejecutar la consulta seleccionada es `Ctrl+E Ctrl+E` (`Cmd+E Cmd+E` en macOS), no `Ctrl+Shift+E`.
- **Pregunta de verificación de PIT (Eclipse):** el mutante del reto ahora corresponde al código del ejemplo: `monto <= saldo → monto < saldo` en `retirar()`.
- **JaCoCo en VS Code:** el reporte `jacoco.xml` lo genera Maven (`mvn test` con el plugin `jacoco-maven-plugin`), no el panel de Testing; se agregó la configuración del plugin.
- **Presentaciones:** aserciones JUnit (`assertEquals` en lugar de `assert(...)`), correo de contacto unificado a `fis@escuelaing.edu.co` y acceso a granate sin VPN consistente en la presentación de Oracle.

## [1.3.0] - 2026-06-18
### ✨ Añadido
- **Unidad 4: Análisis de Software** con página principal, sub-unidad Eclipse (SonarLint, PMD, EclEmma, Pitclipse) y sub-unidad VS Code (enfocada en DOPO).
- **Guía: VS Code Vainilla** — página transversal con extensiones, configuración consciente sin IA y `settings.json` para DOPO y MYSD.
- **Unidad 3** reestructurada en dos sub-unidades: Oracle SQL Developer (Granate + XE + videos) y PostgreSQL en VS Code (SQLTools + flujo Vainilla).
- **Recursos**: secciones de análisis de software y PostgreSQL con referencias completas.

### 🔧 Modificado
- **Home y README**: índice actualizado con Unidad 4, Guía VS Code Vainilla y nueva estructura de Unidad 3.
- `nav_order` reordenado para acomodar las nuevas páginas.

## [1.2.0] - 2026-03-14
### ✨ Añadido
- **Unidad 3: Oracle SQL**: Guía completa de conexión remota (Granate) y local (XE).
- **Soporte para VS Code**: Inclusión de la extensión oficial de Oracle SQL Developer como alternativa ligera.
- **Recursos de MYSD**: Actualización de la biblioteca con enlaces a VPN institucional y descargas de Oracle.
- **Integración de diapositivas**: Interacción de páginas web **Canva** en las Unidades 1 (CVS) y 2 (Pruebas).

## [1.1.0] - 2026-03-08
### ✨ Añadido
- Nueva **Unidad 2: Pruebas Unitarias** con enfoque en TDD y BDD.
- Video tutorial práctico: "Pruebas Unitarias con JUnit en BlueJ (Caso Cuenta Bancaria)".
- Página de **Recursos** con bibliografía técnica actualizada.
- Footers institucionales con el logo de la Escuela en todas las páginas.

## [1.0.0] - 2026-02-26
### ✨ Añadido
- Lanzamiento inicial de la Wiki.
- **Unidad 1: Control de Versiones** basada en la teoría de Grafos Dirigidos Acíclicos.
- Videos prácticos de Git para los entornos de **DOPO** (Java) y **MYSD** (SQL).
- Configuración del `.gitignore` estándar para la línea de fundamentos.

---

### 💡 Nota para el Monitor
*Para mantener esta página, usa el formato [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Ayuda a los profesores a ver tu progreso constante en el material.*
