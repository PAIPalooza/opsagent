# 📚 Backlog for OSAZ Ops Agent MVP

**Sprint Theme:** Credit Automation & Survey Agent for SPF Test Kit Customers

---

## 🧩 EPIC 1: Purchase Verification

> ✅ *Verify that a customer purchased the SPF sample kit using Shopify APIs and store that customer/order in the database.*

### 🔹 User Story 1.1 – Verify SPF Kit Purchase

* **As** a customer
* **I want** the system to confirm I’ve bought a test kit
* **So that** I can unlock my product credit

**Tasks:**

* [ ] Build `/verify-order` FastAPI endpoint
* [ ] Connect to Shopify Orders API using email or order ID
* [ ] Parse response for SPF kit product
* [ ] Return result to Langflow or bot
* [ ] Store customer + order in `customers` and `orders` tables

---

## 🧩 EPIC 2: Survey Collection via Langflow Agent

> ✅ *Guide the customer through a survey to collect shade matching data, feedback, and skincare goals.*

### 🔹 User Story 2.1 – Take Survey for Credit

* **As** a customer
* **I want** to complete a fun and short skincare survey
* **So that** I can get a credit toward my SPF purchase

**Tasks:**

* [ ] Build Langflow prompt chain with 5–6 questions
* [ ] Store survey responses via FastAPI `/submit-survey`
* [ ] Save results in `surveys` table
* [ ] Set up logic to identify shade match + finish preference
* [ ] Capture data for analytics & AI training

---

## 🧩 EPIC 3: Discount Generation & Cart Prefill

> ✅ *Generate a unique discount code and send the customer a pre-filled cart based on survey results.*

### 🔹 User Story 3.1 – Get Discount After Survey

* **As** a customer
* **I want** to receive a ₦3,000 discount code automatically
* **So that** I can purchase the full-size product at a lower cost

**Tasks:**

* [ ] Create `/generate-discount` FastAPI endpoint
* [ ] Integrate with Shopify Discounts API
* [ ] Log generated discount in `discounts` table
* [ ] Set expiry for discount (e.g., 7 days)

---

### 🔹 User Story 3.2 – Pre-Fill Cart Based on Survey

* **As** a customer
* **I want** my matched product and add-ons pre-filled in my cart
* **So that** I don’t have to search for them manually

**Tasks:**

* [ ] Generate dynamic cart URLs
* [ ] Add recommended shade + optional serum
* [ ] Store in `recommendations` table

---

## 🧩 EPIC 4: Conversion Logging + Follow-Up

> ✅ *Track whether customers used the discount and purchased, and re-engage if they don’t.*

### 🔹 User Story 4.1 – Track My Redemption Status

* **As** the ops team
* **I want** to know which customers redeemed their credit
* **So that** I can track conversion rates

**Tasks:**

* [ ] Create `/log-conversion` endpoint
* [ ] Listen for Shopify webhook or capture checkout from frontend
* [ ] Store results in `conversions` table
* [ ] Link to survey + discount records

---

### 🔹 User Story 4.2 – Send Follow-Up If They Don’t Convert

* **As** a customer
* **I want** a reminder if I don’t use my credit
* **So that** I don’t miss out

**Tasks:**

* [ ] Schedule 48-hour reminder logic
* [ ] If conversion not logged, trigger automated DM (via Zapier or ManyChat API)
* [ ] Personalize with shade + cart link

---

## 🧩 EPIC 5: Data Infrastructure & Storage

> ✅ *Ensure all customer interactions, orders, survey data, and conversions are logged to PostgreSQL.*

### 🔹 User Story 5.1 – Log All Survey & Order Data

* **As** a data engineer
* **I want** all interactions saved to the DB
* **So that** we can analyze shade performance and feed our AI model

**Tasks:**

* [ ] Create SQL schema: `customers`, `orders`, `surveys`, `discounts`, `recommendations`, `conversions`
* [ ] Write CRUD methods in FastAPI
* [ ] Seed test data and validate schema relationships

---

## 🧩 EPIC 6: Agent & API Integration

> ✅ *Tie everything together with Langflow agent logic, FastAPI backend, and Shopify.*

### 🔹 User Story 6.1 – Connect Langflow to API Backend

* **As** a developer
* **I want** the Langflow agent to POST data to the backend
* **So that** the flow triggers all core logic without manual dev input

**Tasks:**

* [ ] Connect `/verify-order` to Langflow entry node
* [ ] Send survey responses to `/submit-survey`
* [ ] On completion, call `/generate-discount`
* [ ] Output cart URL + recommendation back to user

---

## 🧩 EPIC 7: QA & Testing

> ✅ *Validate that the full user flow works from start to finish with at least 5 test users.*

### 🔹 User Story 7.1 – Test Complete User Journey

* **As** the QA team
* **I want** to simulate customer flows and check for failures
* **So that** we catch bugs before launch

**Tasks:**

* [ ] Test happy path: order → survey → discount → purchase
* [ ] Test invalid order ID
* [ ] Test duplicate entries
* [ ] Confirm database logs and cart link integrity

---

## ✅ PRIORITY BACKLOG OVERVIEW

| Epic                  | User Story | Priority        | Time Estimate |
| --------------------- | ---------- | --------------- | ------------- |
| Purchase Verification | 1.1        | 🟥 High         | 1.5 hrs       |
| Survey Collection     | 2.1        | 🟥 High         | 2 hrs         |
| Discount Creation     | 3.1        | 🟥 High         | 1 hr          |
| Cart Prefill          | 3.2        | 🟧 Medium       | 1 hr          |
| Conversion Logging    | 4.1        | 🟥 High         | 1 hr          |
| Follow-Up Reminders   | 4.2        | 🟨 Nice-to-Have | 1 hr          |
| Database Setup        | 5.1        | 🟥 High         | 1 hr          |
| Langflow Integration  | 6.1        | 🟥 High         | 2 hrs         |
| QA Testing            | 7.1        | 🟥 High         | 1 hr          |

---
