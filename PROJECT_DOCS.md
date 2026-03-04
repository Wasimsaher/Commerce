# E-Commerce - Project Documentation

## Table of Contents
1. [Phase 1 - Planning](#phase-1---planning)
2. [Phase 2 - Analysis](#phase-2---analysis)
3. [Phase 3 - Design](#phase-3---design)
4. [Phase 4 - Development](#phase-4---development) ← Coming Soon
5. [Phase 5 - Testing](#phase-5---testing) ← Coming Soon
6. [Phase 6 - Deployment](#phase-6---deployment) ← Coming Soon

---

## Phase 1 - Planning

### What are we building?
A web application that allows users to browse products,
add them to a cart, and purchase them securely using Stripe.

### Why are we building it?
To provide a simple and secure online shopping experience.

### Who is it for?
Online shoppers who want to browse and purchase products easily.

### Tech Stack
| Layer      | Technology        |
|------------|-------------------|
| Backend    | PHP / Laravel 12  |
| Frontend   | React             |
| Database   | MySQL             |
| Payment    | Stripe            |

---

## Phase 2 - Analysis

### Authentication Flow

Users can authenticate with email and password for both login and registration:

```
+--------+                    +-----------+
| Login  |                    | Register  |
+---+----+                    +-----+-----+
    |                               |
+---+-------------+         +------+----------------------+
| Email           |         | Name                        |
| Password        |         | Phone                       |
+-----------------+         | Email                       |
                            | Password                    |
                            +-----------------------------+
                                       |
                          On Error   --> Show error message
                          On Success --> Show main page of all products
```

### User Features

Once authenticated, users have access to products, cart, orders and invoices:

```
            +------+
            | User |
            +--+---+
               |
        +------+------+
        |             |
   +----+----+   +----+----+
   |Products |   |   Cart  |
   |  (Read) |   | (CRUD)  |
   +----+----+   +----+----+
                      |
                 +----+----+
                 |  Order  |
                 |  Create |
                 +----+----+
                      |
                 +----+-----+
                 | Invoice  |
                 |  (View)  |
                 +----------+
```

### User Operations Summary

| Feature  | Operations                              |
|----------|-----------------------------------------|
| Products | Read (browse, view single product)      |
| Cart     | CRUD (add, view, update, remove items)  |
| Order    | Create, View history                    |
| Invoice  | View (after successful payment)         |

### Total Entities

| Entity   | Description                             |
|----------|-----------------------------------------|
| User     | Customer of the store                   |
| Product  | Item being sold                         |
| Cart     | User's shopping basket                  |
| Order    | Completed purchase                      |
| Invoice  | Receipt generated after order is placed |

---

## Phase 3 - Design

### Part 1 — Database Design

#### Entity Relationship (How tables connect)
```
users ----------< orders
users ----------< cart_items
products -------< cart_items
orders ---------< order_items
products -------< order_items
orders ---------< invoices
```
`<` means "one to many" — one user has many orders, etc.

---

#### Tables Design

```
users
├── id
├── name
├── email
├── phone
├── password
└── timestamps

products
├── id
├── name
├── description
├── price
├── stock
├── image
└── timestamps

cart_items
├── id
├── user_id      → users.id
├── product_id   → products.id
├── quantity
└── timestamps

orders
├── id
├── user_id      → users.id
├── total
├── status       → pending, paid, cancelled
├── stripe_payment_id
└── timestamps

order_items
├── id
├── order_id     → orders.id
├── product_id   → products.id
├── quantity
├── price
└── timestamps

invoices
├── id
├── order_id     → orders.id
├── amount
└── timestamps
```

---

### Part 2 — API Design

#### Auth Endpoints
```
POST   /api/register    → Create new account
POST   /api/login       → Login
POST   /api/logout      → Logout
```

#### Products Endpoints
```
GET    /api/products        → List all products
GET    /api/products/{id}   → View single product
```

#### Cart Endpoints
```
GET    /api/cart            → View cart
POST   /api/cart            → Add item
PUT    /api/cart/{id}       → Update quantity
DELETE /api/cart/{id}       → Remove item
```

#### Orders Endpoints
```
GET    /api/orders          → View order history
POST   /api/orders          → Place order
GET    /api/orders/{id}     → View single order
```

#### Invoice Endpoints
```
GET    /api/invoices/{id}   → View invoice
```

---
