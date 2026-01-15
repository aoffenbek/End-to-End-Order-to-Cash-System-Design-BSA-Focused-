# TEST SCENARIOS & UAT SUPPORT (BSA CORE)

## 1. Purpose of This Document

This document demonstrates how a **Business Systems Analyst (BSA)** supports **system testing and User Acceptance Testing (UAT)** by:

* Translating requirements into test scenarios
* Defining clear expected results
* Ensuring traceability between requirements and tests

This artifact shows strong collaboration between **business, IT, and QA**.

---

## 2. Testing Scope

### In Scope

* Invoice validation
* Duplicate detection
* AR and Revenue posting
* Exception handling
* Analytics visibility

### Out of Scope

* Payment execution testing
* Performance stress testing
* Security penetration testing

---

## 3. Test Levels Overview

| Test Level                    | Responsibility   |
| ----------------------------- | ---------------- |
| Unit Test                     | Development Team |
| System Integration Test (SIT) | IT / QA          |
| User Acceptance Test (UAT)    | Business Users   |

---

## 4. Requirement-to-Test Traceability

| Requirement ID | Test Scenario ID |
| -------------- | ---------------- |
| BR-01          | TS-01, TS-02     |
| FR-02          | TS-01            |
| FR-04          | TS-03            |
| FR-06          | TS-05            |

---

## 5. Test Scenarios

### TS-01 – Duplicate Invoice Detection

**Related Requirement:** BR-01, FR-02
**Test Type:** UAT

**Given** an invoice with Invoice Number INV-1001 already exists
**When** the same invoice is submitted again
**Then** the system rejects the invoice and logs a duplicate exception

---

### TS-02 – Missing Mandatory Field

**Related Requirement:** FR-01
**Test Type:** UAT

**Given** an invoice is missing the Client ID
**When** the invoice is submitted
**Then** the system rejects the invoice and displays a validation error

---

### TS-03 – AR and Revenue Posting

**Related Requirement:** FR-04
**Test Type:** SIT

**Given** a valid invoice is submitted
**When** posting is executed in ERP
**Then** AR and Revenue are posted in the same accounting document

---

### TS-04 – Exception Visibility

**Related Requirement:** FR-06
**Test Type:** UAT

**Given** an invoice fails validation
**When** the finance user opens the dashboard
**Then** the invoice appears with an exception status

---

### TS-05 – Analytics Replication

**Related Requirement:** NFR-04
**Test Type:** SIT

**Given** an invoice is posted successfully
**When** data replication runs
**Then** the invoice appears in analytics within SLA

---

## 6. UAT Entry Criteria

* All critical SIT defects resolved
* Test data prepared
* Business users trained
* UAT environment available

---

## 7. UAT Exit Criteria

* All High priority defects resolved
* Business sign-off received
* Test evidence documented

---

## 8. Defect Classification

| Severity | Description                  |
| -------- | ---------------------------- |
| High     | Financial posting incorrect  |
| Medium   | Exception handling incorrect |
| Low      | UI or reporting issue        |

---

## 9. BSA Responsibilities in Testing

The Business Systems Analyst:

* Defines test scenarios
* Supports UAT execution
* Clarifies business rules
* Ensures traceability
* Supports go-live decision
