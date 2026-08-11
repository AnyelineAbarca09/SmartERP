# Diseño de Base de Datos - SmartERP

## 1. Introducción

La base de datos de SmartERP utilizará MySQL como sistema gestor de base de datos relacional.

El diseño seguirá un modelo relacional y buscará mantener la integridad de los datos mediante claves primarias, claves foráneas, restricciones y relaciones entre entidades.

---

# 2. Tablas

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

# 3. Tabla: roles

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

# 4. Relaciones

Un rol puede pertenecer a múltiples usuarios.

```text
roles 1 ───────── N users