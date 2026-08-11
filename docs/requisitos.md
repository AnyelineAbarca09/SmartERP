# SmartERP - Requisitos del Sistema

## 1. Descripción del proyecto

SmartERP es un sistema ERP (Enterprise Resource Planning) diseñado para facilitar la gestión de una pequeña empresa.

El sistema permitirá centralizar la administración de usuarios, productos, inventario, clientes, proveedores, compras y ventas en una única plataforma web.

El sistema estará compuesto por un frontend desarrollado con React y TypeScript, un backend desarrollado con Laravel y una base de datos MySQL.

---

# 2. Objetivos

## 2.1 Objetivo general

Desarrollar una aplicación web Full Stack que permita administrar de manera centralizada las principales operaciones de una pequeña empresa.

## 2.2 Objetivos específicos

- Gestionar usuarios y roles.
- Administrar productos y categorías.
- Controlar el inventario.
- Gestionar clientes y proveedores.
- Registrar compras.
- Registrar ventas.
- Actualizar automáticamente el inventario.
- Visualizar indicadores mediante un dashboard.
- Generar reportes.
- Implementar autenticación y autorización.
- Aplicar buenas prácticas de desarrollo de software.

---

# 3. Usuarios del sistema

El sistema tendrá inicialmente dos tipos de usuarios:

## 3.1 Administrador

El administrador tendrá acceso completo al sistema.

### Permisos

- Iniciar sesión.
- Cerrar sesión.
- Gestionar usuarios.
- Gestionar roles.
- Gestionar productos.
- Gestionar categorías.
- Gestionar clientes.
- Gestionar proveedores.
- Registrar compras.
- Registrar ventas.
- Consultar inventario.
- Consultar dashboard.
- Consultar reportes.

---

## 3.2 Empleado

El empleado tendrá acceso limitado a las operaciones necesarias para realizar sus funciones.

### Permisos

- Iniciar sesión.
- Cerrar sesión.
- Consultar productos.
- Registrar ventas.
- Registrar clientes.
- Consultar clientes.
- Consultar inventario.

### Restricciones

El empleado no podrá:

- Gestionar usuarios.
- Gestionar roles.
- Eliminar productos.
- Gestionar configuraciones administrativas.
- Acceder a funcionalidades exclusivas del administrador.

---

# 4. Módulos del sistema

## 4.1 Autenticación

El sistema deberá permitir:

- Iniciar sesión.
- Cerrar sesión.
- Validar credenciales.
- Generar tokens JWT.
- Proteger rutas privadas.
- Controlar el acceso según el rol del usuario.

---

# 4.2 Gestión de usuarios

El administrador podrá:

- Crear usuarios.
- Consultar usuarios.
- Editar usuarios.
- Activar usuarios.
- Desactivar usuarios.
- Asignar roles.

---

# 4.3 Gestión de productos

El sistema permitirá:

- Crear productos.
- Consultar productos.
- Editar productos.
- Desactivar productos.
- Buscar productos.
- Filtrar productos.
- Consultar existencias.
- Definir stock mínimo.

Cada producto tendrá:

- Código.
- Nombre.
- Descripción.
- Precio de compra.
- Precio de venta.
- Stock.
- Stock mínimo.
- Categoría.
- Estado.

---

# 4.4 Gestión de categorías

El sistema permitirá:

- Crear categorías.
- Consultar categorías.
- Editar categorías.
- Desactivar categorías.

Un producto pertenecerá a una categoría.

---

# 4.5 Gestión de clientes

El sistema permitirá:

- Crear clientes.
- Consultar clientes.
- Editar clientes.
- Desactivar clientes.
- Buscar clientes.

Cada cliente tendrá:

- Nombre.
- Apellidos.
- Identificación.
- Teléfono.
- Correo electrónico.
- Dirección.
- Estado.

---

# 4.6 Gestión de proveedores

El sistema permitirá:

- Crear proveedores.
- Consultar proveedores.
- Editar proveedores.
- Desactivar proveedores.
- Buscar proveedores.

Cada proveedor tendrá:

- Nombre de la empresa.
- Persona de contacto.
- Teléfono.
- Correo electrónico.
- Estado.

---

# 4.7 Gestión de compras

El sistema permitirá registrar compras realizadas a proveedores.

Una compra tendrá:

- Proveedor.
- Usuario que registra la compra.
- Fecha.
- Subtotal.
- Impuesto.
- Total.
- Detalles de la compra.

Cada detalle tendrá:

- Producto.
- Cantidad.
- Precio.
- Subtotal.

### Regla de negocio

Cuando una compra sea registrada correctamente, el stock de los productos involucrados deberá aumentar automáticamente.

---

# 4.8 Gestión de ventas

El sistema permitirá registrar ventas realizadas a clientes.

Una venta tendrá:

- Cliente.
- Usuario que registra la venta.
- Fecha.
- Subtotal.
- Impuesto.
- Total.
- Detalles de la venta.

Cada detalle tendrá:

- Producto.
- Cantidad.
- Precio.
- Subtotal.

### Regla de negocio

Cuando una venta sea registrada correctamente, el stock de los productos involucrados deberá disminuir automáticamente.

El sistema no deberá permitir vender una cantidad superior al stock disponible.

---

# 4.9 Gestión de inventario

El sistema deberá permitir:

- Consultar existencias.
- Consultar productos con stock bajo.
- Consultar productos agotados.
- Visualizar movimientos de inventario.

### Regla de negocio

El inventario se actualizará automáticamente mediante las operaciones de compra y venta.

---

# 4.10 Dashboard

El dashboard permitirá visualizar indicadores generales del negocio.

Se mostrarán inicialmente:

- Total de ventas.
- Total de compras.
- Cantidad de productos.
- Productos con stock bajo.
- Productos agotados.
- Clientes registrados.
- Ventas por período.
- Productos más vendidos.

---

# 4.11 Reportes

El sistema deberá permitir consultar:

## Reporte de ventas

Filtros:

- Fecha inicial.
- Fecha final.
- Cliente.
- Usuario.

## Reporte de compras

Filtros:

- Fecha inicial.
- Fecha final.
- Proveedor.
- Usuario.

## Reporte de inventario

Información:

- Producto.
- Stock actual.
- Stock mínimo.
- Estado del inventario.

---

# 5. Requisitos funcionales

| Código | Requisito |
|---|---|
| RF-001 | El sistema deberá permitir iniciar sesión. |
| RF-002 | El sistema deberá permitir cerrar sesión. |
| RF-003 | El administrador podrá gestionar usuarios. |
| RF-004 | El sistema permitirá gestionar productos. |
| RF-005 | El sistema permitirá gestionar categorías. |
| RF-006 | El sistema permitirá gestionar clientes. |
| RF-007 | El sistema permitirá gestionar proveedores. |
| RF-008 | El sistema permitirá registrar compras. |
| RF-009 | El sistema permitirá registrar ventas. |
| RF-010 | El sistema actualizará el inventario automáticamente. |
| RF-011 | El sistema permitirá consultar reportes. |
| RF-012 | El sistema mostrará un dashboard. |
| RF-013 | El sistema controlará el acceso según el rol. |
| RF-014 | El sistema impedirá ventas superiores al stock disponible. |

---

# 6. Requisitos no funcionales

## Seguridad

- Las contraseñas deberán almacenarse de forma segura.
- Las rutas privadas deberán estar protegidas.
- Se utilizará autenticación mediante JWT.
- El acceso a funcionalidades dependerá del rol del usuario.

## Rendimiento

- Las consultas deberán utilizar paginación cuando exista una gran cantidad de registros.
- Las búsquedas deberán estar optimizadas.

## Mantenibilidad

- El código deberá estar organizado por responsabilidades.
- Se aplicarán principios SOLID.
- Se utilizará una arquitectura por capas.
- Se utilizarán patrones de diseño cuando sean apropiados.

## Usabilidad

- La interfaz deberá ser responsive.
- Los formularios deberán mostrar mensajes de validación.
- Los errores deberán mostrarse de forma comprensible para el usuario.

---

# 7. Tecnologías

## Frontend

- React
- TypeScript
- Vite
- Tailwind CSS
- React Router
- Axios
- React Hook Form
- Zod
- TanStack Query

## Backend

- Laravel
- PHP
- API REST
- JWT

## Base de datos

- MySQL

## Control de versiones

- Git
- GitHub

---

# 8. Arquitectura

El sistema utilizará una arquitectura separada entre frontend, backend y base de datos.

```text
React + TypeScript
        |
        | HTTP / JSON
        v
Laravel REST API
        |
        v
MySQL