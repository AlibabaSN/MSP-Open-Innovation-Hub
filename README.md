# MSP-Open-Innovation-Hub

A full-stack innovation hub for MSPs and IT teams.
Users can propose ideas, comment, vote, and track progress on a Kanban board.
Admins can approve and manage ideas.

Authentication is powered by Google & GitHub OAuth, with sessions stored in Postgres.

# 🛠 Tech Stack

🌐 Frontend: React (Vite) + TailwindCSS

⚙️ Backend: Node.js + Express + Knex + PostgreSQL

🔑 Auth: OAuth2 (Google, GitHub) + sessions (Postgres store)

📊 Features: Ideas, Votes, Comments, Kanban board, Admin tools

🐳 Docker Compose: Local development setup

✅ CI/CD: GitHub Actions + Railway (API) + Vercel (Web)


# 🔧 Local Development Setup

git clone <repo-url>

cd msp-open-innovation-hub

cp api/.env.example api/.env

docker compose up --build

Frontend → http://localhost:5173

API → http://localhost:4000

PgAdmin → http://localhost:5050

# 🗄 Database Migrations

Migrations use Knex:
cd api
npm run migrate      # apply migrations
npm run migrate:make add_new_table

# 🔑 OAuth Setup (Google + GitHub)

  # Google OAuth
  1. Go to Google Cloud Console.
  2. Create a new project → Enable OAuth consent screen.
  3. Add credentials → OAuth client ID → Web application.
  4. Add redirect URI:http://localhost:4000/auth/google/callback
     https://<railway-app>.up.railway.app/auth/google/callback

  # GitHub OAuth
  1. Go to GitHub Developer Settings
  2. Create new OAuth App.
  3. Add callback URL:http://localhost:4000/auth/github/callback
https://<railway-app>.up.railway.app/auth/github/callback

# ⚡ CI/CD Setup (GitHub Actions)

The workflow (.github/workflows/ci.yml) does:

Spin up Postgres

Run migrations

Run backend + frontend tests

Build frontend

Deploy → Railway (API) & Vercel (Web)

# Add GitHub Secrets

Go to GitHub repo → Settings → Secrets → Actions and add:

RAILWAY_API_KEY

RAILWAY_PROJECT_ID

VERCEL_TOKEN

VERCEL_ORG_ID

VERCEL_PROJECT_ID

DATABASE_URL

SESSION_SECRET

GOOGLE_CLIENT_ID / GOOGLE_CLIENT_SECRET

GITHUB_CLIENT_ID / GITHUB_CLIENT_SECRET


# 🚀 Deployment
 # Backend → Railway

Go to Railway
, create a project.

Add Postgres Plugin (it auto-creates DATABASE_URL).

Connect GitHub repo.

Add secrets (OAuth + Session + DB).

Deploy → logs will show Running migrations....


# Frontend → Vercel

Go to Vercel
Import GitHub repo → select /web.
Add env var: VITE_API_URL=https://<railway-app>.up.railway.app
Deploy → you’ll get https://<your-app>.vercel.app.

# ✅ After Deployment

Frontend at: https://<your-app>.vercel.app

API at: https://<railway-app>.up.railway.app

Login with Google/GitHub works end-to-end.

Admin can log in → manage ideas → track progress via Kanban.



