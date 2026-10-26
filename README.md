# ShopMate AI: Smarter shopping. Less searching.

**Status: Phase 1 of 7 complete** (backend catalog API). Frontend, auth, cart, AI agent,
checkout, admin and deployment come in later phases.

## Architecture
React + TS + Vite + Tailwind (`frontend/`) -> REST -> FastAPI (`backend/app/api`) ->
services (`services/`, business rules) -> SQLAlchemy models (`models/`) -> SQLite (dev) / PostgreSQL (prod).
The OpenAI agent (`agent/`, Phase 4) will call the same `services/` functions as typed tools,
so it cannot bypass business rules.

## Run locally (backend)
Needs Python 3.10+. Open a terminal in the `backend` folder.

**Windows (PowerShell)**

    python -m venv .venv
    .venv\Scripts\Activate.ps1
    pip install -r requirements.txt
    python run.py

**macOS / Linux**

    python3 -m venv .venv && source .venv/bin/activate
    pip install -r requirements.txt
    python run.py

The database is created and seeded automatically on first start.
Open http://127.0.0.1:8000/docs for the interactive API. Tests: `python -m pytest`.

Troubleshooting: if `pip install` fails, run `python --version` and upgrade pip
(`python -m pip install -U pip`). If port 8000 is busy, change it in `run.py`.
`.env` is optional in Phase 1.

## Data note
All products, prices, ratings, reviews and stock are **demo data**. Product photos are placeholders (`/images/<sku>.jpg`).

## Production note
Do not use SQLite on Render's ephemeral disk; set `DATABASE_URL` to a managed PostgreSQL instance.
