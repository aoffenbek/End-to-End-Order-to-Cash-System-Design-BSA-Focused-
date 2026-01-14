# WEEK 3 – SYSTEM ARCHITECTURE & RESPONSIBILITIES

## 1. Purpose of This Document

This document defines the **logical system architecture** supporting the Invoice-to-Cash (I2C) process.

The goal is to:

* Clearly separate system responsibilities
* Avoid overlapping ownership
* Ensure financial correctness and auditability
* Support analytics and operational monitoring

This is a **logical architecture**, not a physical or technical deployment diagram.

---

## 2. System Landscape Overview

The I2C process is supported by five main logical components:

1. Client / External Systems
2. Invoice Intake System
3. Accounting ERP (SAP-like)
4. Data Platform
5. Power BI (Analytics & Control)

Each system has a **single primary responsibility**.

---

## 3. Logical Architecture Diagram – Invoice-to-Cash

![I2C Logical System Architecture](../diagrams/I2C_Logical_System_Architecture.png)

The diagram above shows the logical system landscape supporting the Invoice-to-Cash process. It emphasizes clear system boundaries, one-directional data flow, and separation between transactional processing and analytical control.

---

## 4. System Responsibilities

### 4.1 Client / External Systems

**Primary responsibility:** Invoice creation

Responsibilities:

* Create invoices
* Provide mandatory invoice data
* Submit invoices through agreed channel

Out of scope:

* Validation rules
* Accounting logic
* Data corrections

---

### 4.2 Invoice Intake System

**Primary responsibility:** Invoice validation and control

Responsibilities:

* Validate invoice format and mandatory fields
* Detect duplicate invoices
* Enforce pre-accounting business rules
* Reject invalid invoices

Design principle:

* No financial postings occur here

---

### 4.3 Accounting ERP (SAP-like)

**Primary responsibility:** Financial posting and legal accounting

Responsibilities:

* Post Accounts Receivable
* Post revenue according to accounting rules
* Generate accounting document IDs
* Maintain audit trail

Design principle:

* Single source of truth for financial data

---

### 4.4 Data Platform

**Primary responsibility:** Data consolidation and history

Responsibilities:

* Replicate transactional data
* Preserve immutable records
* Enable reconciliation and analytics

Design principle:

* No business logic changes
* Read-only analytical layer

---

### 4.5 Power BI (Analytics & Control Layer)

**Primary responsibility:** Monitoring and control

Responsibilities:

* Monitor invoice lifecycle
* Highlight exceptions
* Calculate reconciliation KPIs
* Support operational and audit users

Design principle:

* Detect issues, do not fix them

---

## 5. Source of Truth Definition

| Data Type           | Source of Truth |
| ------------------- | --------------- |
| Invoice header data | Accounting ERP  |
| Accounting postings | Accounting ERP  |
| Revenue recognition | Accounting ERP  |
| Analytical KPIs     | Power BI        |

The Data Platform acts as a **replica**, not a master.

---

## 6. Integration Points

| From          | To            | Purpose               |
| ------------- | ------------- | --------------------- |
| Client        | Intake System | Invoice submission    |
| Intake System | ERP           | Approved invoices     |
| ERP           | Data Platform | Financial replication |
| Data Platform | Power BI      | Analytics dataset     |

Integrations are **one-directional** to reduce risk.

---

## 7. Error Handling Boundaries

| Error Type               | Where Detected | Where Fixed     |
| ------------------------ | -------------- | --------------- |
| Invalid invoice          | Intake System  | Client / Intake |
| Duplicate invoice        | Intake System  | Intake          |
| Posting failure          | ERP            | ERP             |
| Missing analytics record | Power BI       | Data Platform   |

Errors are resolved **as close to their origin as possible**.

---

## 8. Architecture Risks & Mitigations

| Risk               | Mitigation                       |
| ------------------ | -------------------------------- |
| Double posting     | ERP document ID enforcement      |
| Data inconsistency | Single financial source of truth |
| Silent failures    | Control dashboards               |
| Manual corrections | Audit logging                    |

---

## 9. BSA Rationale

This architecture:

* Reduces financial risk
* Improves transparency
* Enables scalable analytics
* Supports audit and compliance

System boundaries are explicit, preventing responsibility gaps.
