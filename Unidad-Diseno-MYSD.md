---
layout: default
title: "Diseño con Astah · MYSD"
parent: "Unidad 5: Diseño con Astah"
nav_order: 1
permalink: /Unidad-Diseno-MYSD/
---

# 🗄️ Diseño con Astah · MYSD
> **Línea de Fundamentos de Ingeniería de Software** | *IS-FUNDAMENTOS*
> Monitoría de **Modelos y Servicios de Datos (MYSD)** 🎓

{: .note }
> **Caso:** Empresa comercializadora. **Ciclo de vida:** iterativo + incremental, donde los **ciclos son áreas de negocio** y dentro de cada ciclo el desarrollo es **por grandes conceptos**.

> 🚀 **Diapositivas de la Unidad:** [Presentación Interactiva - Diseño con Astah MYSD](https://fis-eci.github.io/software-foundations-eci-slides/DisenoMYSD-presentation.html)

---

## 🏗️ Estructura de diseño

| Nivel | Artefactos |
| :--- | :--- |
| **Diseño conceptual · General** | Conceptos · Consultas gerenciales |
| **Diseño conceptual · Extendido** | Conceptos · Funciones · Consultas operativas |
| **Diseño lógico** | Modelo Mini |
| **Diseño físico** | Datos · Componentes · Actores |

### 📁 Esquema Astah (requisito de entrega)

```text
EmpresaComercializadora.asta
├── 01 Diseño conceptual
│   ├── General
│   │   ├── Conceptos              (diagrama de clases)
│   │   └── Consultas gerenciales  (historias de usuario)
│   └── Extendido · Ciclo 1 Ventas
│       ├── Conceptos              (diagrama de clases)
│       ├── Funciones              (casos de uso)
│       └── Consultas operativas   (historias de usuario)
├── 02 Diseño lógico
│   └── Modelo Mini                (diagrama de clases)
└── 03 Diseño físico
    ├── Datos                      (tablas y restricciones)
    ├── Componentes                (paquetes PC_)
    └── Actores                    (paquetes PA_ y roles)
```

---

## 1️⃣ Presentación del caso

Las empresas comercializadoras son organizaciones dedicadas a la **compra de productos a proveedores** para su posterior **venta a clientes finales**, actuando como intermediarias con el objetivo de satisfacer las necesidades del mercado; además, pueden complementar esta actividad mediante la **oferta de servicios asociados**.

## 2️⃣ Diseño general

### Conceptos

![Diseño conceptual general]({{ '/assets/diagramas/mysd-conceptos-general.svg' | relative_url }})

El diseño general solo identifica los **grandes conceptos (GC)** y sus relaciones; los atributos llegan en el diseño extendido.

### Consultas gerenciales

| Ciclo | Historia de usuario |
| :--- | :--- |
| Ventas | **COMO** Gerente de ventas **QUIERO** consultar el detalle de información de todos los bienes **PARA PODER** determinar incrementos de precio para el año entrante. *(Código, nombre, precio de venta, precio de compra y utilidad esperada, de mayor a menor utilidad.)* |
| Ventas *(propuesta)* | **COMO** Gerente general **QUIERO** conocer el total vendido por mes **PARA PODER** evaluar el desempeño comercial. |
| Compras *(propuesta)* | **COMO** Gerente de compras **QUIERO** consultar los proveedores con mayor valor comprado **PARA PODER** negociar mejores condiciones. |

## 3️⃣ División por ciclos

| Ciclo | Área de negocio | Grandes conceptos (en orden) | Funciones |
| :--- | :--- | :--- | :--- |
| **1** | Ventas | Clientes → Bienes → Facturas | Mantener Cliente, Mantener Bien, Registrar Factura |
| **2** | Compras | Proveedores → Compras (reutiliza Bienes) | Mantener Proveedor, Registrar Compra |

{: .highlight }
> Facturas se diseña al final del ciclo 1 porque depende de Clientes y de Bienes. Cada ciclo recorre de nuevo el diseño extendido, lógico y físico, solo para su área.

---

## 4️⃣ Diseño detallado · Ciclo 1 Ventas

### Diseño conceptual extendido · Conceptos

![Conceptos del ciclo Ventas]({{ '/assets/diagramas/mysd-conceptos-ventas.svg' | relative_url }})

* `«I»` identificador, `«U»` único, `/` atributo derivado, `[0..1]` opcional, `[1..*]` multivaluado.
* `Factura ◆— LineaFactura`: composición, una línea no existe sin su factura.
* Herencia **exclusiva y completa**: todo bien es producto o servicio, nunca ambos.
* `Utiliza` es una clase de asociación: cuántas `unidades` de un producto usa un servicio.

### Funciones

![Diagrama de funciones]({{ '/assets/diagramas/mysd-funciones.svg' | relative_url }})

### Consultas operativas

> **COMO** Vendedor **QUIERO** consultar la información completa de un servicio **PARA PODER** definir el monto de un descuento especial.
> Para el servicio definido (CSERVICIO): costo de mano de obra, costo de productos, costo total, precio de venta y utilidad esperada.

### Diseño lógico · Bosquejo

![Bosquejo del diseño lógico]({{ '/assets/diagramas/mysd-bosquejo-logico.svg' | relative_url }})

{: .important }
> **Se necesitan 9 tablas:** Clientes, Telefonos, Bienes, Productos, Servicios, Utilizaciones, Reemplazos, Facturas y LineasFactura. Las relaciones *Recomienda*, *EsDueño* y *EsDe* se guardan como claves foráneas; *Utiliza* y *PuedeReemplazar* (muchos a muchos) tienen tabla propia; la herencia usa tres tablas.

### Diseño lógico · Modelo Mini

![Modelo Mini]({{ '/assets/diagramas/mysd-modelo-mini.svg' | relative_url }})

Colores por gran concepto: 🔵 **Clientes** (Clientes, Telefonos) · 🟢 **Bienes** (Bienes, Productos, Servicios, Utilizaciones, Reemplazos) · 🟠 **Facturas** (Facturas, LineasFactura).

### Diseño físico · Datos

```sql
-- Tablas
CREATE TABLE Clientes(
  tid CHAR(2) NOT NULL, nid NUMBER(15) NOT NULL, nombre VARCHAR(20) NOT NULL,
  correo VARCHAR(10), tidRecomienda CHAR(2), nidRecomienda NUMBER(15));
CREATE TABLE Telefonos(
  tid CHAR(2) NOT NULL, nid NUMBER(15) NOT NULL, telefono VARCHAR(10) NOT NULL);
CREATE TABLE Bienes(
  codigo VARCHAR(5) NOT NULL, nombre VARCHAR(10) NOT NULL, precioVenta NUMBER(10,2) NOT NULL);
CREATE TABLE Productos(
  codigo VARCHAR(5) NOT NULL, existencias NUMBER(5) NOT NULL, precioCompra NUMBER(10,2) NOT NULL);
CREATE TABLE Servicios(
  codigo VARCHAR(5) NOT NULL, manoDeObra NUMBER(10,2) NOT NULL);
CREATE TABLE Utilizaciones(
  servicio VARCHAR(5) NOT NULL, producto VARCHAR(5) NOT NULL, unidades NUMBER(5) NOT NULL);
CREATE TABLE Reemplazos(
  producto VARCHAR(5) NOT NULL, reemplazo VARCHAR(5) NOT NULL);
CREATE TABLE Facturas(
  numero NUMBER(9) NOT NULL, fecha DATE NOT NULL, total NUMBER(10,2) NOT NULL,
  tidCliente CHAR(2) NOT NULL, nidCliente NUMBER(15) NOT NULL);
CREATE TABLE LineasFactura(
  factura NUMBER(9) NOT NULL, bien VARCHAR(5) NOT NULL,
  cantidad NUMBER(5) NOT NULL, precioVenta NUMBER(10,2) NOT NULL);

-- Claves primarias
ALTER TABLE Clientes      ADD CONSTRAINT PK_CLIENTES      PRIMARY KEY(tid, nid);
ALTER TABLE Telefonos     ADD CONSTRAINT PK_TELEFONOS     PRIMARY KEY(tid, nid, telefono);
ALTER TABLE Bienes        ADD CONSTRAINT PK_BIENES        PRIMARY KEY(codigo);
ALTER TABLE Productos     ADD CONSTRAINT PK_PRODUCTOS     PRIMARY KEY(codigo);
ALTER TABLE Servicios     ADD CONSTRAINT PK_SERVICIOS     PRIMARY KEY(codigo);
ALTER TABLE Utilizaciones ADD CONSTRAINT PK_UTILIZACIONES PRIMARY KEY(servicio, producto);
ALTER TABLE Reemplazos    ADD CONSTRAINT PK_REEMPLAZOS    PRIMARY KEY(producto, reemplazo);
ALTER TABLE Facturas      ADD CONSTRAINT PK_FACTURAS      PRIMARY KEY(numero);
ALTER TABLE LineasFactura ADD CONSTRAINT PK_LINEASFACTURA PRIMARY KEY(factura, bien);

-- Claves únicas
ALTER TABLE Clientes ADD CONSTRAINT UK_CLIENTES_CORREO UNIQUE(correo);

-- Claves foráneas
ALTER TABLE Clientes ADD CONSTRAINT FK_CLIENTES_RECOMIENDA
  FOREIGN KEY(tidRecomienda, nidRecomienda) REFERENCES Clientes(tid, nid);
ALTER TABLE Telefonos ADD CONSTRAINT FK_TELEFONOS_CLIENTES
  FOREIGN KEY(tid, nid) REFERENCES Clientes(tid, nid);
ALTER TABLE Productos ADD CONSTRAINT FK_PRODUCTOS_BIENES
  FOREIGN KEY(codigo) REFERENCES Bienes(codigo);
ALTER TABLE Servicios ADD CONSTRAINT FK_SERVICIOS_BIENES
  FOREIGN KEY(codigo) REFERENCES Bienes(codigo);
ALTER TABLE Utilizaciones ADD CONSTRAINT FK_UTILIZACIONES_SERVICIOS
  FOREIGN KEY(servicio) REFERENCES Servicios(codigo);
ALTER TABLE Utilizaciones ADD CONSTRAINT FK_UTILIZACIONES_PRODUCTOS
  FOREIGN KEY(producto) REFERENCES Productos(codigo);
ALTER TABLE Reemplazos ADD CONSTRAINT FK_REEMPLAZOS_PRODUCTO
  FOREIGN KEY(producto) REFERENCES Productos(codigo);
ALTER TABLE Reemplazos ADD CONSTRAINT FK_REEMPLAZOS_REEMPLAZO
  FOREIGN KEY(reemplazo) REFERENCES Productos(codigo);
ALTER TABLE Facturas ADD CONSTRAINT FK_FACTURAS_CLIENTES
  FOREIGN KEY(tidCliente, nidCliente) REFERENCES Clientes(tid, nid);
ALTER TABLE LineasFactura ADD CONSTRAINT FK_LINEASFACTURA_FACTURAS
  FOREIGN KEY(factura) REFERENCES Facturas(numero);
ALTER TABLE LineasFactura ADD CONSTRAINT FK_LINEASFACTURA_BIENES
  FOREIGN KEY(bien) REFERENCES Bienes(codigo);

-- Ejemplo de restricción declarativa: Moneda positiva con decimales 00, 25 o 50
ALTER TABLE Bienes ADD CONSTRAINT CK_BIENES_PRECIO
  CHECK (precioVenta > 0 AND MOD(precioVenta, 1) IN (0, 0.25, 0.5));
```

### Diseño físico · Componentes y actores

![Componentes y actores]({{ '/assets/diagramas/mysd-componentes-actores.svg' | relative_url }})

* **Componentes `PC_`:** un paquete PL/SQL por gran concepto con operaciones `ad_` (adicionar), `mo_` (modificar), `el_` (eliminar) y `co_` (consultar).
* **Actores `PA_`:** un paquete por actor que expone solo lo que ese usuario puede hacer; se otorga a su rol con `GRANT EXECUTE ON PA_GERENTE_VENTAS TO GERENTE_VENTAS;`.

### Consultas implementadas

```sql
-- Operativa · Vendedor: información completa de un servicio
SELECT s.codigo, b.nombre,
       s.manoDeObra AS costoManoDeObra,
       NVL(SUM(u.unidades * p.precioCompra), 0) AS costoProductos,
       s.manoDeObra + NVL(SUM(u.unidades * p.precioCompra), 0) AS costoTotal,
       b.precioVenta,
       b.precioVenta - s.manoDeObra - NVL(SUM(u.unidades * p.precioCompra), 0) AS utilidad
FROM Servicios s
  JOIN Bienes b ON b.codigo = s.codigo
  LEFT JOIN Utilizaciones u ON u.servicio = s.codigo
  LEFT JOIN Productos p ON p.codigo = u.producto
WHERE s.codigo = 'CSERVICIO'
GROUP BY s.codigo, b.nombre, s.manoDeObra, b.precioVenta;

-- Gerencial · Gerente de ventas: detalle de todos los bienes
SELECT b.codigo, b.nombre, b.precioVenta,
       NVL(p.precioCompra, sv.costo) AS precioCompra,
       b.precioVenta - NVL(p.precioCompra, sv.costo) AS utilidad
FROM Bienes b
  LEFT JOIN Productos p ON p.codigo = b.codigo
  LEFT JOIN (SELECT s.codigo,
                    s.manoDeObra + NVL(SUM(u.unidades * pr.precioCompra), 0) AS costo
             FROM Servicios s
               LEFT JOIN Utilizaciones u ON u.servicio = s.codigo
               LEFT JOIN Productos pr ON pr.codigo = u.producto
             GROUP BY s.codigo, s.manoDeObra) sv
    ON sv.codigo = b.codigo
ORDER BY utilidad DESC;
```

{: .note }
> Para los servicios, el "precio de compra" de la consulta gerencial es su **costo**: mano de obra más el costo de los productos que utiliza.

---

## ✅ Lista de entrega del ciclo

* [ ] Paquetes 01 conceptual (general y extendido), 02 lógico y 03 físico.
* [ ] Conceptos con tipos, estereotipos `«I»` `«U»`, derivados y multiplicidades.
* [ ] Funciones con todos los actores; consultas como historias de usuario.
* [ ] Modelo Mini con PK, UK y FK, coloreado por gran concepto.
* [ ] Datos, componentes `PC_` y actores `PA_` coherentes con las funciones.
* [ ] Todo nombrado igual en el diagrama, en el SQL y en la documentación.
