# 🎬 Guiones de Producción — Videos Pendientes IS-FUNDAMENTOS

Documento interno de producción. No forma parte de la wiki pública.

---

## 📋 Resumen de Videos Pendientes

| # | Video | Unidad | Tiempo estimado |
|---|---|---|---|
| 1 | Instalación Eclipse + 4 plugins | Unidad 4 — Eclipse | 8–10 min |
| 2 | Los cuatro análisis en Eclipse (`CuentaBancaria`) | Unidad 4 — Eclipse | 15–18 min |
| 3 | Los cuatro análisis en VS Code (`CuentaBancaria`) | Unidad 4 — VS Code | 15–18 min |
| 4 | VS Code + SQLTools setup PostgreSQL | Unidad 3 — PostgreSQL | 8–10 min |
| 5 | Flujo SQL consciente con Git | Unidad 3 — PostgreSQL | 10–12 min |

---

## 🎬 VIDEO 1 — Instalación y Configuración de Eclipse para DOPO

**Unidad:** Unidad 4 → Eclipse | **Duración estimada:** 8–10 min

### Antes de grabar

- Desinstala Eclipse si lo tienes (para mostrar el proceso desde cero limpio).
- Ten el JDK 11 o 17 instalado y verifica con `java -version` en terminal.
- Abre el navegador en `eclipse.org/downloads`.
- Cierra todo lo que no uses para tener pantalla limpia.

### Pasos en cámara

**Bloque 1 — Instalación de Eclipse (2 min)**
1. Ir a `eclipse.org/downloads` → clic en **Download**.
2. Ejecutar el instalador descargado.
3. Seleccionar **"Eclipse IDE for Java Developers"** — mencionar que no es la versión Enterprise ni la de C++.
4. Aceptar la ruta por defecto → **Install** → **Launch**.
5. En el diálogo de Workspace, explicar qué es (carpeta donde viven los proyectos) → aceptar la ruta por defecto o crear una en `Documentos/DOPO`.

**Bloque 2 — Instalación de SonarLint (2 min)**
1. Menú **Help → Eclipse Marketplace**.
2. Buscar `SonarLint` → clic en **Install**.
3. Aceptar licencia → **Finish** → dejar que instale.
4. Cuando pida reiniciar: **Restart Now**.
5. Tras reiniciar: **Window → Show View → Other → SonarLint → On-The-Fly Issues** — verificar que aparece la vista.

**Bloque 3 — Instalación de PMD (1.5 min)**
1. **Help → Eclipse Marketplace** → buscar `PMD Eclipse Plugin`.
2. Instalar → aceptar → **Restart Now**.
3. Verificar: clic derecho sobre cualquier proyecto en Package Explorer → debe aparecer la opción **PMD**.

**Bloque 4 — Instalación de EclEmma (1.5 min)**
1. **Help → Eclipse Marketplace** → buscar `EclEmma`.
2. Instalar → **Restart Now**.
3. Verificar: **Window → Show View → Other → Java → Coverage** — debe aparecer la vista de cobertura.

**Bloque 5 — Instalación de Pitclipse (1.5 min)**
1. **Help → Eclipse Marketplace** → buscar `Pitclipse`.
2. Instalar → **Restart Now**.
3. Verificar: clic derecho sobre un proyecto → debe aparecer **PIT → PIT Mutation Test**.

**Cierre (30 seg)**
- Mostrar la pantalla de Eclipse con las cuatro vistas activas.
- Decir: *"Con esto el entorno está listo para ejecutar los cuatro análisis del curso."*

---

## 🎬 VIDEO 2 — Los Cuatro Análisis en Acción en Eclipse

**Unidad:** Unidad 4 → Eclipse | **Duración estimada:** 15–18 min

### Antes de grabar

Crea el proyecto `CuentaBancaria` en BlueJ con estos dos archivos exactamente así (con los defectos intencionales):

```java
// CuentaBancaria.java
public class CuentaBancaria {
    private double saldo;
    private String tipo = "ahorros";

    public void consignar(double monto) {
        if (monto > 0) {
            saldo = saldo + monto;
        }
    }

    public void retirar(double monto) {
        if (monto > 0 & monto <= saldo) {  // defecto intencional: & en vez de &&
            saldo = saldo - monto;
        }
    }

    public double getSaldo() { return saldo; }
    public String getTipo() { return tipo; }

    private void metodoInterno() {          // defecto intencional: método muerto
        System.out.println("debug");
    }
}
```

```java
// CuentaBancariaTest.java (pruebas iniciales incompletas a propósito)
import static org.junit.Assert.*;
import org.junit.Test;

public class CuentaBancariaTest {

    @Test
    public void shouldAumentarSaldoWhenConsignarMontoValido() {
        CuentaBancaria cuenta = new CuentaBancaria();
        cuenta.consignar(100.0);
        assertEquals(100.0, cuenta.getSaldo(), 0.01);
    }

    @Test
    public void shouldRetirarWhenMontoValidoYSaldoSuficiente() {
        CuentaBancaria cuenta = new CuentaBancaria();
        cuenta.consignar(100.0);
        cuenta.retirar(50.0);
        assertEquals(50.0, cuenta.getSaldo(), 0.01);
    }
}
```

### Pasos en cámara

**Bloque 0 — Importar proyecto (1.5 min)**
1. **File → Import → General → Existing Projects into Workspace → Next**.
2. Seleccionar la carpeta raíz del proyecto BlueJ → **Finish**.
3. Verificar que no hay errores rojos en la vista **Problems**.
4. Mostrar el código de `CuentaBancaria.java` y explicar brevemente los dos defectos que vamos a encontrar con las herramientas.

**Bloque 1 — SonarLint (3 min)**
1. Abrir `CuentaBancaria.java` — SonarLint ya subraya el `&` en `retirar`.
2. Abrir **Window → Show View → Other → SonarLint → On-The-Fly Issues**.
3. Hacer clic sobre el incidente para ir a la línea.
4. Leer en voz alta la descripción de la regla violada.
5. ⏸️ **ACTIVIDAD:** *"Pausa el video ahora — antes de ver la corrección, escribe en papel cómo lo arreglarías."*
6. Corregir: cambiar `&` por `&&`.
7. Guardar → mostrar que el incidente desaparece de la vista SonarLint.

**Bloque 2 — PMD (3 min)**
1. Clic derecho sobre el proyecto → **PMD → Check Code**.
2. Abrir vista **PMD Violations** — mostrar la lista ordenada por prioridad.
3. Señalar el incidente de `metodoInterno()` (método privado no referenciado).
4. Explicar: *"Código muerto — viola el principio YAGNI."*
5. ⏸️ **ACTIVIDAD:** *"Pausa — ¿por qué crees que este incidente merece ser resuelto?"*
6. Eliminar `metodoInterno()` del código.
7. Volver a ejecutar **PMD → Check Code** — mostrar que el incidente desapareció.

**Bloque 3 — JaCoCo / EclEmma (4 min)**
1. Clic derecho sobre `CuentaBancariaTest` → **Coverage As → JUnit Test**.
2. Mostrar el código coloreado: verde, rojo, amarillo.
3. Señalar la línea amarilla en el `if` de `retirar` — rama del `else` implícito sin cubrir.
4. Abrir vista **Coverage** → mostrar el % de Branch Coverage.
5. ⏸️ **ACTIVIDAD:** *"Pausa — identifica la rama roja o amarilla y escribe el caso de prueba que la cubriría."*
6. Agregar en `CuentaBancariaTest.java`:

```java
@Test
public void shouldNotRetirarWhenMontoNegativo() {
    // Given
    CuentaBancaria cuenta = new CuentaBancaria();
    cuenta.consignar(100.0);
    // When
    cuenta.retirar(-50.0);
    // Then
    assertEquals(100.0, cuenta.getSaldo(), 0.01);
}
```

7. Re-ejecutar **Coverage As → JUnit Test** — mostrar que la rama se cubre (verde).

**Bloque 4 — PIT / Pitclipse (4 min)**
1. Clic derecho sobre el proyecto → **PIT → PIT Mutation Test**.
2. Esperar (puede tardar 1–2 min) — mientras tanto explicar brevemente qué hace PIT.
3. Abrir el reporte HTML cuando termine — navegar a `CuentaBancaria`.
4. Señalar un mutante **Survived** en rojo, por ejemplo `monto > 0` → `monto >= 0`.
5. Explicar: *"PIT cambió el `>` por `>=` y ninguna prueba detectó el error — significa que nunca probamos monto igual a cero."*
6. ⏸️ **ACTIVIDAD:** *"Pausa — escribe la prueba que mataría exactamente este mutante."*
7. Agregar:

```java
@Test
public void shouldNotConsignarWhenMontoCero() {
    // Given
    CuentaBancaria cuenta = new CuentaBancaria();
    // When
    cuenta.consignar(0.0);
    // Then
    assertEquals(0.0, cuenta.getSaldo(), 0.01);
}
```

8. Re-ejecutar PIT — mostrar que el Mutation Score subió.

**Cierre (30 seg)**
- Mostrar tabla mental: análisis inicial vs. análisis final para los cuatro análisis.

---

## 🎬 VIDEO 3 — Los Cuatro Análisis en Acción en VS Code

**Unidad:** Unidad 4 → VS Code | **Duración estimada:** 15–18 min

### Antes de grabar

- VS Code con configuración Vainilla aplicada.
- Extensiones instaladas: Extension Pack for Java, SonarLint, PMD, Java Test Runner, Coverage Gutters.
- El mismo proyecto `CuentaBancaria` con los mismos defectos del Video 2, pero como proyecto Maven con este `pom.xml`:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.escuela</groupId>
  <artifactId>cuenta-bancaria</artifactId>
  <version>1.0</version>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
  <build>
    <plugins>
      <plugin>
        <groupId>org.pitest</groupId>
        <artifactId>pitest-maven</artifactId>
        <version>1.15.0</version>
        <configuration>
          <targetClasses><param>com.escuela.*</param></targetClasses>
          <targetTests><param>com.escuela.*Test</param></targetTests>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### Pasos en cámara

**Bloque 0 — Abrir proyecto (1 min)**
1. **File → Open Folder** → seleccionar carpeta del proyecto.
2. VS Code detecta el proyecto Java automáticamente.
3. Verificar vista **Problems** sin errores (`Ctrl+Shift+M`).

**Bloque 1 — SonarLint (3 min)**
1. Abrir `CuentaBancaria.java` — mostrar el subrayado del `&`.
2. Abrir **Problems** (`Ctrl+Shift+M`) — señalar el incidente SonarLint.
3. Hacer clic para ir a la línea — leer la descripción.
4. ⏸️ **ACTIVIDAD:** *"Pausa el video — antes de ver la corrección, escribe cómo lo arreglarías."*
5. Corregir `&` → `&&` y guardar — incidente desaparece.

**Bloque 2 — PMD (2.5 min)**
1. `Ctrl+Shift+P` → escribir `PMD: Run` → Enter.
2. Mostrar resultado en **Problems**.
3. Señalar `metodoInterno()`.
4. ⏸️ **ACTIVIDAD:** *"Pausa — ¿por qué es relevante este incidente?"*
5. Eliminar método → re-ejecutar `PMD: Run` → incidente desapareció.

**Bloque 3 — JaCoCo + Coverage Gutters (4 min)**
1. Abrir panel de Testing (ícono 🧪 en barra lateral) → **Run All Tests**.
2. `Ctrl+Shift+P` → `Coverage Gutters: Display Coverage`.
3. Mostrar líneas rojas en `retirar`.
4. ⏸️ **ACTIVIDAD:** *"Pausa — identifica las líneas rojas y escribe el caso de prueba que las cubriría."*
5. Agregar `shouldNotRetirarWhenMontoNegativo()` (mismo código que Video 2).
6. Re-ejecutar pruebas → `Coverage Gutters: Display Coverage` → líneas en verde.

**Bloque 4 — PIT con Maven (5 min)**
1. Abrir terminal integrada (`Ctrl+\``).
2. Ejecutar: `mvn pitest:mutationCoverage` — mientras corre, explicar qué hace PIT.
3. Abrir `target/pit-reports/index.html` en el navegador.
4. Navegar a `CuentaBancaria` — señalar mutante **Survived**.
5. ⏸️ **ACTIVIDAD:** *"Pausa — escribe la prueba que mataría exactamente este mutante."*
6. Agregar `shouldNotConsignarWhenMontoCero()` (mismo código que Video 2).
7. Re-ejecutar `mvn pitest:mutationCoverage` — mostrar score mejorado.

---

## 🎬 VIDEO 4 — Configuración de VS Code con SQLTools para PostgreSQL

**Unidad:** Unidad 3 → PostgreSQL en VS Code | **Duración estimada:** 8–10 min

### Antes de grabar

- VS Code con configuración Vainilla aplicada (tenerla lista, no instalarla en cámara).
- Credenciales del servidor PostgreSQL del curso disponibles.
- Opcionalmente: PostgreSQL local instalado como respaldo.

### Pasos en cámara

**Bloque 0 — Contexto (1 min)**
1. Mostrar brevemente la Guía VS Code Vainilla en el wiki.
2. Confirmar que la configuración Vainilla general ya está aplicada (`settings.json`).
3. Mencionar que este video agrega específicamente la configuración para MYSD.

**Bloque 1 — Instalar extensiones (2 min)**
1. `Ctrl+Shift+X` → buscar `SQLTools` (de Matheus Teixeira) → **Install**.
2. Buscar `SQLTools PostgreSQL` → instalar el driver oficial → **Reload**.
3. Mostrar que aparece el ícono de SQLTools en la barra lateral.

**Bloque 2 — Configuración Vainilla MYSD (2 min)**
1. `Ctrl+Shift+P` → `Open User Settings (JSON)`.
2. Mostrar que ya están las claves generales Vainilla.
3. Explicar las tres reglas MYSD: no autocompletado SQL, no asistentes visuales, ejecución manual.

**Bloque 3 — Crear la conexión (3 min)**
1. Clic en el ícono de SQLTools en la barra lateral.
2. **Add New Connection** → seleccionar **PostgreSQL**.
3. Completar el formulario campo por campo:
   - **Connection Name:** `Escuela-Postgre`
   - **Server/Host:** [dirección del servidor]
   - **Port:** `5432`
   - **Database:** [base de datos asignada]
   - **Username:** [usuario asignado]
   - **Password:** [contraseña]
4. Clic en **Test Connection** — mostrar `Connected successfully`.
5. **Save Connection**.

**Bloque 4 — Explorar el esquema (1.5 min)**
1. Expandir la conexión en el panel lateral.
2. Mostrar tablas y esquemas disponibles.
3. Cerrar la conexión al final: clic derecho → **Disconnect** — mencionar que esto es parte del protocolo de trabajo responsable.

---

## 🎬 VIDEO 5 — Flujo de Trabajo SQL en VS Code: Consultas Conscientes

**Unidad:** Unidad 3 → PostgreSQL en VS Code | **Duración estimada:** 10–12 min

### Antes de grabar

- VS Code con SQLTools conectado (estado final del Video 4).
- Carpeta de proyecto abierta con estructura `scripts/`.
- Terminal Git disponible.

### Pasos en cámara

**Bloque 0 — Estructura del proyecto (1 min)**
1. Mostrar la carpeta del proyecto en VS Code:

```
mi-proyecto/
├── src/          ← código Java
├── scripts/      ← scripts SQL (crear esta carpeta en cámara)
└── .gitignore
```

2. Crear la carpeta `scripts/` desde el explorador de VS Code.

**Bloque 1 — DDL: Crear tablas manualmente (3 min)**
1. Crear `scripts/esquema.sql`.
2. Escribir manualmente (sin autocompletado) el DDL:

```sql
CREATE TABLE cliente (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(200) UNIQUE
);

CREATE TABLE cuenta (
    id SERIAL PRIMARY KEY,
    saldo NUMERIC(12,2) DEFAULT 0,
    tipo VARCHAR(20),
    cliente_id INTEGER REFERENCES cliente(id)
);
```

3. Seleccionar todo el texto → `Ctrl+Shift+E` para ejecutar.
4. Mostrar en el panel de resultados que las tablas se crearon.
5. Expandir la conexión en SQLTools — mostrar que las tablas aparecen en el esquema.

**Bloque 2 — DML: Insertar y consultar (3 min)**
1. Crear `scripts/datos.sql`.
2. Escribir manualmente:

```sql
INSERT INTO cliente (nombre, email)
VALUES ('Juan Pérez', 'juan@escuela.edu.co');

INSERT INTO cliente (nombre, email)
VALUES ('María García', 'maria@escuela.edu.co');

INSERT INTO cuenta (saldo, tipo, cliente_id)
VALUES (500000, 'ahorros', 1);

SELECT c.nombre, cu.saldo, cu.tipo
FROM cliente c
JOIN cuenta cu ON cu.cliente_id = c.id;
```

3. Seleccionar solo el `SELECT` → `Ctrl+Shift+E` — mostrar los resultados.
4. Mencionar: *"Nunca ejecutes todo el archivo sin revisar línea a línea."*

**Bloque 3 — Versionado de scripts con Git (2.5 min)**
1. Abrir terminal integrada (`Ctrl+\``).
2. `git status` — mostrar que `scripts/` aparece como untracked.
3. `git add scripts/esquema.sql` → commit:

```
git commit -m "feat: add cliente and cuenta tables schema"
```

4. `git add scripts/datos.sql` → commit:

```
git commit -m "feat: add sample data for cliente and cuenta"
```

5. Mostrar `git log --oneline` — dos commits atómicos y descriptivos.

**Bloque 4 — Limpieza responsable (1 min)**
1. Ejecutar manualmente en SQLTools:

```sql
TRUNCATE TABLE cuenta;
TRUNCATE TABLE cliente CASCADE;
```

2. Verificar en el esquema que las tablas están vacías.
3. Desconectar: clic derecho sobre la conexión → **Disconnect**.
4. Cierre: *"Scripts versionados, servidor limpio — así se trabaja en recursos compartidos."*
