# 🗄️ Esquema de Base de Datos – Etapa 08

Este documento describe el diseño de la base de datos del sistema de compras, incluyendo tablas, claves primarias, claves foráneas y relaciones principales.

---

## 📌 Tabla: users

| Campo            | Tipo            | Notas                      |
|------------------|-----------------|----------------------------|
| user_id (PK)     | BIGINT          | Identificador único        |
| role_id (FK)     | BIGINT          | Rol del usuario            |
| email            | VARCHAR(255)    | Único                      |
| password_hash    | VARCHAR(255)    |                            |
| first_name       | VARCHAR(255)    |                            |
| last_name        | VARCHAR(255)    |                            |
| phone            | VARCHAR(50)     |                            |
| status           | ENUM            | ACTIVE, INACTIVE, BLOCKED  |
| created_at       | TIMESTAMP       |                            |

---

## 📌 Tabla: roles

| Campo         | Tipo           | Notas |
|---------------|----------------|-------|
| role_id (PK)  | BIGINT         |       |
| name          | VARCHAR(255)   | Único |
| description   | TEXT           |       |

---

## 📌 Tabla: addresses

| Campo             | Tipo           | Notas                               |
|-------------------|----------------|-------------------------------------|
| address_id (PK)   | BIGINT         |                                     |
| user_id (FK)      | BIGINT         |                                     |
| type              | ENUM           | SHIPPING / BILLING                  |
| line1             | VARCHAR(255)   |                                     |
| line2             | VARCHAR(255)   | NULLABLE                            |
| city              | VARCHAR(100)   |                                     |
| state             | VARCHAR(100)   |                                     |
| country           | VARCHAR(100)   |                                     |
| postal_code       | VARCHAR(20)    |                                     |
| is_default        | BOOLEAN        |                                     |

---

## 📌 Tabla: categories

| Campo           | Tipo           | Notas                          |
|-----------------|----------------|--------------------------------|
| category_id (PK) | BIGINT        |                                |
| parent_id (FK)   | BIGINT        | Auto-relación                  |
| name            | VARCHAR(255)   |                                |
| slug            | VARCHAR(255)   | Único                          |

---

## 📌 Tabla: products

| Campo           | Tipo           | Notas                      |
|-----------------|----------------|----------------------------|
| product_id (PK) | BIGINT         |                            |
| category_id (FK)| BIGINT         |                            |
| sku             | VARCHAR(100)   | Único                      |
| name            | VARCHAR(255)   |                            |
| description     | TEXT           |                            |
| price           | DECIMAL(10,2)  |                            |
| stock_qty       | INT            |                            |
| is_active       | BOOLEAN        |                            |
| created_at      | TIMESTAMP      |                            |

---

## 📌 Tabla: carts

| Campo         | Tipo           | Notas                |
|---------------|----------------|----------------------|
| cart_id (PK)  | BIGINT         |                      |
| user_id (FK)  | BIGINT NULL    | Invitado si es NULL  |
| session_id (FK) | BIGINT       |                      |
| status        | ENUM           | OPEN, ABANDONED...   |
| created_at    | TIMESTAMP      |                      |
| updated_at    | TIMESTAMP      |                      |

---

## 📌 Tabla: cart_items

| Campo           | Tipo           | Notas                        |
|-----------------|----------------|------------------------------|
| cart_item_id(PK)| BIGINT         |                              |
| cart_id (FK)    | BIGINT         |                              |
| product_id (FK) | BIGINT         |                              |
| quantity        | INT            | > 0                          |
| unit_price      | DECIMAL(10,2)  | Precio congelado             |
| added_at        | TIMESTAMP      |                              |

---

## 📌 Tabla: orders

| Campo               | Tipo           | Notas                   |
|---------------------|----------------|-------------------------|
| order_id (PK)       | BIGINT         |                         |
| order_number        | VARCHAR(255)   | Único                   |
| user_id (FK)        | BIGINT         |                         |
| order_status_id(FK) | BIGINT         |                         |
| shipping_address_id | BIGINT         |                         |
| billing_address_id  | BIGINT         |                         |
| subtotal            | DECIMAL(10,2)  |                         |
| tax                 | DECIMAL(10,2)  |                         |
| shipping_cost       | DECIMAL(10,2)  |                         |
| total               | DECIMAL(10,2)  |                         |
| created_at          | TIMESTAMP      |                         |

---

## 📌 Tabla: order_items

| Campo             | Tipo           | Notas                     |
|-------------------|----------------|---------------------------|
| order_item_id (PK)| BIGINT         |                           |
| order_id (FK)     | BIGINT         |                           |
| product_id (FK)   | BIGINT         |                           |
| quantity          | INT            |                           |
| unit_price        | DECIMAL(10,2)  | Precio histórico          |
| line_total        | DECIMAL(10,2)  |                           |

---

## 📌 Tabla: payments

| Campo             | Tipo           | Notas                         |
|-------------------|----------------|-------------------------------|
| payment_id (PK)   | BIGINT         |                               |
| order_id (FK)     | BIGINT         |                               |
| payment_method_id | BIGINT (FK)    |                               |
| payment_status_id | BIGINT (FK)    |                               |
| amount            | DECIMAL(10,2)  | Puede ser negativo (refunds)  |
| currency          | ENUM           | USD/COP/EUR                   |
| provider_reference| VARCHAR(255)   |                               |
| paid_at           | TIMESTAMP NULL |                               |