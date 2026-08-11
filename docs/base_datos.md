# Diseño de Base de Datos - SmartERP

## 1. Introducción

La base de datos de SmartERP utilizará MySQL como sistema gestor de base de datos relacional.

El diseño seguirá un modelo relacional y buscará mantener la integridad de los datos mediante claves primarias, claves foráneas, restricciones y relaciones entre entidades.

---

# Tablas

Las principales tablas del sistema serán:

- roles
- users
- categories
- products
- customers
- suppliers
- sales
- sale_details
- purchases
- purchase_details
- inventory_movements

---

# Tabla: roles

La tabla `roles` almacenará los diferentes roles disponibles dentro del sistema.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único |
| name | VARCHAR(50) | NOT NULL, UNIQUE | Nombre del rol |
| description | VARCHAR(255) | NULL | Descripción del rol |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Datos iniciales

La tabla tendrá inicialmente los siguientes registros:

| id | name | description |
|---|---|---|
| 1 | Administrador | Acceso completo al sistema |
| 2 | Empleado | Acceso limitado a operaciones del negocio |

---

# Relaciones 

Un rol puede pertenecer a múltiples usuarios.

```text
roles 1 ───────── N users


# Tabla: users

La tabla `users` almacenará los usuarios que podrán acceder al sistema.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único |
| role_id | BIGINT | FOREIGN KEY, NOT NULL | Rol asignado al usuario |
| name | VARCHAR(100) | NOT NULL | Nombre del usuario |
| email | VARCHAR(150) | NOT NULL, UNIQUE | Correo electrónico |
| password | VARCHAR(255) | NOT NULL | Contraseña almacenada mediante hash |
| status | BOOLEAN | DEFAULT TRUE | Indica si el usuario está activo |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Relaciones

Cada usuario pertenece a un único rol.

```text
users N ───────── 1 roles


# Tabla: categories

La tabla `categories` almacenará las categorías utilizadas para clasificar los productos del sistema.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único |
| name | VARCHAR(100) | NOT NULL, UNIQUE | Nombre de la categoría |
| description | VARCHAR(255) | NULL | Descripción de la categoría |
| status | BOOLEAN | DEFAULT TRUE | Indica si la categoría está activa |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Relaciones

Una categoría puede tener múltiples productos.

```text
categories 1 ───────── N products


# Tabla: products

La tabla `products` almacenará los productos disponibles para la venta y gestión del inventario.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único |
| category_id | BIGINT | FOREIGN KEY, NOT NULL | Categoría del producto |
| code | VARCHAR(50) | NOT NULL, UNIQUE | Código único del producto |
| name | VARCHAR(150) | NOT NULL | Nombre del producto |
| description | TEXT | NULL | Descripción del producto |
| purchase_price | DECIMAL(12,2) | NOT NULL | Precio de compra |
| sale_price | DECIMAL(12,2) | NOT NULL | Precio de venta |
| stock | INT | DEFAULT 0 | Existencia actual |
| minimum_stock | INT | DEFAULT 0 | Cantidad mínima de inventario |
| status | BOOLEAN | DEFAULT TRUE | Indica si el producto está activo |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Relaciones

Cada producto pertenece a una categoría.

```text
products N ───────── 1 categories


#. Tabla: customers

La tabla `customers` almacenará los clientes de la empresa.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único |
| first_name | VARCHAR(100) | NOT NULL | Nombre del cliente |
| last_name | VARCHAR(100) | NOT NULL | Apellidos del cliente |
| identification | VARCHAR(30) | UNIQUE, NULL | Identificación del cliente |
| phone | VARCHAR(30) | NULL | Número telefónico |
| email | VARCHAR(150) | UNIQUE, NULL | Correo electrónico |
| address | VARCHAR(255) | NULL | Dirección |
| status | BOOLEAN | DEFAULT TRUE | Estado del cliente |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Relaciones

Un cliente puede tener múltiples ventas.

```text
customers 1 ───────── N sales


# Tabla: suppliers

La tabla `suppliers` almacenará los proveedores de la empresa.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único |
| company_name | VARCHAR(150) | NOT NULL | Nombre de la empresa |
| contact_name | VARCHAR(100) | NULL | Persona de contacto |
| phone | VARCHAR(30) | NULL | Número telefónico |
| email | VARCHAR(150) | UNIQUE, NULL | Correo electrónico |
| status | BOOLEAN | DEFAULT TRUE | Estado del proveedor |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Relaciones

Un proveedor puede tener múltiples compras.

```text
suppliers 1 ───────── N purchases


# 9. Tabla: sales

La tabla `sales` almacenará la información general de cada venta realizada en el sistema.

Esta tabla representa la cabecera de una venta. Los productos asociados a cada venta se almacenarán en la tabla `sale_details`.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único de la venta |
| customer_id | BIGINT | FOREIGN KEY, NOT NULL | Cliente asociado |
| user_id | BIGINT | FOREIGN KEY, NOT NULL | Usuario que registra la venta |
| sale_date | DATETIME | NOT NULL | Fecha y hora de la venta |
| subtotal | DECIMAL(12,2) | NOT NULL | Subtotal de la venta |
| tax | DECIMAL(12,2) | NOT NULL | Impuesto |
| total | DECIMAL(12,2) | NOT NULL | Total de la venta |
| status | VARCHAR(20) | DEFAULT `completed` | Estado de la venta |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Relaciones

Una venta pertenece a un cliente.

```text
customers 1 ───────── N sales



# 10. Tabla: sale_details

La tabla `sale_details` almacenará los productos asociados a cada venta.

Esta tabla representa el detalle de una venta y permite que una venta contenga múltiples productos.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único |
| sale_id | BIGINT | FOREIGN KEY, NOT NULL | Venta asociada |
| product_id | BIGINT | FOREIGN KEY, NOT NULL | Producto vendido |
| quantity | INT | NOT NULL | Cantidad vendida |
| unit_price | DECIMAL(12,2) | NOT NULL | Precio del producto al momento de la venta |
| subtotal | DECIMAL(12,2) | NOT NULL | Cantidad multiplicada por precio |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Relaciones

Cada detalle pertenece a una venta.

```text
sales 1 ───────── N sale_details




# 11. Tabla: purchases

La tabla `purchases` almacenará la información general de las compras realizadas a los proveedores.

Esta tabla representa la cabecera de una compra. Los productos asociados se almacenarán en la tabla `purchase_details`.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único de la compra |
| supplier_id | BIGINT | FOREIGN KEY, NOT NULL | Proveedor asociado |
| user_id | BIGINT | FOREIGN KEY, NOT NULL | Usuario que registra la compra |
| purchase_date | DATETIME | NOT NULL | Fecha y hora de la compra |
| subtotal | DECIMAL(12,2) | NOT NULL | Subtotal |
| tax | DECIMAL(12,2) | NOT NULL | Impuesto |
| total | DECIMAL(12,2) | NOT NULL | Total |
| status | VARCHAR(20) | DEFAULT `completed` | Estado de la compra |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Relaciones

Una compra pertenece a un proveedor.

```text
suppliers 1 ───────── N purchases




# Tabla: purchase_details

La tabla `purchase_details` almacenará los productos asociados a cada compra.

Esta tabla representa el detalle de una compra y permite registrar múltiples productos dentro de una misma compra.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único |
| purchase_id | BIGINT | FOREIGN KEY, NOT NULL | Compra asociada |
| product_id | BIGINT | FOREIGN KEY, NOT NULL | Producto comprado |
| quantity | INT | NOT NULL | Cantidad comprada |
| unit_price | DECIMAL(12,2) | NOT NULL | Precio de compra al momento de la operación |
| subtotal | DECIMAL(12,2) | NOT NULL | Cantidad multiplicada por precio |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Relaciones

Cada detalle pertenece a una compra.

```text
purchases 1 ───────── N purchase_details




# Tabla: inventory_movements

La tabla `inventory_movements` almacenará el historial de movimientos realizados sobre el inventario.

Permitirá identificar cuándo, cuánto y por qué se modificó el stock de un producto.

## Campos

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id | BIGINT | PRIMARY KEY | Identificador único |
| product_id | BIGINT | FOREIGN KEY, NOT NULL | Producto afectado |
| user_id | BIGINT | FOREIGN KEY, NOT NULL | Usuario responsable |
| type | VARCHAR(20) | NOT NULL | Tipo de movimiento |
| quantity | INT | NOT NULL | Cantidad del movimiento |
| reference_type | VARCHAR(30) | NULL | Tipo de operación que originó el movimiento |
| reference_id | BIGINT | NULL | Identificador de la operación relacionada |
| notes | VARCHAR(255) | NULL | Observaciones |
| created_at | TIMESTAMP | | Fecha de creación |
| updated_at | TIMESTAMP | | Fecha de actualización |

## Tipos de movimiento

Los movimientos podrán ser:

- `IN`: entrada de inventario.
- `OUT`: salida de inventario.
- `ADJUSTMENT`: ajuste manual del inventario.

## Relaciones

Un producto puede tener múltiples movimientos de inventario.

```text
products 1 ───────── N inventory_movements
