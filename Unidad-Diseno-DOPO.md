---
layout: default
title: "Diseño con Astah · DOPO"
parent: "Unidad 5: Diseño con Astah"
nav_order: 2
permalink: /Unidad-Diseno-DOPO/
---

# ☕ Diseño con Astah · DOPO
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **DOPO (Desarrollo Orientado por Objetos)** 🎓

{: .note }
> **Caso:** Batalla N (batalla naval). **Ciclo de vida:** iterativo + incremental, donde los **ciclos son versiones del sistema** y dentro de cada ciclo el desarrollo es **por comportamiento**: método → diagrama de clases → diagrama de secuencia → código.

> 🚀 **Diapositivas de la Unidad:** [Presentación Interactiva - Diseño con Astah DOPO](https://fis-eci.github.io/software-foundations-eci-slides/DisenoDOPO-presentation.html)

---

## 🏗️ Estructura de diseño

| Artefacto | Propósito |
| :--- | :--- |
| **Package Diagram** | Capas del sistema: `presentation` depende de `domain`, nunca al revés. |
| **Presentation · Class Diagram** | La interfaz gráfica y a quién del dominio le pide los datos. |
| **Domain · Class Diagram** | La estructura: clases, atributos, operaciones y asociaciones. |
| **Domain · Sequence Diagram** | El comportamiento de cada método nuevo. |

### 📁 Esquema Astah (requisito de entrega)

```text
BatallaN.asta
├── Package Diagram              (presentation → domain)
├── presentation
│   └── Class Diagram            (BatallaNavalGUI)
└── domain
    ├── Class Diagram            (una vista por versión)
    └── Sequence Diagrams
        ├── Flota.numeroMaquinas
        ├── Flota.suficientesMarinos
        ├── Flota.alias
        ├── Flota.disponibilidadEnPortaaviones
        ├── Flota.muevase
        ├── Flota.seranDestruidas
        ├── Flota.esBuenAtaque
        ├── Flota.enAire
        └── Flota.problemaEnAire
```

---

## 1️⃣ Presentación del caso

En el juego batalla naval una serie de **flotas** compiten entre sí para tomar el control del **tablero**. Estas flotas se componen de **barcos, portaaviones, aviones y marinos**. De la totalidad de los marinos disponibles en la flota, sólo los que están en turno están asignados a una de estas máquinas. Cada máquina tiene una **ubicación** determinada por su longitud y latitud. En una ubicación pueden estar muchas naves. *(Todos los contenedores son `ArrayList`.)*

## 2️⃣ Diseño general

### Package Diagram y presentación

![Diagrama de paquetes]({{ '/assets/diagramas/dopo-paquetes.svg' | relative_url }})

![Diagrama de clases de presentación]({{ '/assets/diagramas/dopo-presentacion.svg' | relative_url }})

### Dominio · versión inicial

![Diagrama de clases inicial]({{ '/assets/diagramas/dopo-dominio-v1.svg' | relative_url }})

* Una flecha indica **navegabilidad**: la clase de origen conoce a la de destino.
* El rol (`aviones`, `ubicacion`, …) es el nombre del atributo privado en la clase de origen; `*` se implementa con `ArrayList`.
* `piloto 1` y `copiloto 0..1` son dos asociaciones distintas entre `Avion` y `Marino`.
* `Tablero — Flota` es una asociación en ambos sentidos.

## 3️⃣ División por ciclos

| Ciclo | Versión | Comportamiento |
| :--- | :--- | :--- |
| **1** | Estructura | Mapa de memoria, atributos diseñados y nuevos atributos |
| **2** | Gestión de la flota | `numeroMaquinas` (\*), `suficientesMarinos` (\*), `alias` (\*\*), `disponibilidadEnPortaaviones` (\*\*), `muevase` (\*\*) |
| **3** | Ataque en agua | `seranDestruidas` (1\*\*), `esBuenAtaque` (1\*\*\*) |
| **4** | Espacio aéreo | `enAire` (2\*\*), `problemaEnAire` (2\*\*\*) |

{: .highlight }
> Los métodos de un mismo grupo (1 y 2) se resuelven en orden: `esBuenAtaque` reutiliza `seranDestruidas` y `problemaEnAire` reutiliza `enAire`.

---

## 4️⃣ Diseño detallado

### Ciclo 1 · Mapa de memoria

> LA GRAN FLOTA BLANCA tiene un portaaviones (número 100) que lleva dos aviones en misión de ataque (placas HR100 y JB100), piloteados por Henry Reuterdahl y John Charles Roach. Este portaaviones, cuyo capitán es el almirante Sperry, está al 50% de su capacidad. LA GRAN ARMADA DE CASTILLA tiene un barco (número 900) y un avión (placa PEACE). Pedrarias Dávila y Fernando Villamil son marinos de esta flota; Pedrarias está asignado al barco 900 y Fernando está sin asignación.

![Mapa de memoria]({{ '/assets/diagramas/dopo-memoria.svg' | relative_url }})

{: .warning }
> **Observa el avión PEACE:** el diagrama exige `piloto 1`, pero nadie lo pilotea, así que el objeto queda con `piloto = null` y **viola la multiplicidad**. Al diseñar, esa inconsistencia debe resolverse en el modelo (por ejemplo, `piloto 0..1` mientras el avión está en tierra) o en los datos.

### Ciclo 1 · Nuevos atributos

* Un **código** para identificar las flotas: no se puede modificar y todos lo pueden consultar.
* Los **tripulantes mínimos** y los **puntajes** de portaaviones, barco y avión: los puntajes cambian durante el juego, los tripulantes no.
* El **tablero es cuadrado**: longitudes y latitudes en el rango [-100, 100].

![Diagrama de clases versión 1]({{ '/assets/diagramas/dopo-dominio-v2.svg' | relative_url }})

```java
// Flota
private final String codigo;          // se asigna en el constructor
public String getCodigo() { return codigo; }

// Tablero
public static final int MINIMO = -100;
public static final int MAXIMO = 100;

// PortaAviones (Barco: TRIPULANTES = 4, Avion: TRIPULANTES = 2)
public static final int TRIPULANTES = 5;
private static int puntaje;
public static int getPuntaje() { return puntaje; }
public static void setPuntaje(int puntaje) { PortaAviones.puntaje = puntaje; }
```

### Ciclo 2 · Gestión de la flota

![Diagrama de clases versión 2]({{ '/assets/diagramas/dopo-dominio-v3.svg' | relative_url }})

| Método | Diagrama de secuencia |
| :--- | :--- |
| `numeroMaquinas()` | ![numeroMaquinas]({{ '/assets/diagramas/seq-numeroMaquinas.svg' | relative_url }}) |
| `suficientesMarinos()` | ![suficientesMarinos]({{ '/assets/diagramas/seq-suficientesMarinos.svg' | relative_url }}) |
| `alias()` | ![alias]({{ '/assets/diagramas/seq-alias.svg' | relative_url }}) |
| `disponibilidadEnPortaaviones()` | ![disponibilidad]({{ '/assets/diagramas/seq-disponibilidad.svg' | relative_url }}) |
| `muevase(dLon, dLat)` | ![muevase]({{ '/assets/diagramas/seq-muevase.svg' | relative_url }}) |

```java
// Flota
public int numeroMaquinas() {
    return aviones.size() + portaAviones.size() + barcos.size();
}

public boolean suficientesMarinos() {
    int requeridos = portaAviones.size() * PortaAviones.TRIPULANTES
                   + barcos.size() * Barco.TRIPULANTES
                   + aviones.size() * Avion.TRIPULANTES;
    return marinos.size() >= requeridos;
}

public int alias() {
    return tablero.flotasLlamadas(nombre) - 1;   // sin contarse a sí misma
}

public int disponibilidadEnPortaaviones() {
    int total = 0;
    for (PortaAviones p : portaAviones) total += p.disponibilidad();
    return total;
}

public void muevase(int dLon, int dLat) {
    for (Barco b : barcos) b.muevase(dLon, dLat);
}

// Tablero
public int flotasLlamadas(String nombre) {
    int n = 0;
    for (Flota otra : flotas) {
        if (otra.getNombre().equals(nombre)) n++;
    }
    return n;
}

// PortaAviones
public int disponibilidad() { return capacidad - aviones.size(); }

// Barco
public void muevase(int dLon, int dLat) { ubicacion.muevase(dLon, dLat); }

// Posicion
public void muevase(int dLon, int dLat) {
    int lon = longitud + dLon, lat = latitud + dLat;
    if (lon >= Tablero.MINIMO && lon <= Tablero.MAXIMO
            && lat >= Tablero.MINIMO && lat <= Tablero.MAXIMO) {
        longitud = lon;
        latitud = lat;
    }
}
```

{: .note }
> **Decisión de diseño en `muevase`:** cada barco se mueve si su destino queda dentro del tablero. Si "si es posible" se interpretara como "todos o ninguno", primero habría que verificar todos los destinos y solo después mover.

### Ciclos 3 y 4 · Ataque en agua y espacio aéreo

![Diagrama de clases final]({{ '/assets/diagramas/dopo-dominio-v4.svg' | relative_url }})

| Método | Diagrama de secuencia |
| :--- | :--- |
| `seranDestruidas(lon, lat)` | ![seranDestruidas]({{ '/assets/diagramas/seq-seranDestruidas.svg' | relative_url }}) |
| `esta(lon, lat)` (apoyo) | ![esta]({{ '/assets/diagramas/seq-esta.svg' | relative_url }}) |
| `esBuenAtaque(lon, lat)` | ![esBuenAtaque]({{ '/assets/diagramas/seq-esBuenAtaque.svg' | relative_url }}) |
| `enAire()` | ![enAire]({{ '/assets/diagramas/seq-enAire.svg' | relative_url }}) |
| `problemaEnAire()` | ![problemaEnAire]({{ '/assets/diagramas/seq-problemaEnAire.svg' | relative_url }}) |

```java
// Flota
public ArrayList<Object> seranDestruidas(int lon, int lat) {
    ArrayList<Object> destruidas = new ArrayList<>();
    for (PortaAviones p : portaAviones) if (p.esta(lon, lat)) destruidas.add(p);
    for (Barco b : barcos) if (b.esta(lon, lat)) destruidas.add(b);
    for (Avion a : aviones) if (!a.isEnAire() && a.esta(lon, lat)) destruidas.add(a);
    return destruidas;
}

public boolean esBuenAtaque(int lon, int lat) {
    if (!seranDestruidas(lon, lat).isEmpty()) return false;   // sin bajas propias
    int afectadas = 0;
    for (Flota enemiga : tablero.enemigas(this)) {
        afectadas += enemiga.seranDestruidas(lon, lat).size();
    }
    return afectadas > 0;                                       // destruye enemigos
}

public ArrayList<String> enAire() {
    ArrayList<String> placas = new ArrayList<>();
    for (Flota enemiga : tablero.enemigas(this)) placas.addAll(enemiga.placasEnAire());
    return placas;
}

public ArrayList<String> placasEnAire() {
    ArrayList<String> placas = new ArrayList<>();
    for (Avion a : aviones) if (a.isEnAire()) placas.add(a.getPlaca());
    return placas;
}

public boolean problemaEnAire() {
    ArrayList<String> enemigos = enAire();
    for (String placa : placasEnAire()) {
        if (enemigos.contains(placa)) return true;
    }
    return false;
}

// Tablero
public ArrayList<Flota> enemigas(Flota flota) {
    ArrayList<Flota> enemigas = new ArrayList<>();
    for (Flota f : flotas) if (f != flota) enemigas.add(f);
    return enemigas;
}

// PortaAviones, Barco y Avion
public boolean esta(int lon, int lat) {
    return ubicacion != null && ubicacion.esta(lon, lat);
}

// Posicion
public boolean esta(int lon, int lat) {
    return longitud == lon && latitud == lat;
}
```

{: .highlight }
> **¿Siguiente versión?** Las tres máquinas repiten `ubicacion` y `esta`. El proyecto `battleShip` propone una superclase `Machine` con la ubicación común: un buen ejercicio es rediseñar los diagramas con herencia.

---

## ✅ Lista de entrega por versión

* [ ] Package Diagram con `presentation` → `domain`.
* [ ] Class Diagram de presentación y de dominio actualizados a la versión.
* [ ] Un Sequence Diagram por método nuevo, nombrado `Clase.metodo`.
* [ ] Cada mensaje de una secuencia existe como operación en el diagrama de clases.
* [ ] Código Java idéntico al diseño: mismos nombres, tipos y visibilidades.
* [ ] Mapa de memoria (diagrama de objetos) del ciclo 1.
