# Attendus

## Tech Stack
- Django, PostgreSQL, Docker
- Tailwind CSS (standalone CLI)
- Alpine.js

## Setup

### Prerequisites
- Docker & Docker Compose
- `make`

### First-time setup
1. Clone the repo
2. Copy `.env.example` to `.env` and fill in values
3. Download Tailwind CLI (one-time):
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
5. Build containers:
```bash
   docker compose up --build
   docker compose exec web python manage.py migrate
   docker compose exec web python manage.py createsuperuser
```

### Day-to-day development
```bash
docker compose up
make tailwind-watch    # in a separate terminal
```