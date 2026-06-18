---
layout: default
title: "📝 Bitácora de Cambios"
nav_order: 9
permalink: /Changelog/
---

# 📝 Bitácora de Cambios (Changelog)
> **Seguimiento de Actualizaciones del Objeto de Aprendizaje**

Todos los cambios notables en este repositorio de monitoría serán documentados en esta página.

---

## [1.3.2] - 2026-06-18
### ✨ Añadido
- **Unidad 3 — Oracle SQL Developer** (`Unidad-SQL-Oracle.md`): sub-unidad con el contenido completo de Oracle SQL Developer — conexión a Granate, Oracle XE local, tabla de troubleshooting ampliada y los tres videos guiados. Corregido el bug de `Hostname` duplicado en la sección de Oracle XE.
- **Unidad 3 — PostgreSQL en VS Code** (`Unidad-SQL-Postgre-VSC.md`): nueva sub-unidad para trabajo con PostgreSQL desde VS Code usando SQLTools bajo filosofía Vainilla; incluye parámetros de conexión remota y local, flujo de trabajo consciente con scripts `.sql`, buenas prácticas en servidor compartido y sección de videos.

### 🔧 Modificado
- **Unidad 3 — Página Principal** (`Unidad-SQL.md`): convertida en página padre (`has_children: true`) con conceptos transversales (SGBD, parámetros de conexión, `.gitignore` para MYSD) y tabla de selección de entorno.
- **Guía VS Code Vainilla** (`VSCode-Vanila.md`): link de MYSD actualizado para apuntar a la nueva sub-unidad `Unidad-SQL-Postgre-VSC`.
- **Home y README**: actualizados con la nueva estructura de sub-unidades de Unidad 3.

## [1.3.1] - 2026-06-18
### ✨ Añadido
- **Guía: VS Code Vainilla** (`VSCode-Vanila.md`): página independiente y transversal con toda la configuración de VS Code para DOPO y MYSD — extensiones, tablas de configuración por curso y `settings.json` completo.

### 🔧 Modificado
- **Unidad 4 — VS Code** (`Unidad-Analisis-VSC.md`): eliminadas las secciones de MYSD (extensiones SQLTools, configuración SQL) y la repetición de la configuración Vainilla. Ahora delega a la Guía VS Code Vainilla y se enfoca exclusivamente en DOPO.
- **Home y README**: añadida la Guía VS Code Vainilla como entrada independiente en el índice.
- `nav_order` de Recursos actualizado a 8 y Changelog a 9 para dar lugar a la nueva página (7).

## [1.3.0] - 2026-06-18
### ✨ Añadido
- **Unidad 4: Análisis de Software** (página principal): teoría de los cuatro análisis (SonarLint, PMD, JaCoCo, PIT) con tabla de indicadores y práctica por ejemplo sobre `CuentaBancaria`.
- **Unidad 4 — Eclipse**: guía completa de instalación de Eclipse IDE, plugins EclEmma, Pitclipse, SonarLint y PMD, flujo de trabajo y ciclo de análisis S3/S4.
- **Unidad 4 — VS Code**: configuración "Vainilla" (programación consciente sin IA), extensiones para DOPO y MYSD, tabla de `settings.json` lista para copiar y ciclo de análisis S3/S4.
- **Recursos**: nueva sección de análisis de software con enlaces a SonarLint, PMD, JaCoCo, EclEmma, PIT, Pitclipse, Coverage Gutters, Eclipse y Extension Pack for Java.
- **Home y README**: actualizados con Unidad 4 en el índice de unidades y en el stack tecnológico.

### 🔧 Corregido
- Conflicto de `nav_order` entre `Recursos.md` (era 6) y `Unidad-Analisis.md` (6): Recursos movido a 7 y Changelog a 8.

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
