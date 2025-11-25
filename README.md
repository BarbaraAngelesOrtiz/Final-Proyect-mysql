# 📌 Procedures, Funciones y Automatización en MySQL

Este repositorio contiene un conjunto de scripts SQL orientados a la construcción de lógica de negocio en MySQL, incluyendo la creación de funciones personalizadas, procedimientos almacenados, triggers y generación automatizada de datos para un sistema de facturación y ventas.

El proyecto demuestra cómo estructurar procesos complejos dentro del motor de base de datos, manteniendo integridad, automatización y consistencia a través de diferentes componentes de MySQL.

---

# 📂 Contenido
## 1. Estructura de Base de Datos

Incluye la creación de tablas relacionadas con un sistema de ventas:

- clientes
- productos
- facturas
- items
- facturacion

Se incorporan claves primarias, claves foráneas y configuración básica de integridad referencial.

## 2. Funciones Personalizadas (UDFs)

Se desarrollan funciones que encapsulan lógica y facilitan tareas automatizadas, como:

- Generación de valores aleatorios controlados
- Selección dinámica de clientes, productos o vendedores
- Cálculo de valores asociados a las ventas

Se implementan funciones que dinamizan el sistema:

🔹 f_aleatorio(min, max)
Genera valores aleatorios enteros entre un rango.

🔹 f_cliente_aleatorio()
Retorna un cliente aleatorio de la tabla clientes.

🔹 f_producto_aleatorio()
Selecciona un producto al azar.

🔹 f_vendedor_aleatorio()
Devuelve un vendedor en forma aleatoria.


## 3. Procedimientos Almacenados

El repositorio incluye procedimientos diseñados para:

- Crear ventas completas de forma automática
- Insertar ítems asociados a facturas
- Generar grandes volúmenes de datos sintéticos para pruebas
- Ejecutar la lógica de negocio sin depender de aplicaciones externas

El procedimiento principal, sp_venta, realiza la construcción de una venta de inicio a fin, incluyendo selección aleatoria de entidades, cantidad de ítems, precios y cálculos de impuestos.

Se desarrolla el stored procedure principal:

🔧 sp_venta(fecha, maxitems, maxcantidad)

El procedimiento:

- Crea una factura nueva.
- Selecciona automáticamente cliente, vendedor y productos aleatorios.
- Determina cuántos ítems tendrá la factura.
- Inserta cantidades y precios.
- Evita duplicación de productos en una misma factura.
- Calcula el impuesto.

Este SP permite generar miles de ventas simuladas para análisis, dashboards o pruebas.

## 4. Automatización con Triggers

Se implementa una estructura de triggers que mantiene actualizada una tabla de facturación diaria.
Los triggers reaccionan a operaciones INSERT, UPDATE y DELETE sobre la tabla items y ejecutan un procedimiento encargado de recalcular los totales por fecha.

Esto permite generar un registro consolidado en tiempo real, útil para análisis, auditorías o integración con dashboards.

Se crea la tabla:
```bash
facturacion (fecha, venta_total)
```

Y se implementan triggers para mantenerla siempre actualizada:

- TG_FACTURACION_INSERT
- TG_FACTURACION_UPDATE
- TG_FACTURACION_DELETE

Cada uno reacciona a cambios en la tabla items y ejecuta:

🔄 sp_triggers

Recalcula automáticamente el total de ventas por fecha.
Esto convierte la tabla facturacion en un materialized view actualizado en tiempo real.

---

# 🧪 Caso de Uso Principal

La combinación de funciones, procedimientos y triggers permite:

- Generar datos de prueba realistas
- Simular transacciones para análisis o validación de modelos
- Automatizar cálculos y procesos internos de una base de datos
- Desarrollar prototipos de sistemas de ventas sin interfaz externa

Es un enfoque útil para entornos de pruebas, proyectos de Data Engineering, validación de pipelines o aprendizaje de lógica SQL avanzada.

---

# 🚀 Ejecución Básica

Para generar una venta automática:

```bash
CALL sp_venta('20210622', 15, 100);
```

Para ver los totales generados:

```bash
SELECT * FROM facturacion;
```
---

# 🧠 Lo aprendido 

En este tramo del curso se profundizó en:

- Uso avanzado de stored procedures
- Creación y aplicación de funciones personalizadas
- Generación automática de datos para pruebas
- Implementación de triggers para automatizar procesos
- Uso de RAND(), FLOOR() y técnicas para seleccionar registros aleatorios
- Manipulación de grandes volúmenes de inserciones simuladas
- Diseño de lógica completa:
funciones → procedimientos → triggers → facturación final

---
```
# 📂 Estructura del repositorio/
├── RecuperacionAmbiente/
│     ├── Carga_Facturas_01.csv
│     ├── Carga_Facturas_02.csv
│     ├── Carga_Facturas_03.csv
│     ├── Carga_Tablas_Registros.sql
│     ├── Comandos_Aula_1.sql
│     ├── Creacion_Esquema.sql
│     ├── LIMIT.sql
│     ├── Problema_Primary_Key.sql
│     ├── Stored_Procedures_y_Triggers.sql
│     ├── Triggers.sql
│     ├── comandos.sql
│     ├── funcion_RAND.sql
│     ├── inclusion_productos.sql
│     ├── venta.sql
│     ├── vendedores.csv
│     └── DumpJugosVentas/
│           ├── jugos_ventas_facturas.sql
│           ├── jugos_ventas_items_facturas.sql
│           ├── jugos_ventas_tabla_de_clientes.sql
│           ├── jugos_ventas_tabla_de_productos.sql
│           └── jugos_ventas_tabla_de_vendedores.sql
│
├── comandos.sql
├── schema.png
│ 
└──  README.md      
```
--- 

![MySQL](https://img.shields.io/badge/MySQL-4D8BBE?style=flat&logo=mysql&logoColor=white)
![Last Commit](https://img.shields.io/github/last-commit/USER/REPO)
![Status](https://img.shields.io/badge/Status-Completed-blue)





