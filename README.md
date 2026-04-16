# Laravel + Inertia.js Technical Challenge

## Overview

Simple full-stack app built with:

- Laravel
- Inertia.js + Vue 3
- Tailwind CSS
- SQLite

Features:

- Authentication (Laravel Breeze)
- User profile update
- Create, edit, delete posts
- View all posts
- Authorization (users can modify only their own posts)

---

## Installation

```bash
git clone <repo-url>
cd <project-folder>
composer install
npm install
cp .env.example .env
php artisan key:generate
```

Create database:

```
touch database/database.sqlite
php artisan migrate
```

Run

```
php artisan serve
npm run dev
```

App: http://127.0.0.1:8000

## Time Spent

~4–5 hours

## Notes / Trade-offs

- Focus on functionality over polish
- Basic UI (Tailwind, no advanced components)
- Limited error handling
- Minimal abstraction (kept simple due to time constraint)

## Improvements (with more time)

- Extract logic into Services / Resources consistently
- Improve UI consistency and reusable components
- Add better error handling and notifications
- Introduce automated tests
