# Student Management System

A full-stack student management system built with Django REST Framework and React.

## What was improved in this submission-ready version

- Removed hard-coded backend secrets and database credentials.
- Added environment-based configuration for Django and frontend API settings.
- Fixed the frontend grading endpoint path.
- Tightened role-based permissions for users, courses, tasks, resources, and announcements.
- Added authentication API tests.
- Added `.gitignore` and cleaner project setup guidance.
- Refactored repeated role checks into shared permission/mixin helpers.
- Added Render-ready production settings, static file handling, and database URL support.
- Added SPA rewrite support for frontend refresh-safe routing.

## Project structure

```text
student management system/
├── backend/
│   ├── announcements/
│   ├── courses/
│   ├── resources/
│   ├── student_system/
│   ├── tasks/
│   ├── users/
│   ├── .env.example
│   ├── manage.py
│   └── requirements.txt
├── frontend/
│   ├── src/
│   ├── .env.example
│   ├── package.json
│   └── vite.config.ts
└── README.md
```

## Main features

- Token-based authentication
- Role-based access control for student, teacher, and admin users
- Course creation and enrollment
- Task publishing, submission, and grading
- Resource upload and download
- Course announcements
- Frontend and backend separated through API calls

## Tech stack

### Backend

- Django
- Django REST Framework
- django-cors-headers
- PyMySQL
- SQLite for local development, optional MySQL or PostgreSQL for deployment

### Frontend

- React
- TypeScript
- Vite
- Axios
- React Router
- Ant Design

## Backend configuration

Copy the example file and update values as needed:

```bash
cd backend
cp .env.example .env
```

Important configurable values:

- `SECRET_KEY`
- `DEBUG`
- `ALLOWED_HOSTS`
- `DATABASE_URL`
- `DB_ENGINE`
- `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `DB_HOST`, `DB_PORT`
- `CORS_ALLOWED_ORIGINS`
- `CSRF_TRUSTED_ORIGINS`

### Local development database

Default local development uses SQLite.

### Optional MySQL configuration

Set the following in `backend/.env`:

```env
DB_ENGINE=mysql
DB_NAME=student_system
DB_USER=root
DB_PASSWORD=your_password
DB_HOST=127.0.0.1
DB_PORT=3306
```

## Frontend configuration

```bash
cd frontend
cp .env.example .env
```

Configurable values:

- `VITE_API_BASE_URL`
- `VITE_DEV_PROXY_TARGET`

For local development, keep:

```env
VITE_API_BASE_URL=/api
VITE_DEV_PROXY_TARGET=http://localhost:8000
```

## Installation

### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate
# Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Backend runs at `http://localhost:8000`.

### Frontend

```bash
cd frontend
npm install
cp .env.example .env
npm run dev
```

Frontend runs at `http://localhost:5173`.

## Running tests

```bash
cd backend
python manage.py test
```

The project includes API tests for authentication and existing model/API tests for courses and tasks.

## API examples

| Method | Path | Description |
|---|---|---|
| POST | `/api/auth/login/` | Login |
| POST | `/api/auth/register/` | Public registration |
| GET | `/api/auth/me/` | Current user |
| GET | `/api/courses/` | List courses |
| POST | `/api/courses/{id}/enroll/` | Enroll in a course |
| POST | `/api/submissions/{id}/grade/` | Grade a submission |

## Submission checklist

Before final submission, make sure you also provide:

- Public GitHub repository URL
- Public deployed application URL
- Test evidence screenshots
- Accessibility evidence
- Sustainability or Lighthouse evidence
- PDF report required by the assignment brief


## Render deployment

This repo now includes a `render.yaml` blueprint for one backend web service, one frontend static site, and one PostgreSQL database.

Backend production updates included in code:

- `gunicorn` for production startup
- `whitenoise` for static file serving
- `dj-database-url` for `DATABASE_URL` parsing
- PostgreSQL support through `psycopg`
- secure production defaults when `DEBUG=False`

Frontend deployment updates included in code:

- `public/_redirects` for SPA refresh handling
- Render rewrite rule in `render.yaml`
- environment-based `VITE_API_BASE_URL` for backend API switching
