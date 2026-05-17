# LABMMONE

Full-stack laboratory management system composed of a Flask REST API backend (**LABMM**) and an Angular frontend (**LABMMIF**), orchestrated with Docker Compose.

## Architecture

| Component | Technology | Description |
|-----------|-----------|-------------|
| `LABMM` | Flask 3 + SQLite | REST API with JWT authentication |
| `LABMMIF` | Angular 21 | Single-page application |

---

## Quick Start with Docker

### Prerequisites

- Docker Engine 24+
- Docker Compose v2

### 1. Configure environment variables

Create a `.env` file in the project root:

```env
SECRET_KEY=your-secret-key
JWT_SECRET_KEY=your-jwt-secret-key
DATABASE_URL=sqlite:///labmm.db

# Optional: defaults shown below
ADMIN_EMAIL=admin@labmm.local
ADMIN_PASSWORD=changeme
ADMIN_FIRST_NAME=Admin
ADMIN_LAST_NAME=User
```

### 2. Development

```bash
git submodule update --init --recursive
docker compose up --build
```

- Frontend: http://localhost:4200
- Backend API: http://localhost:5000

Source files are bind-mounted so changes hot-reload without rebuilding.

### 3. Production

```bash
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d --build
```

- App served on http://localhost (port 80 via Nginx)

---

## Running Without Docker

See the individual guides for local development:

- [LABMM/HOW_TO_RUN.md](https://github.com/warrior-graph/LABMM/blob/master/HOW_TO_RUN.md) — Backend (Python 3.10+)
- [LABMMIF/HOW_TO_RUN.md](https://github.com/warrior-graph/LABMMIF/blob/master/HOW_TO_RUN.md) — Frontend (Node.js 24 LTS, Angular CLI 21+)

---

## Backend Overview

- **Auth:** JWT-based (`/auth/login`, `/auth/register`)
- **Resources:** laboratories, members, projects, research, articles, roles
- **Database:** SQLite (persisted in a named Docker volume)
- **Migrations:** Flask-Migrate / Alembic

### Running Tests

```bash
cd LABMM
pip install -r requirements.txt
pytest
```

---

## Project Structure

```
LABMMONE/
├── docker-compose.yml           # Base services
├── docker-compose.override.yml  # Development overrides (auto-loaded)
├── docker-compose.prod.yml      # Production overrides
├── LABMM/                       # Flask backend
│   ├── labmm/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── schemas/
│   │   └── utils/
│   ├── migrations/
│   ├── tests/
│   └── requirements.txt
└── LABMMIF/                     # Angular frontend
    └── src/
        └── app/
            ├── core/
            ├── features/
            └── shared/
```

---

## License

See [LICENSE](LICENSE).
