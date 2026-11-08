# Farmacia Salud Vida
### Documentación del submódulo de base de datos

---

## Tabla de contenido

1. [Descripción técnica de la base de datos](#1-descripción-técnica-de-la-base-de-datos)
2. [Diccionario de datos](#2-diccionario-de-datos)
3. [Relación e integración con los otros submódulos](#3-relación-e-integración-con-los-otros-submódulos)

---

## 1. Descripción técnica de la base de datos

La base de datos **FarmaciaSaludVida** fue desarrollada utilizando Microsoft SQL Server y el lenguaje Transact-SQL (T-SQL), con el propósito de almacenar y organizar la información relacionada con la administración de una farmacia.

Permite gestionar la información de categorías, proveedores, medicamentos, clientes y ventas, manteniendo una estructura organizada mediante relaciones entre tablas.

### 1.1. Características técnicas

| Característica | Descripción |
|---|---|
| Nombre de la base de datos | FarmaciaSaludVida |
| Motor de base de datos | Microsoft SQL Server |
| Lenguaje utilizado | Transact-SQL (T-SQL) |
| Modelo de base de datos | Relacional |
| Cantidad de tablas | 6 |
| Procedimientos almacenados | 2 |

### 1.2. Estructura de la base de datos

La base de datos está conformada por las siguientes tablas:

| N.º | Tabla | Descripción |
|---|---|---|
| 1 | Categorias | Almacena las categorías de los medicamentos. |
| 2 | Proveedores | Contiene la información de los proveedores. |
| 3 | Medicamentos | Registra los medicamentos, precios y existencias. |
| 4 | Clientes | Almacena la información de los clientes. |
| 5 | Ventas | Registra las ventas realizadas. |
| 6 | DetalleVentas | Contiene los medicamentos y cantidades de cada venta. |

### 1.3. Nomenclatura y restricciones utilizadas

En la construcción de la base de datos se utilizaron los siguientes elementos:

| Elemento | Función |
|---|---|
| PRIMARY KEY (PK) | Identifica de manera única cada registro de una tabla. |
| FOREIGN KEY (FK) | Establece relaciones entre diferentes tablas. |
| IDENTITY | Genera automáticamente valores consecutivos para los identificadores. |
| NOT NULL | Establece que un campo no puede quedar vacío. |
| UNIQUE | Evita valores duplicados en un campo. |
| DEFAULT | Asigna un valor predeterminado. |
| CHECK | Valida que los datos cumplan una condición establecida. |
| DECIMAL | Permite almacenar valores numéricos con decimales. |
| VARCHAR | Permite almacenar cadenas de texto. |
| DATE | Permite almacenar fechas. |
| INT | Permite almacenar números enteros. |

---

## 2. Diccionario de datos

El siguiente diccionario describe los campos principales de cada tabla, indicando sus tipos de datos y su función dentro de la base de datos.

### 2.1. Tabla: Categorias

**Descripción:** almacena las diferentes categorías utilizadas para clasificar los medicamentos.

| Campo | Tipo de dato | Descripción |
|---|---|---|
| CategoriaID (PK) | INT IDENTITY(1,1) | Identificador único de la categoría. |
| NombreCategoria | VARCHAR(50) | Nombre de la categoría. |
| Descripcion | VARCHAR(150) | Descripción de la categoría. |

### 2.2. Tabla: Proveedores

**Descripción:** almacena la información de las empresas encargadas de suministrar los medicamentos.

| Campo | Tipo de dato | Descripción |
|---|---|---|
| ProveedorID (PK) | INT IDENTITY(1,1) | Identificador único del proveedor. |
| NombreEmpresa | VARCHAR(100) | Nombre de la empresa proveedora. |
| Telefono | VARCHAR(20) | Teléfono de contacto. |
| Ciudad | VARCHAR(50) | Ciudad donde se encuentra el proveedor. |

### 2.3. Tabla: Medicamentos

**Descripción:** contiene la información de los medicamentos registrados en la farmacia.

| Campo | Tipo de dato | Descripción |
|---|---|---|
| MedicamentoID (PK) | INT IDENTITY(1,1) | Identificador único del medicamento. |
| NombreComercial | VARCHAR(100) | Nombre comercial del medicamento. |
| PrincipioActivo | VARCHAR(100) | Componente activo del medicamento. |
| CategoriaID (FK) | INT | Identificador de la categoría relacionada. |
| ProveedorID (FK) | INT | Identificador del proveedor relacionado. |
| PrecioUnitario | DECIMAL(10,2) | Precio unitario del medicamento. |
| Stock | INT | Cantidad disponible en inventario. |
| FechaExpiracion | DATE | Fecha de vencimiento del medicamento. |

### 2.4. Tabla: Clientes

**Descripción:** almacena los datos personales y de contacto de los clientes.

| Campo | Tipo de dato | Descripción |
|---|---|---|
| ClienteID (PK) | INT IDENTITY(1,1) | Identificador único del cliente. |
| Cedula | VARCHAR(20) | Número de identificación del cliente. |
| NombreCompleto | VARCHAR(100) | Nombre completo del cliente. |
| Telefono | VARCHAR(20) | Número telefónico. |
| CorreoElectronico | VARCHAR(100) | Correo electrónico del cliente. |
| FechaRegistro | DATE | Fecha en que se registra el cliente. |
| Direccion | VARCHAR(150) | Dirección del cliente. |

### 2.5. Tabla: Ventas

**Descripción:** registra las ventas realizadas a los clientes de la farmacia.

| Campo | Tipo de dato | Descripción |
|---|---|---|
| VentaID (PK) | INT IDENTITY(1,1) | Identificador único de la venta. |
| ClienteID (FK) | INT | Identificador del cliente relacionado. |
| FechaVenta | DATE | Fecha en que se realiza la venta. |
| TotalVenta | DECIMAL(10,2) | Valor total de la venta. |

### 2.6. Tabla: DetalleVentas

**Descripción:** almacena los medicamentos, las cantidades y los subtotales correspondientes a cada venta.

| Campo | Tipo de dato | Descripción |
|---|---|---|
| DetalleID (PK) | INT IDENTITY(1,1) | Identificador único del detalle. |
| VentaID (FK) | INT | Identificador de la venta relacionada. |
| MedicamentoID (FK) | INT | Identificador del medicamento relacionado. |
| Cantidad | INT | Cantidad de unidades vendidas. |
| Subtotal | DECIMAL(10,2) | Valor correspondiente al detalle de venta. |

## 2.7. Relaciones entre las tablas

La base de datos utiliza llaves primarias (PRIMARY KEY) y llaves foráneas (FOREIGN KEY) para relacionar las tablas y mantener la integridad de la información.

Las relaciones implementadas son las siguientes:

| Tabla principal | Tabla relacionada | Tipo de relación | Campo relacionado |
|---|---|---|---|
| Categorias | Medicamentos | Uno a muchos (1:N) | CategoriaID |
| Proveedores | Medicamentos | Uno a muchos (1:N) | ProveedorID |
| Clientes | Ventas | Uno a muchos (1:N) | ClienteID |
| Ventas | DetalleVentas | Uno a muchos (1:N) | VentaID |
| Medicamentos | DetalleVentas | Uno a muchos (1:N) | MedicamentoID |

### Descripción de las relaciones

**1. Categorias - Medicamentos (1:N)**

Una categoría puede tener varios medicamentos registrados, pero cada medicamento pertenece a una sola categoría.

**2. Proveedores - Medicamentos (1:N)**

Un proveedor puede suministrar varios medicamentos, mientras que cada medicamento está asociado a un proveedor.

**3. Clientes - Ventas (1:N)**

Un cliente puede realizar varias compras, pero cada venta está asociada a un solo cliente.

**4. Ventas - DetalleVentas (1:N)**

Una venta puede contener varios detalles de productos, mientras que cada detalle pertenece a una sola venta.

**5. Medicamentos - DetalleVentas (1:N)**

Un medicamento puede aparecer en diferentes detalles de venta, mientras que cada detalle corresponde a un solo medicamento.




**Nota:** Las tablas Ventas y Medicamentos se relacionan indirectamente mediante DetalleVentas, permitiendo que una venta incluya diferentes medicamentos y que un medicamento pueda aparecer en diferentes ventas.

---

## 3. Relación e integración con los otros submódulos

El proyecto integrador está conformado por tres submódulos: **base de datos, backend y frontend**. Cada uno cumple una función específica y se complementan para representar el funcionamiento general del sistema Farmacia Salud Vida.

De acuerdo con el alcance establecido para el **Nivel 1**, los submódulos están relacionados conceptualmente, pero todavía no cuentan con una conexión técnica entre ellos.

### 3.1. Relación entre el backend y la base de datos

El backend contiene las clases y la lógica del sistema, mientras que la base de datos se encarga de almacenar la información.

Las clases del backend se relacionan conceptualmente con las tablas de la base de datos, ya que representan elementos similares del sistema, como medicamentos, clientes, proveedores y ventas.

Por ejemplo, la información de un medicamento representada en el backend corresponde a los campos almacenados en la tabla `Medicamentos`.

Esta relación permite identificar cómo se organizaría la información en una futura integración entre ambos componentes.

### 3.2. Relación entre el frontend y la base de datos

El frontend corresponde a la parte visual del sistema, mediante la cual los usuarios pueden interactuar con las diferentes funcionalidades.

Las vistas y formularios del frontend representan operaciones relacionadas con la información almacenada en la base de datos, como:

- Consulta de medicamentos.
- Registro de clientes.
- Visualización de proveedores.
- Consulta de ventas.

Estas funcionalidades tienen correspondencia con las tablas diseñadas en la base de datos.

Sin embargo, en esta etapa las vistas no realizan consultas directas a SQL Server.

### 3.3. Relación general de los tres submódulos

La relación conceptual entre los componentes se puede resumir de la siguiente manera:

| Submódulo | Función dentro del proyecto |
|---|---|
| Frontend | Presenta la interfaz y permite la interacción del usuario. |
| Backend | Contiene las clases y la lógica del funcionamiento del sistema. |
| Base de datos | Almacena y organiza la información del sistema. |

### 3.4. Alcance de la integración en el Nivel 1

En esta primera etapa, los submódulos se desarrollan de manera independiente, pero comparten el mismo contexto funcional.

Por lo tanto:

- Las clases del backend tienen una relación conceptual con las tablas de la base de datos.
- Las vistas del frontend representan funcionalidades relacionadas con la información almacenada.
- No existe una conexión técnica entre el frontend, el backend y SQL Server.
- La integración técnica se podrá desarrollar en etapas posteriores del proyecto.

De esta manera, cada submódulo aporta una parte del desarrollo general de Farmacia Salud Vida, manteniendo una estructura organizada y coherente con los objetivos del proyecto integrador.
