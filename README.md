# AI Resume Evaluator

An AI-powered web app that scores a resume against a job description and returns structured, actionable feedback.

## Overview

Users upload a resume (PDF) along with a job description and receive an AI-generated evaluation covering a match score, key strengths, gaps, and an overall recommendation. Access is protected by JWT authentication, with role-based access for admin functionality.

## Core Features

- PDF resume upload with automatic text extraction
- AI-based resume evaluation against a job description, powered by OpenAI's GPT models
- Structured evaluation output: match score, key strengths, gaps, and an overall recommendation
- Optional custom prompt for tailoring the evaluation
- User authentication (register, login, current-user lookup) with hashed passwords and JWT tokens
- Role-based access control with an admin panel for listing, promoting, and removing users
- Dockerized backend and frontend for a consistent local setup

## Tech Stack

**Backend**
- FastAPI (Python)
- SQLModel + SQLite
- OpenAI API (gpt-4o-mini)
- pypdf for PDF text extraction
- JWT auth via python-jose, password hashing via passlib/bcrypt

**Frontend**
- React 18
- Vite
- React Router
- Axios

**Deployment**
- Docker and Docker Compose (separate backend and frontend containers)

## Project Structure

```
AI-Resume-Evaluator/
├── backend/
│   ├── routers/
│   │   ├── auth.py       # register, login, /me
│   │   ├── evaluate.py   # PDF upload + AI evaluation
│   │   └── admin.py      # user management (list, update role, delete)
│   ├── main.py
│   ├── database.py
│   ├── models.py
│   ├── schemas.py
│   ├── auth_utils.py
│   ├── pdf_utils.py
│   ├── llm.py
│   ├── Dockerfile
│   └── requirements.txt
├── frontend/
│   ├── src/
│   ├── index.html
│   ├── package.json
│   ├── vite.config.js
│   └── Dockerfile
└── Docker-compose.yml
```

## Getting Started

### Requirements

- Python 3.9+
- Node.js and npm
- An OpenAI API key
- Docker (optional, for the containerized setup)

### Option 1: Run with Docker Compose

1. Clone the repository:

```
git clone https://github.com/nadaalamri-9/AI-Resume-Evaluator.git
cd AI-Resume-Evaluator
```

2. Create a `backend/.env` file with your OpenAI API key:

```
OPENAI_API_KEY=your_openai_api_key
```

3. Start both services:

```
docker compose -f Docker-compose.yml up --build
```

4. The backend runs at http://localhost:5000 and the frontend runs at http://localhost:8000.

### Option 2: Run Manually

**Backend**

```
cd backend
python -m venv venv
source venv/bin/activate  # venv\Scripts\activate on Windows
pip install -r requirements.txt
uvicorn main:app --reload
```

**Frontend**

```
cd frontend
npm install
npm run dev
```

## API Overview

| Method | Endpoint | Description |
|---|---|---|
| POST | `/auth/register` | Create a new user account |
| POST | `/auth/login` | Authenticate and receive a JWT |
| GET | `/auth/me` | Get the current authenticated user |
| POST | `/evaluate/` | Upload a resume and job description for AI evaluation |
| GET | `/admin/users` | List all users (admin only) |
| PATCH | `/admin/users/{email}/role` | Update a user's role (admin only) |
| DELETE | `/admin/users/{email}` | Remove a user (admin only) |

## Environment Variables

| Variable | Purpose |
|---|---|
| `OPENAI_API_KEY` | OpenAI API key used to generate resume evaluations |

Never commit real API keys or `.env` files.

## Author

Nada Alamri
[github.com/nadaalamri-9](https://github.com/nadaalamri-9)
