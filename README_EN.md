# 📌 Procedures, Functions, and Automation in MySQL

This repository contains a set of SQL scripts geared towards building business logic in MySQL, including the creation of custom functions, stored procedures, triggers, and automated data generation for a billing and sales system.

The project demonstrates how to structure complex processes within the database engine, maintaining integrity, automation, and consistency across different MySQL components.

---

# 📂 Contents
## 1. Database Structure

Includes the creation of tables related to a sales system:

- customers
- products
- invoices
- items
- billing

Primary keys, foreign keys, and basic referential integrity configuration are incorporated.

## 2. Custom Functions (UDFs)

Functions are developed that encapsulate logic and facilitate automated tasks, such as:

- Generation of controlled random values
- Dynamic selection of customers, products, or salespeople
- Calculation of values ​​associated with sales

Functions are implemented to make the system more dynamic:

🔹 f_random(min, max)
Generates random integer values ​​within a range.

🔹 f_random_customer()
Returns a random customer from the customers table.

🔹 f_random_product()
Selects a product at random.

🔹 f_random_salesperson()
Returns a salesperson at random.

## 3. Stored Procedures

The repository includes procedures designed to:

- Automatically create complete sales
- Insert items associated with invoices
- Generate large volumes of synthetic data for testing
- Execute business logic without relying on external applications

The main stored procedure, sp_venta, constructs a sale from start to finish, including random selection of entities, quantity of items, prices, and tax calculations.

The main stored procedure is defined as follows:

🔧 sp_venta(fecha, maxitems, maxcantidad)

The procedure:

- Creates a new invoice.

- Automatically selects a random customer, salesperson, and products.

- Determines the number of items on the invoice.

- Inserts quantities and prices.

- Prevents duplicate products on the same invoice.

- Calculates the tax.

This stored procedure allows you to generate thousands of simulated sales for analysis, dashboards, or testing.

## 4. Automation with Triggers

A trigger structure is implemented to keep a daily billing table updated.

The triggers react to INSERT, UPDATE, and DELETE operations on the items table and execute a procedure responsible for recalculating the totals by date.

This allows for the generation of a consolidated, real-time record, useful for analysis, audits, or integration with dashboards.

The table is created:
```bash
billing (date, total_sale)
```

And triggers are implemented to keep it always updated:

- TG_BILLING_INSERT
- TG_BILLING_UPDATE
- TG_BILLING_DELETE

Each one reacts to changes in the items table and executes:

🔄 sp_triggers

Automatically recalculates the total sales by date.

This turns the billing table into a materialized view updated in real time.

---

# 🧪 Main Use Case

The combination of functions, procedures, and triggers allows you to:

- Generate realistic test data
- Simulate transactions for analysis or model validation
- Automate calculations and internal database processes
- Develop sales system prototypes without an external interface

This is a useful approach for testing environments, data engineering projects, pipeline validation, or learning advanced SQL logic.

--

# 🚀 Basic Execution

To generate an automatic sale:

```bash
CALL sp_venta('20210622', 15, 100);

``

To view the generated totals:

```bash
SELECT * FROM facturacion;

` ... ```
---

# 🧠 What I Learned

This section of the course covered the following in depth:

- Advanced use of stored procedures
- Creation and application of custom functions
- Automatic generation of data for testing
- Implementation of triggers to automate processes
- Use of RAND(), FLOOR(), and techniques for selecting random records
- Handling large volumes of simulated inserts
- Design of complete logic:
functions → procedures → triggers → final billing
