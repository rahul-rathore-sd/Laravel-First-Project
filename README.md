# Laravel Learning Roadmap

A hands-on Laravel 12 starter for newcomers. Clone it, run it, then build features in order — each stage teaches one core idea so you grow from “hello world” to a real app.

> **Who this is for:** beginners who know a little PHP (or are learning it alongside Laravel) and want a clear path instead of random tutorials.

---

## What you’ll learn

By the end of this roadmap you’ll be comfortable with:

- Routes, controllers, and Blade views  
- Eloquent models, migrations, and seeders  
- Forms, validation, and CSRF  
- Authentication and authorization  
- File uploads and storage  
- Queues, mail, and basic APIs  
- Testing and deployment basics  

---

## Prerequisites

Install these before you start:

| Tool | Version | Why |
|------|---------|-----|
| [PHP](https://www.php.net/) | 8.2+ | Laravel runs on PHP |
| [Composer](https://getcomposer.org/) | Latest | PHP dependency manager |
| [Node.js](https://nodejs.org/) | 18+ | Vite + Tailwind assets |
| [Git](https://git-scm.com/) | Latest | Version control |

Optional but useful: a DB client (TablePlus, DBeaver) and [Laravel Herd](https://herd.laravel.com/) (Windows/macOS) for a zero-config PHP environment.

---

## Quick start

```bash
# 1. Clone (or open this folder)
cd firstproject

# 2. Install PHP dependencies
composer install

# 3. Environment + app key
copy .env.example .env          # Windows
# cp .env.example .env          # macOS / Linux
php artisan key:generate

# 4. Database (SQLite is already set up for beginners)
# If database/database.sqlite is missing:
#   type nul > database\database.sqlite   # Windows
#   touch database/database.sqlite        # macOS / Linux
php artisan migrate

# 5. Frontend assets
npm install
npm run build

# 6. Run the app
php artisan serve
```

Open [http://127.0.0.1:8000](http://127.0.0.1:8000) — you should see the Laravel welcome page.

**Dev mode (server + Vite + queues + logs together):**

```bash
composer run dev
```

---

## Project map (know the folders)

```
firstproject/
├── app/                    # Your application code
│   ├── Http/Controllers/   # Handle requests, return responses
│   ├── Models/             # Eloquent models (talk to the DB)
│   └── Providers/          # App bootstrapping / service binding
├── bootstrap/              # Framework startup
├── config/                 # App, DB, mail, cache, … settings
├── database/
│   ├── migrations/         # Versioned database schema
│   ├── seeders/            # Sample / demo data
│   └── factories/          # Fake data for tests & seeders
├── public/                 # Web root (index.php lives here)
├── resources/
│   ├── views/              # Blade templates
│   ├── css/ & js/          # Frontend (Vite)
├── routes/
│   ├── web.php             # Browser routes
│   └── console.php         # Artisan console routes
├── storage/                # Logs, cache, uploads
├── tests/                  # Feature & unit tests
├── .env                    # Local secrets (never commit)
└── artisan                 # CLI entry point
```

**Rule of thumb:** change `app/`, `resources/views/`, `routes/`, and `database/` most of the time. Treat `vendor/` as read-only.

---

## Learning roadmap

Work through these stages in order. After each stage, commit your work so you can look back later.

### Stage 0 — Orientation (day 1)

- [ ] Run `php artisan serve` and open the welcome page  
- [ ] Read `routes/web.php` and change the `/` route message  
- [ ] Create a Blade view in `resources/views/` and return it from a route  
- [ ] Run `php artisan list` and try `route:list`, `tinker`, `migrate:status`  

**Goal:** you know how a request becomes a response.

---

### Stage 1 — Routing & controllers

- [ ] Add named routes and route parameters (`/posts/{id}`)  
- [ ] Create a controller: `php artisan make:controller PostController`  
- [ ] Move logic out of `web.php` into controller methods  
- [ ] Use resource routing: `Route::resource('posts', PostController::class)`  

**Docs:** [Routing](https://laravel.com/docs/routing) · [Controllers](https://laravel.com/docs/controllers)

---

### Stage 2 — Blade & layouts

- [ ] Create a layout (`layouts/app.blade.php`) with `@yield` / `@section`  
- [ ] Build a simple list + detail page  
- [ ] Use Blade directives: `@if`, `@foreach`, `@csrf`, `@error`  
- [ ] Pass data from controllers with `compact()` or arrays  

**Docs:** [Blade](https://laravel.com/docs/blade)

---

### Stage 3 — Database & Eloquent

- [ ] Create a model + migration: `php artisan make:model Post -m`  
- [ ] Define columns, run `php artisan migrate`  
- [ ] CRUD with Eloquent (`all`, `find`, `create`, `update`, `delete`)  
- [ ] Add a factory + seeder and run `php artisan db:seed`  
- [ ] Practice relationships: `hasMany` / `belongsTo` (e.g. User → Posts)  

**Mini project idea:** a “Posts” table with title, body, and timestamps.

**Docs:** [Eloquent](https://laravel.com/docs/eloquent) · [Migrations](https://laravel.com/docs/migrations)

---

### Stage 4 — Forms & validation

- [ ] Build create / edit forms with Blade  
- [ ] Protect forms with `@csrf`  
- [ ] Validate in the controller (`$request->validate([...])`)  
- [ ] Show field errors next to inputs  
- [ ] Extract a Form Request: `php artisan make:request StorePostRequest`  

**Docs:** [Validation](https://laravel.com/docs/validation) · [Requests](https://laravel.com/docs/requests)

---

### Stage 5 — Authentication

- [ ] Install [Laravel Breeze](https://laravel.com/docs/starter-kits) (Blade stack) for login/register  
- [ ] Protect routes with `auth` middleware  
- [ ] Use `auth()->user()` and `@auth` / `@guest` in Blade  
- [ ] Restrict editing so users only change their own posts  

**Docs:** [Authentication](https://laravel.com/docs/authentication) · [Authorization](https://laravel.com/docs/authorization)

---

### Stage 6 — Go deeper (pick what you need)

| Topic | Try this | Docs |
|-------|----------|------|
| File uploads | Avatar or post image → `Storage` | [Filesystem](https://laravel.com/docs/filesystem) |
| Mail | Welcome email on register | [Mail](https://laravel.com/docs/mail) |
| Queues | Send mail in the background | [Queues](https://laravel.com/docs/queues) |
| API | `routes/api.php` + JSON resources | [API Resources](https://laravel.com/docs/eloquent-resources) |
| Policies | `PostPolicy` for update/delete | [Authorization](https://laravel.com/docs/authorization) |
| Testing | Feature test for “create post” | [Testing](https://laravel.com/docs/testing) |

---

### Stage 7 — Capstone ideas

Pick one and build it end-to-end:

1. **Personal blog** — posts, tags, comments, markdown  
2. **Task manager** — projects, tasks, due dates, status  
3. **Bookmark saver** — links, categories, search  
4. **Simple shop** — products, cart (session), checkout stub  

Ship checklist: migrations, seeders, auth, validation, tests for happy paths, README for *your* app.

---

## Everyday Artisan commands

```bash
php artisan serve                 # Local server
php artisan route:list            # See all routes
php artisan make:model Post -mcr  # Model + migration + controller + resource
php artisan make:migration ...    # New migration only
php artisan migrate               # Run pending migrations
php artisan migrate:fresh --seed  # Reset DB + seed (destroys data!)
php artisan tinker                # Interactive REPL
php artisan test                  # Run PHPUnit tests
php artisan pint                  # Code style (Laravel Pint)
```

---

## Suggested study rhythm

| Week | Focus |
|------|--------|
| 1 | Stages 0–2 (routes, controllers, Blade) |
| 2 | Stage 3 (database + Eloquent) |
| 3 | Stage 4–5 (forms + auth) |
| 4 | Stage 6–7 (one advanced topic + capstone start) |

Spend more time building than watching videos. When stuck: read the error, check `storage/logs/laravel.log`, then search the [Laravel docs](https://laravel.com/docs).

---

## Official & community resources

- [Laravel Documentation](https://laravel.com/docs) — start here always  
- [Laracasts](https://laracasts.com/) — excellent video series for beginners  
- [Laravel Bootcamp](https://bootcamp.laravel.com/) — guided mini-app  
- [Laravel News](https://laravel-news.com/) — ecosystem updates  
- [PHP The Right Way](https://phptherightway.com/) — solid PHP foundations  

---

## Contributing / how to use this repo

1. Treat each roadmap stage as a branch or a clear commit message (`feat: stage 3 posts CRUD`).  
2. Keep experiments in feature branches so `main` stays runnable.  
3. If you teach with this repo, fork it and add your own notes under a `notes/` folder.

---

## Tech stack

- **Laravel** 12  
- **PHP** 8.2+  
- **Vite** + **Tailwind CSS** 4  
- **SQLite** by default (easy local setup; switch to MySQL/PostgreSQL in `.env` when ready)  

---

## License

MIT — learn freely, build freely.

Happy coding. You’ve got this.
