ENTITY RELATIONSHIP SCHEMA
---------------

# Entities Definition

## **User Entity**

| Attribute       | Type                      | Constraints                |
| --------------- | ------------------------- | -------------------------- |
| `id`            | int                       | **\[pk]**                  |
| `first_name`    | varchar                   | **\[NOT NULL]**            |
| `last_name`     | varchar                   | **\[NOT NULL]**            |
| `email`         | varchar                   | **\[UNIQUE, NOT NULL]**    |
| `password_hash` | varchar                   | **\[NOT NULL]**            |
| `phone_number`  | varchar                   | *\[NULL]*                  |
| `role`          | ENUM (guest, host, admin) | **\[NOT NULL]**            |
| `created_at`    | Timestamp                 | \[def: CURRENT\_TIMESTAMP] |

---

## **Property Entity**

| Attribute       | Type      | Constraints                      |
| --------------- | --------- | -------------------------------- |
| `id`            | int       | **\[pk, UUID]**                  |
| `host_id`       | int       | **\[fk, relationship: user.id]** |
| `name`          | varchar   | **\[NOT NULL]**                  |
| `description`   | text      | **\[NOT NULL]**                  |
| `location`      | varchar   | **\[NOT NULL]**                  |
| `pricepernight` | decimal   | **\[NOT NULL]**                  |
| `updated_at`    | Timestamp | \[def: CURRENT\_TIMESTAMP]       |
| `created_at`    | Timestamp | \[def: CURRENT\_TIMESTAMP]       |

---

## **Booking Entity**

| Attribute              | Type                                | Constraints                           |
| ---------------------- | ----------------------------------- | ------------------------------------- |
| `id`                   | int                                 | **\[pk, UUID]**                       |
| `property_id`          | int                                 | **\[fk, ref: property.id, NOT NULL]** |
| `user_id`              | int                                 | **\[fk, ref: user.id, NOT NULL]**     |
| `start_date`           | date                                | **\[NOT NULL]**                       |
| `end_date`             | date                                | **\[NOT NULL]**                       |
| `locked_pricepernight` | decimal                             | **\[NOT NULL]**                       |
| `status`               | ENUM (pending, confirmed, canceled) | **\[NOT NULL]**                       |
| `created_at`           | Timestamp                           | \[def: CURRENT\_TIMESTAMP]            |

---

## **Payment Entity**

| Attribute        | Type                                | Constraints                          |
| ---------------- | ----------------------------------- | ------------------------------------ |
| `id`             | int                                 | **\[pk, UUID]**                      |
| `booking_id`     | int                                 | **\[fk, ref: booking.id, NOT NULL]** |
| `amount`         | decimal                             | **\[NOT NULL]**                      |
| `payment_date`   | date                                | **\[NOT NULL]**                      |
| `payment_method` | ENUM (credit\_card, paypal, stripe) | **\[NOT NULL]**                      |

---

## **Review Entity**

| Attribute     | Type      | Constraints                                        |
| ------------- | --------- | -------------------------------------------------- |
| `id`          | int       | **\[pk, UUID]**                                    |
| `property_id` | int       | **\[fk, ref: property.id, NOT NULL]**              |
| `user_id`     | int       | **\[fk, ref: user.id, NOT NULL]**                  |
| `rating`      | int       | **\[CHECK: rating >= 1 && rating <= 5, NOT NULL]** |
| `comment`     | text      | **\[NOT NULL]**                                    |
| `created_at`  | Timestamp | \[def: CURRENT\_TIMESTAMP]                         |

---

## **Message Entity**

| Attribute      | Type | Constraints                       |
| -------------- | ---- | --------------------------------- |
| `id`           | int  | **\[pk, UUID]**                   |
| `sender_id`    | int  | **\[fk, ref: user.id, NOT NULL]** |
| `recipient_id` | int  | **\[fk, ref: user.id, NOT NULL]** |
| `message_body` | text | **\[NOT NULL]**                   |
| `sent_at`      | Date | \[def: CURRENT\_TIMESTAMP]        |

---

# Entity Constraints

### **User Entity**

* **UNIQUE Fields**: `email`
* **Required Fields**: All fields except `phone_number`

### **Property Entity**

* **Foreign Key**: `host_id → user.id`
* **Required Fields**: All except `updated_at`, `created_at` (defaulted)

### **Booking Entity**

* **Foreign Keys**: `property_id`, `user_id`
* **Required Fields**: All
* **Status Values**: `pending`, `confirmed`, `canceled`

### **Payment Entity**

* **Foreign Key**: `booking_id`
* **Required Fields**: All

### **Review Entity**

* **Foreign Keys**: `property_id`, `user_id`
* **Required Fields**: All

### **Message Entity**

* **Foreign Keys**: `sender_id`, `recipient_id`
* **Required Fields**: All

---

# Indexes

* **Primary Keys (PK)**: `id` for all entities
* **Indexed Fields**: `email`, `property_id`, `booking_id`

---
# Entity-Relationship-Diagram


![ERD](https://github.com/user-attachments/assets/ebffa142-3ac7-4afc-849f-d06781d6bf73)
