# 📄 Product Requirements Document (PRD)

**Product Name:**
**OSAZ Ops Agent v1** – *Shade Concierge & Credit Automation*

**Version:**
`v0.1 – MVP`

**Prepared By:**
Osazomon Imarenezor

**Date:**
May 28, 2025

---

## 🧠 Problem Statement

Customers who purchase the OSAZ SPF Shade Test Kit are:

* Not consistently completing the follow-up survey,
* Not redeeming their product credit,
* Causing a gap in AI training data and a drop-off in sales conversions.

We need an intelligent Ops Agent that automates this entire workflow — verifies purchase, collects survey data, applies product credit, and nudges toward checkout.

---

## 🎯 Goals

* Verify SPF kit purchases via Shopify
* Guide users through a branded, AI-powered survey
* Apply ₦3,000 / \$5 credit toward full-size SPF
* Recommend shade + upsells based on survey input
* Log and store data in PostgreSQL for AI + ops use
* Increase full-size product conversions

---

## 👥 Target Users

* **Consumers** who purchased the sample kit
* **OSAZ Ops Team** (internal dashboard access)
* **AI Training Team** (data pipeline access)

---

## 🧱 Tech Stack

| Layer               | Tech Used                                          |
| ------------------- | -------------------------------------------------- |
| Backend API         | FastAPI (Python 3.11+)                             |
| DB Storage          | PostgreSQL (Cloud or Supabase)                     |
| Messaging           | ManyChat, WhatsApp API, or Instagram DM automation |
| AI Workflow         | Langflow (Langchain orchestration) + OpenAI API    |
| Frontend (Optional) | React (for dashboard admin access in later phases) |

---

## 🔁 End-to-End User Flow

### 🎯 Trigger:

Customer receives SPF shade test kit → 3–5 days later, they get an automated DM or SMS:

> “Hey \[First Name]! Ready to get your perfect match? 🌞 Take a quick 2-min skin survey and I’ll hook you up with ₦3,000 off your full-size SPF!”

---

### 🧩 Agent Flow:

#### 1. **Purchase Verification**

* Input: Email, phone, or order ID
* Query Shopify Orders API to verify kit purchase
* If invalid → polite error message
* If valid → move to survey flow

#### 2. **Survey Collection (Langflow Chain)**

* Ask:

  1. Which shade matched best?
  2. How did it feel on your skin?
  3. Any skin concerns you’re trying to target?
  4. Desired finish? (Matte, dewy, natural glow)
  5. Would you like to add hyperpigmentation or retinoid treatment?

* Store all responses in **PostgreSQL** under `customer_surveys`

#### 3. **Credit Creation**

* On survey completion:

  * Generate unique, one-time discount code via **Shopify Discounts API**
  * Amount: ₦3,000 or \$5
  * Apply to pre-filled cart URL with correct shade + upsell offer

#### 4. **Checkout Nudge**

* Respond with:

> “All done! Your match is shade \[X]. I’ve added it to your cart with ₦3K off. Want me to include a fade serum at 10% off too?”

Buttons:

* 🛒 Checkout Now (cart prefilled)
* ➕ Add Serum & Checkout
* 🔁 Browse Other Products

#### 5. **Follow-Up if No Conversion**

* After 48 hrs → DM:

> “Hey! Your shade is still waiting for you 🧴. Don’t miss out—your ₦3,000 credit expires in 48 hours!”

---

## 🗄️ Database Schema (PostgreSQL)

### Table: `customer_surveys`

| Field                     | Type      |
| ------------------------- | --------- |
| id                        | UUID (PK) |
| customer\_email           | Text      |
| phone\_number             | Text      |
| order\_id                 | Text      |
| shade\_selected           | Text      |
| skin\_concerns            | Text\[]   |
| texture\_feedback         | Text      |
| finish\_preference        | Text      |
| add\_on\_interest         | Text      |
| survey\_completed\_at     | Timestamp |
| discount\_code            | Text      |
| discount\_expires\_at     | Timestamp |
| cart\_url                 | Text      |
| converted\_to\_full\_size | Boolean   |

---

## 📈 Success Metrics (MVP)

| KPI                           | Target                  |
| ----------------------------- | ----------------------- |
| Survey Completion Rate        | ≥ 65%                   |
| Credit Redemption Rate        | ≥ 40%                   |
| Full-size SPF Conversion Rate | ≥ 30%                   |
| Time to Complete Flow         | < 3 minutes             |
| Data Captured for AI          | ≥ 100 new entries/month |

---

## 🧠 Internal Admin Features (Post-MVP, Optional)

* Weekly CSV export of all survey + conversion data
* Trend analysis on most popular shades
* Bounce analysis for funnel drop-off
* Top-requested add-ons (e.g., hyperpigmentation serum)

---

## 📅 Implementation Timeline

| Week   | Milestone                                               |
| ------ | ------------------------------------------------------- |
| Week 1 | Set up Langflow blocks, survey logic, FastAPI endpoints |
| Week 2 | Shopify API integration (verify + discounts)            |
| Week 3 | PostgreSQL schema setup + test automation               |
| Week 4 | DM trigger automation + test with live users            |
| Week 5 | Launch to 50 sample kit customers                       |
| Week 6 | Analyze data + iterate on agent tone, logic             |

---
