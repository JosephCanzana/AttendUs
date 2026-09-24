# Attendus

## Tech Stack
- Django, PostgreSQL, Docker
- Tailwind CSS (standalone CLI)
- Alpine.js

## Development Setup

### Prerequisites
- Docker with Compose
- `make` for the Tailwind helper commands

### First-time setup
1. Clone the repository and enter the project directory.
2. Copy the example environment file:

```bash
cp .env.example .env
```

Update `.env` before starting the application. The default values are suitable for local Docker development; do not commit the resulting `.env` file.

3. Download the Tailwind CLI (one-time):

```bash
curl -sLO https://github.com/tailwindlabs/tailwindcss/releases/latest/download/tailwindcss-linux-x64
chmod +x tailwindcss-linux-x64
mv tailwindcss-linux-x64 theme/tailwindcss
```

4. Download Alpine.js (one-time):

```bash
mkdir -p static/js
curl -sLo static/js/alpine.min.js https://cdn.jsdelivr.net/npm/alpinejs@3.14.9/dist/cdn.min.js
```

5. Build and start the containers:

```bash
docker compose up --build
```

In a second terminal, apply migrations and optionally create an admin user:

```bash
docker compose exec web python manage.py migrate
docker compose exec web python manage.py createsuperuser
```

The application is available at <http://localhost:8002>. PostgreSQL is available to local tools at `localhost:5432`.

## Day-to-day development

Start the application:

```bash
docker compose up
```

Run Tailwind in a separate terminal while editing templates or CSS:

```bash
make tailwind-watch
```

Useful commands:

```bash
docker compose exec web python manage.py check
docker compose exec web python manage.py test
make tailwind-build
```

Stop the containers with `Ctrl+C`. To remove the containers and the PostgreSQL volume, use `docker compose down -v`; this deletes local database data.

## Project layout

- `attendus/`: Django project configuration and entry points
- `sandbox/`: application code, URLs, templates, and migrations
- `static/`: source CSS and frontend assets
- `theme/tailwindcss`: standalone Tailwind executable
- `docker-compose.yml`: Django and PostgreSQL development services

## Troubleshooting

- If Django cannot connect to PostgreSQL, confirm that `.env` exists and that `POSTGRES_HOST=db` when running inside Compose.
- If CSS changes do not appear, ensure `make tailwind-watch` is running and that `static/css/output.css` has been generated.
- After changing dependencies, rebuild the web image with `docker compose up --build`.