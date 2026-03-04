# Simple E-Commerce

A web application that allows users to browse products, add them to a cart, and purchase them securely using Stripe.

---

## Tech Stack

| Layer    | Technology       |
|----------|------------------|
| Backend  | PHP / Laravel 12 |
| Frontend | React            |
| Database | MySQL            |
| Payment  | Stripe           |

---

## Prerequisites

Make sure you have the following installed:

| Tool       | Version | Check             |
|------------|---------|-------------------|
| PHP        | 8.2+    | `php -v`          |
| Composer   | 2.x     | `composer -V`     |
| Node.js    | 20+     | `node -v`         |
| npm        | 10+     | `npm -v`          |
| MySQL      | 8.0+    | `mysql --version` |

---

## Installation

### 1. Clone the project
```bash
git clone https://github.com/your-username/commerce.git
cd commerce
```

### 2. Install dependencies
```bash
composer install
npm install
```

### 3. Setup environment
```bash
cp .env.example .env
php artisan key:generate
```

### 4. Configure your `.env` file
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=ecommerce
DB_USERNAME=root
DB_PASSWORD=

STRIPE_KEY=your_stripe_public_key
STRIPE_SECRET=your_stripe_secret_key
```

### 5. Setup database
```bash
mysql -u root -e "CREATE DATABASE IF NOT EXISTS ecommerce;"
php artisan migrate
php artisan db:seed
```

### 6. Run the project
```bash
# Terminal 1 - Backend
php artisan serve

# Terminal 2 - Frontend
npm run dev
```

Open `http://localhost:8000` in your browser.

---

## Project Structure

```
commerce/
├── backend/                → Laravel API (backend)
│   ├── app/
│   │   ├── Http/Controllers/ → Handle API requests
│   │   ├── Models/           → Database models
│   │   └── Services/         → Business logic
│   ├── database/
│   │   ├── migrations/       → Database tables
│   │   └── seeders/          → Fake data
│   ├── routes/
│   │   └── api.php           → API routes
│   └── .env                  → Environment config
│
└── frontend/       → React app (frontend)
    ├── src/
    │   ├── components/       → Reusable UI components
    │   ├── pages/            → App pages
    │   └── services/         → API calls
    └── .env                  → Frontend environment config
```

---

## Documentation

For full project specifications, requirements, and design decisions see [PROJECT_DOCS.md](./PROJECT_DOCS.md).
