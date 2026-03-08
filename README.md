# Blog — Laravel Web Application

A full-featured blog application built with **Laravel** as a progressively developed learning project — starting from basic CRUD and evolving into a production-ready app with authentication, a REST API, tags, Blade components, and JWT.

---

## What I Learned

### 🔧 Laravel Core
- Setting up a Laravel project from scratch using **Artisan**
- **MVC architecture** — separating concerns across Models, Views, and Controllers
- **Eloquent ORM** — defining models, relationships, and querying the database without raw SQL
- **Migrations** — versioning the database schema and managing changes over time
- **Seeders & Factories** — generating fake data for testing

### 🛣️ Routing & Controllers
- Defining **RESTful resource routes** with `Route::resource()`
- Using **route middleware** to protect routes (`auth`, custom `onlyMe`)
- **Single Action Controllers** — clean, focused controllers for simple pages
- **Route grouping** to apply middleware to multiple routes at once

### 🔐 Authentication
- Building a full **Login / Signup** system from scratch with `AuthController`
- Hashing passwords, sessions, and managing authenticated state
- **Custom middleware** (`onlyMe`) to restrict specific pages to the owner only
- Implementing **JWT authentication** for the REST API using `tymon/jwt-auth`

### 🗃️ Database & Relationships
- **One-to-Many**: User → Posts, Post → Comments
- **Many-to-Many**: Posts ↔ Tags (with a pivot table `post_tag`)
- **UUIDs** on models using `HasUuids` trait
- Writing and running **migrations** for all relationships including foreign keys and unique constraints

### 🧩 Blade & Frontend
- **Blade templating** — layouts, `@yield`, `@section`, `@include`
- **Blade Components** — reusable UI pieces (`<x-layout>`, `<x-comment>`, `<x-delete-modal>`, `<x-nav-link>`)
- Clean **form handling** with CSRF protection, validation, and old input

### 🌐 REST API
- Building a separate **API layer** under `routes/api.php`
- **JWT-protected API endpoints** for login, logout, token refresh, and `me`
- `apiResource` for a full CRUD posts API
- Separating API controllers under `app/Http/Controllers/api/`

### 🏷️ Tags System
- Full CRUD for tags with a dedicated `TagController`
- Attaching/detaching tags to posts via **many-to-many** relationship
- Displaying posts filtered by tag

---

## Features

- 📝 Create, read, update, delete **blog posts**
- 💬 **Comments** on posts (authenticated users)
- 🏷️ **Tags** — organize posts by topic
- 🔐 **Auth** — signup, login, logout
- 🌐 **REST API** with JWT authentication
- 🧩 Reusable **Blade components**
- 📄 About, Contact, Jobs static pages
- 🔒 Owner-only route protection

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Laravel 11 |
| Database | SQLite / MySQL |
| Auth (Web) | Laravel Sessions |
| Auth (API) | JWT (`tymon/jwt-auth`) |
| Frontend | Blade + Tailwind CSS |
| Build | Vite |

---

## Getting Started

```bash
# Install dependencies
composer install
npm install

# Setup environment
cp .env.example .env
php artisan key:generate

# Run migrations
php artisan migrate

# Start dev server
php artisan serve
npm run dev
```

---

## Project Structure

```
app/
├── Http/
│   ├── Controllers/
│   │   ├── api/              # JWT API controllers
│   │   ├── AuthController    # Login / Signup / Logout
│   │   ├── PostController    # Blog post CRUD
│   │   ├── CommentController # Comments
│   │   ├── TagController     # Tags CRUD
│   │   └── ...               # Single action controllers
│   └── Middleware/
│       └── onlyMe.php        # Owner-only access
├── Models/
│   ├── User.php              # Implements JWTSubject
│   ├── Post.php              # belongs to User, has many Comments, belongs to many Tags
│   ├── Comment.php
│   └── Tag.php               # HasUuids, belongs to many Posts
routes/
├── web.php                   # Web routes (auth + guest)
└── api.php                   # JWT-protected API routes
resources/views/
├── components/               # Reusable Blade components
├── posts/                    # Post CRUD views
├── comments/                 # Comment views
├── tags/                     # Tag views
└── auth/                     # Login & Signup pages
```
