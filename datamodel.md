## 🧬 OSAZ Ops Agent – PostgreSQL Data Model

---

### 🧑 `customers`

| Field                 | Type         | Description                    |
| --------------------- | ------------ | ------------------------------ |
| `id`                  | UUID (PK)    | Unique internal customer ID    |
| `email`               | VARCHAR(255) | Customer's email               |
| `phone_number`        | VARCHAR(20)  | Customer's phone number        |
| `first_name`          | VARCHAR(100) | Optional: From Shopify         |
| `last_name`           | VARCHAR(100) | Optional: From Shopify         |
| `shopify_customer_id` | TEXT         | Shopify ID for cross-reference |
| `created_at`          | TIMESTAMP    | Auto-filled                    |

---

### 📦 `orders`

| Field              | Type                     | Description                           |
| ------------------ | ------------------------ | ------------------------------------- |
| `id`               | UUID (PK)                | Unique internal order ID              |
| `shopify_order_id` | TEXT                     | Shopify order ID                      |
| `customer_id`      | UUID (FK → customers.id) | Links order to customer               |
| `order_status`     | VARCHAR(50)              | e.g., "fulfilled", "delivered", etc.  |
| `order_date`       | TIMESTAMP                | Date of order                         |
| `product_type`     | VARCHAR(100)             | e.g., "shade\_kit", "full\_size\_spf" |
| `currency`         | VARCHAR(10)              | "NGN" or "USD"                        |
| `total_amount`     | NUMERIC(10,2)            | Total paid                            |
| `created_at`       | TIMESTAMP                | Auto-filled                           |

---

### 📝 `surveys`

| Field                  | Type                     | Description                           |
| ---------------------- | ------------------------ | ------------------------------------- |
| `id`                   | UUID (PK)                | Unique survey entry                   |
| `customer_id`          | UUID (FK → customers.id) | Who took the survey                   |
| `order_id`             | UUID (FK → orders.id)    | Which sample kit this ties to         |
| `shade_selected`       | VARCHAR(50)              | e.g., "Shade 3"                       |
| `shade_fit_rating`     | INTEGER                  | 1–5 scale (optional)                  |
| `skin_type`            | VARCHAR(50)              | "Oily", "Dry", "Combo", etc.          |
| `skin_concerns`        | TEXT\[]                  | Array: \["Hyperpigmentation", "Acne"] |
| `finish_preference`    | VARCHAR(50)              | "Matte", "Dewy", etc.                 |
| `texture_feedback`     | TEXT                     | Free-text response                    |
| `interested_in_addons` | TEXT\[]                  | \["Retinoid", "Fade Serum"]           |
| `survey_completed_at`  | TIMESTAMP                | Auto-filled                           |

---

### 🎟️ `discounts`

| Field                 | Type                            | Description                    |
| --------------------- | ------------------------------- | ------------------------------ |
| `id`                  | UUID (PK)                       | Unique discount entry          |
| `customer_id`         | UUID (FK → customers.id)        | Who this discount was given to |
| `discount_code`       | VARCHAR(100)                    | Shopify-compatible code        |
| `amount`              | NUMERIC(10,2)                   | e.g., 3000.00 or 5.00          |
| `currency`            | VARCHAR(10)                     | "NGN" or "USD"                 |
| `applied_to_order_id` | UUID (FK → orders.id, nullable) | If used, this shows where      |
| `expires_at`          | TIMESTAMP                       | Expiry time (e.g., 7 days)     |
| `created_at`          | TIMESTAMP                       | Auto-filled                    |
| `used`                | BOOLEAN                         | Default false                  |

---

### 🛒 `recommendations`

| Field                | Type                   | Description                          |
| -------------------- | ---------------------- | ------------------------------------ |
| `id`                 | UUID (PK)              | Rec ID                               |
| `survey_id`          | UUID (FK → surveys.id) | Ties back to user data               |
| `recommended_shade`  | VARCHAR(50)            | e.g., "Shade 4"                      |
| `recommended_bundle` | TEXT\[]                | e.g., \["Shade 4 SPF", "Fade Serum"] |
| `cart_url`           | TEXT                   | Pre-filled checkout cart link        |
| `created_at`         | TIMESTAMP              | Auto-filled                          |

---

### 📉 `conversions`

| Field          | Type                     | Description                         |
| -------------- | ------------------------ | ----------------------------------- |
| `id`           | UUID (PK)                | Conversion ID                       |
| `customer_id`  | UUID (FK → customers.id) | Who converted                       |
| `survey_id`    | UUID (FK → surveys.id)   | From which survey                   |
| `discount_id`  | UUID (FK → discounts.id) | Which discount was used             |
| `cart_url`     | TEXT                     | If link was clicked                 |
| `converted`    | BOOLEAN                  | Did they purchase?                  |
| `converted_at` | TIMESTAMP                | When the purchase was made (if any) |
| `created_at`   | TIMESTAMP                | For timestamping all attempts       |

---

## 🔗 RELATIONSHIPS OVERVIEW

* `customers` ⬅️→ `orders`
* `orders` ⬅️→ `surveys`
* `surveys` ⬅️→ `recommendations`
* `customers` ⬅️→ `discounts`
* `discounts` ⬅️→ `conversions`
* `surveys` ⬅️→ `conversions`

---

## 🧪 BONUS: AI Training Table (Optional, Future-Ready)

### 🧠 `model_training_data`

| Field                   | Type                   | Description                          |
| ----------------------- | ---------------------- | ------------------------------------ |
| `id`                    | UUID (PK)              |                                      |
| `survey_id`             | UUID (FK → surveys.id) |                                      |
| `image_url`             | TEXT                   | If image upload is enabled later     |
| `match_accuracy_rating` | INTEGER                | 1–5 scale (user-rated match quality) |
| `feedback_notes`        | TEXT                   | Manual QA notes                      |
| `used_for_training`     | BOOLEAN                | True/false                           |

---

## ✅ Summary of Key Tables

| Table                 | Purpose                             |
| --------------------- | ----------------------------------- |
| `customers`           | Master user record                  |
| `orders`              | Purchase data (sample + full-size)  |
| `surveys`             | Survey answers from SPF kit flow    |
| `discounts`           | Credit tracking & Shopify sync      |
| `recommendations`     | AI-powered match suggestions        |
| `conversions`         | Full-size product purchase tracking |
| `model_training_data` | (Optional) ML feedback loop logging |

---
