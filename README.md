# php-airbnb-frostfall

A Laravel application running with Laravel Sail (Docker).

---

## Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (or Docker Engine on Linux)
- [Composer](https://getcomposer.org/) — only needed for the first install step

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/your-org/php-airbnb-frostfall.git
cd php-airbnb-frostfall
```

### 2. Install PHP dependencies

```bash
composer install
```

### 3. Copy the environment file

```bash
cp .env.example .env
```

Then open `.env` and fill in your values — at minimum:

```env
DB_CONNECTION=pgsql
DB_HOST=pgsql
DB_PORT=5432
DB_DATABASE=php_airbnb_frostfall_new
DB_USERNAME=sail
DB_PASSWORD=secret
```

### 4. Start the containers

```bash
./vendor/bin/sail up -d
```

> On first run, Docker will pull the required images. This may take a minute.

### 5. Generate the application key

```bash
./vendor/bin/sail artisan key:generate
```

### 6. Run migrations

```bash
./vendor/bin/sail artisan migrate
```

### 7. (Optional) Seed the database

```bash
./vendor/bin/sail artisan db:seed
```

The app is now running at **http://localhost**.

---

## Daily Usage

| Task | Command |
|---|---|
| Start containers | `./vendor/bin/sail up -d` |
| Stop containers | `./vendor/bin/sail down` |
| Run migrations | `./vendor/bin/sail artisan migrate` |
| Run tests | `./vendor/bin/sail artisan test` |
| Open a shell | `./vendor/bin/sail shell` |
| Run Composer | `./vendor/bin/sail composer <cmd>` |
| Run NPM | `./vendor/bin/sail npm <cmd>` |

> **Tip:** Add a shell alias to avoid typing the full path every time:
> ```bash
> alias sail='./vendor/bin/sail'
> ```

---

## Frontend (Vite)

To compile assets and start the Vite dev server:

```bash
./vendor/bin/sail npm install
./vendor/bin/sail npm run dev
```

---

## Troubleshooting

### Containers not starting

Check logs for a specific service:

```bash
./vendor/bin/sail logs pgsql
./vendor/bin/sail logs laravel.test
```

### Database connection errors

If you see password authentication failures or the `pgsql` host can't be resolved, the most common fix is a **full reset of the Docker volumes**:

```bash
./vendor/bin/sail down --volumes
./vendor/bin/sail up -d
./vendor/bin/sail artisan migrate
```

> ⚠️ This wipes all local database data. Only use in development.

### Port conflict on 5432 or 80

If another service is using those ports, update your `.env`:

```env
APP_PORT=8080
FORWARD_DB_PORT=5433
```

Then restart: `./vendor/bin/sail down && ./vendor/bin/sail up -d`

---

## Tech Stack

- **Framework:** Laravel 13
- **Runtime:** PHP 8.5 (via Laravel Sail)
- **Database:** PostgreSQL 18
- **Frontend:** Vite
- **Local environment:** Docker / Laravel Sail
