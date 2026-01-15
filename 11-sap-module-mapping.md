# SAP MODULE MAPPING (FI / SD CONTEXT)

## 1. Purpose of This Document

This document maps the **Invoice-to-Cash (I2C)** Business Systems Analysis artifacts to **SAP FI and SD modules**.

The goal is to demonstrate how a BSA with **basic SAP knowledge** can still:

* Speak SAP language
* Understand module responsibilities
* Bridge business processes with SAP configuration and data

---

## 2. SAP Modules in Scope

| SAP Module                    | Role in I2C                    |
| ----------------------------- | ------------------------------ |
| SAP SD (Sales & Distribution) | Billing and invoice generation |
| SAP FI (Financial Accounting) | AR and revenue posting         |
| SAP CO (optional)             | Profitability analysis         |

---

## 3. Process-to-SAP Mapping

| I2C Step           | SAP Module | SAP Object          |
| ------------------ | ---------- | ------------------- |
| Invoice creation   | SD         | Billing Document    |
| Invoice posting    | FI         | Accounting Document |
| AR update          | FI         | Customer Line Item  |
| Revenue posting    | FI         | G/L Posting         |
| Exception handling | SD / FI    | Block / Status      |

---

## 4. Data Object Mapping

| Business Entity     | SAP Table / Object |
| ------------------- | ------------------ |
| Invoice             | VBRK / VBRP        |
| Accounting Document | BKPF / BSEG        |
| Accounts Receivable | BSID / BSAD        |
| Revenue             | G/L Accounts       |
| Customer            | KNA1               |

*Note: Table names are indicative and used for conceptual understanding.*

---

## 5. Reconciliation in SAP Context

| Reconciliation Area  | SAP View             |
| -------------------- | -------------------- |
| Invoice vs AR        | SD Billing vs FI AR  |
| AR Aging             | FI Line Item Reports |
| Revenue completeness | FI G/L vs CO         |
| ERP vs Analytics     | SAP Extracts         |

---

## 6. KPIs in SAP Language

| KPI                  | SAP Perspective       |
| -------------------- | --------------------- |
| Posting success rate | FI document status    |
| AR aging             | FBL5N-style reporting |
| Duplicate invoices   | SD billing controls   |
| Revenue completeness | FI G/L balance        |

---

## 7. Change Management – SAP Impact

| Change Type        | SAP Impact               |
| ------------------ | ------------------------ |
| Validation rule    | SD billing config        |
| Posting logic      | FI account determination |
| New KPI            | SAP extract / BW         |
| Exception workflow | SAP status handling      |

---

## 8. BSA Positioning with SAP

This document demonstrates that the BSA:

* Understands SAP modular separation
* Does not configure SAP, but **defines requirements clearly**
* Works effectively with SAP consultants and developers
