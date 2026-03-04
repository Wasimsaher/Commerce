# E-Commerce - Project Documentation

## Table of Contents
1. [Phase 1 - Planning](#phase-1---planning)
2. [Phase 2 - Analysis](#phase-2---analysis)
3. [Phase 3 - Design](#phase-3---design) ← Coming Soon
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
