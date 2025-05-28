# 🚀 One-Day Agile Sprint Plan – **OSAZ Ops Agent MVP**

## 🧠 Sprint Goal:

**Build and deploy an end-to-end MVP of the OSAZ Ops Agent using FastAPI, Langflow, PostgreSQL, and Shopify APIs.**

---

## 🕐 Timeline: **8 AM – 8 PM**

(12 hours, sprint + polish)

---

## ✅ Prerequisites (Complete before 8 AM)

* Postgres DB running (e.g., Supabase or Docker container)
* Langflow environment ready
* Shopify API key access with test product + test order
* FastAPI project initialized (venv + basic folder structure)

---

## 🔄 Sprint Breakdown by Hour

### 🕗 **8:00 – 9:00 AM** — *Kickoff + Schema Setup*

**Goal:** Set up Postgres schema and FastAPI project structure

**Tasks:**

* [ ] Create SQL tables: `customers`, `orders`, `surveys`, `discounts`, `recommendations`, `conversions`
* [ ] Use Alembic or SQLAlchemy for migrations
* [ ] Scaffold FastAPI endpoints:

  * `/verify-order`
  * `/submit-survey`
  * `/generate-discount`
  * `/recommend-product`
  * `/log-conversion`

**Owner(s):** Backend Dev

---

### 🕘 **9:00 – 10:30 AM** — *Build Shopify Integration + Order Verification*

**Goal:** Verify SPF kit purchase by calling Shopify API

**Tasks:**

* [ ] Hit Shopify Orders API using email/order ID
* [ ] Match order for “shade\_kit” product
* [ ] Return order metadata to Langflow or frontend
* [ ] Log order + customer in DB if new

**Owner(s):** Backend Dev

---

### 🕥 **10:30 – 12:00 PM** — *Langflow Survey Agent Build*

**Goal:** Use Langflow to guide the user through a conversational SPF survey

**Tasks:**

* [ ] Define prompt flow with GPT-4:

  * Ask for shade match
  * Texture feedback
  * Skin type + concerns
  * Finish preference
  * Add-on interest
* [ ] Capture responses in Langflow memory
* [ ] POST results to `/submit-survey`

**Owner(s):** AI/Agent Engineer

---

### 🕛 **12:00 – 1:00 PM** — *LUNCH + Standup Check-In*

Review progress. Identify any blockers. Swap tasks if necessary.

---

### 🕐 **1:00 – 2:30 PM** — *Discount Code + Recommendation Flow*

**Goal:** Automate discount code generation and cart creation

**Tasks:**

* [ ] Connect to Shopify Discounts API
* [ ] Create unique ₦3K / \$5 discount per user
* [ ] Save in `discounts` table
* [ ] Generate pre-filled cart URL with shade match + add-ons
* [ ] Store in `recommendations` table

**Owner(s):** Backend Dev + Shopify Engineer (or same person)

---

### 🕝 **2:30 – 3:30 PM** — *Frontend or Message Bot Testing*

**Goal:** Connect flow to WhatsApp/IG DM or simulate frontend form

**Tasks:**

* [ ] Use ManyChat or Postman to simulate survey trigger
* [ ] Trigger Langflow via webhook or Slackbot (if DM isn't ready)
* [ ] Test full journey: order verify → survey → discount → cart

**Owner(s):** QA/Dev

---

### 🕞 **3:30 – 5:00 PM** — *Data Logging + Conversion Tracking*

**Goal:** Ensure all data is logged for ops + future AI training

**Tasks:**

* [ ] Log `surveys` to DB from Langflow
* [ ] Log discount code + cart links
* [ ] Capture post-purchase webhook or POST to `/log-conversion`
* [ ] Send 48hr follow-up message logic (placeholder)

**Owner(s):** Backend Dev + Agent Dev

---

### 🕔 **5:00 – 6:00 PM** — *Testing + Edge Cases*

**Goal:** Make sure it doesn’t break. Handle edge cases.

**Tasks:**

* [ ] Invalid order handling
* [ ] Partial survey completion
* [ ] Discount already applied
* [ ] Cart abandonment
* [ ] Double responses from same user

**Owner(s):** QA/Dev Team

---

### 🕕 **6:00 – 7:00 PM** — *Demo Prep + Internal Launch*

**Goal:** Build a basic test report and give Osaz a demo

**Tasks:**

* [ ] Create test user + flow walkthrough
* [ ] Screen record demo
* [ ] Summarize known bugs
* [ ] Load test with 5–10 dummy customers

**Owner(s):** Everyone

---

### 🕖 **7:00 – 8:00 PM** — *Docs + Debrief*

**Goal:** Final handoff, documentation, and next sprint prep

**Tasks:**

* [ ] Write quick README with API usage and DB schema
* [ ] Document Langflow blocks
* [ ] Set up Trello/Notion board for follow-up bugs + V2 features
* [ ] Save Langflow JSON chain
* [ ] Plan: push to staging server (Heroku, Railway, etc.)

---

## 🎯 Deliverables by End of Day

* [x] Working API for order → survey → discount → recommendation
* [x] Langflow-powered conversational agent for SPF quiz
* [x] Data logged to Postgres
* [x] Pre-filled Shopify cart link generation
* [x] Manual test/demo of 5 users
* [x] Internal demo video + next steps list

---

## 💡 Optional Next-Day Tasks

* Add 48hr follow-up bot
* Add frontend mini-dashboard
* Improve cart logic to include inventory checks
* A/B test different survey tones

---
