# FactoryFlow: Order-to-Audit Manufacturing Management System

An end-to-end prototype built to manage operations for a small South Indian snack manufacturer—taking workflows from a field salesman's order through raw material procurement, batch production, GST invoicing, and dispatch to the monthly auditor's report.



---

## Tech Stack
* **Frontend:** React, TypeScript, Vite, Tailwind CSS
* **Backend:** Python, FastAPI, SQLAlchemy, Alembic
* **Database:** PostgreSQL

---

## Core Architecture & Design Decisions
* **Ledger-Based Inventory:** Stock balances are derived dynamically from an append-only `stock_movements` ledger (`SUM(movements)` per item) rather than mutable balance columns, ensuring full auditability across raw materials, packaging, and finished goods.
* **Costing Method (Weighted Average):** Raw material consumption is valued using **weighted-average costing** (treating inventory as a single cost pool and recalculating unit cost upon each purchase receipt) so production variance and spoilage remain transparent.
* **Precision Arithmetic:** All monetary values are stored as integer paise (`BIGINT`) and quantities as `NUMERIC(14,3)` (`Decimal` in Python)—floating-point arithmetic is strictly avoided.
* **Versioned BOMs & Unit Conversions:** Production runs lock onto the active Bill of Materials (`bom_versions`) at creation, preserving historical cost accuracy alongside explicit unit conversions (e.g., `1 carton = 20 packets`).

---

## Role-Based Workflows
* **Salesman (Mobile-First):** Customer lookup, order creation, order tracking, and personal sales summary.
* **Admin:** Order approval, stock availability checks, GST invoice generation (PDF), dispatch tracking, payment allocation, and master data management.
* **Production:** BOM management, material receipts/issues, batch production runs, and planned-vs-actual variance tracking.
* **Accountant (Read-Only):** Sales, GST, purchase, stock ledger, production variance, collections, and ageing reports with CSV/Excel/PDF exports.
* **Owner:** Executive dashboard tracking orders, stock levels, variance alerts, cost per packet, and receivables.

---

## Project Status
🚧 **In Active Development** — Initial repository structure and database setup complete. Local setup commands, benchmark verification results, and architecture notes will be added as each module is completed.