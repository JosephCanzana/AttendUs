# Agent Instructions

## Project Overview

AttendUs is a Django application backed by PostgreSQL. The frontend uses Django templates, Tailwind CSS built with the standalone CLI, and Alpine.js.

## Repository Rules

- Keep changes focused on the requested behavior.
- Preserve the existing Django app structure unless a change requires a new app or module.
- Use environment variables from `.env` for secrets and database settings. Never commit `.env` or hard-code credentials.
- Keep generated assets, such as Tailwind output, out of source changes unless the task specifically requires them.
- Prefer the existing Docker Compose and Makefile workflows over adding new local tooling.
- Do not modify the database or delete user data without explicit approval.

## Development Workflow

1. Copy `.env.example` to `.env` when setting up a fresh checkout.
2. Start the services with `docker compose up --build`.
3. Apply migrations with `docker compose exec web python manage.py migrate`.
4. Run Tailwind in a separate terminal with `make tailwind-watch` when changing templates or CSS.

The web container is available at `http://localhost:8002` and the PostgreSQL service is exposed on port `5432`.

## Validation

- Run Django checks with `docker compose exec web python manage.py check`.
- Run tests with `docker compose exec web python manage.py test`.
- Build production CSS with `make tailwind-build` when validating CSS changes.
- Inspect the diff and avoid unrelated formatting or dependency changes.
