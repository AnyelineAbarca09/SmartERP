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