# WorkNet Project Setup Guide

## Project Overview
**WorkNet** is a Django-based job matching and worker management platform. It enables employers to post job requests and workers to apply for jobs, with AI-powered skill extraction and matching using Google Gemini API.

### Key Features:
- User registration (Workers, Employers, Admins)
- Job posting and management
- Worker profiles with skill extraction
- AI-powered job matching (using Google Gemini)
- Application management
- Rating and review system
- Task history and notifications
- Chatbot integration
- Dashboard for different user types

---

## System Requirements

- **Python**: 3.10 or higher
- **Database**: SQLite3 (default, no additional setup needed)
- **Operating System**: Windows, macOS, or Linux
- **Internet Connection**: Required for Gemini API integration

---

## Prerequisites

Install the following on your system:

### 1. Python
Download and install Python from [python.org](https://www.python.org/downloads/)
- Ensure "Add Python to PATH" is checked during installation
- Verify installation:
  ```bash
 python manage.py runserver
  ```

### 2. Git (Optional but recommended)
Download from [git-scm.com](https://git-scm.com)

### 3. Code Editor/IDE
- VS Code, PyCharm, or any preferred editor

---

## Step-by-Step Setup Instructions

### Step 1: Clone or Download the Project

```bash
# If using Git:
git clone <repository-url>
cd workon

# Or manually download and extract the project folder
```

### Step 2: Create Virtual Environment

A virtual environment keeps project dependencies isolated from system Python.

**On Windows (PowerShell/CMD):**
```bash
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**On macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

**Dependencies installed:**
- Django==4.2.7 (Web framework)
- google-generativeai==0.3.2 (AI skill extraction)
- requests==2.31.0 (HTTP library for web scraping)
- beautifulsoup4==4.12.2 (Web scraping)
- python-dotenv==1.0.0 (Environment variable management)

### Step 4: Configure Environment Variables

Create or update the `.env` file in the project root directory:

```bash
# Required: Google Gemini API Key (for AI features)
GEMINI_API_KEY=your_actual_gemini_api_key_here
```

**How to get a Gemini API Key:**
1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Click "Get API Key"
3. Create a new API key
4. Copy and paste it into the `.env` file

### Step 5: Initialize Database

Apply Django migrations to set up the database structure:

```bash
python manage.py migrate
```

This creates the SQLite database (`db.sqlite3`) with all required tables.

### Step 6: Create Sample Data (Optional)

Populate the database with initial skills data:

```bash
python manage.py create_sample_data
```

This adds common skills categories like Construction, IT, Design, etc.

### Step 7: Create Superuser (Admin Account)

Create an administrator account for accessing the Django admin panel:

```bash
python manage.py createsuperuser
```

Follow the prompts to set:
- Username
- Email address
- Password (enter twice for confirmation)

---

## Running the Application

### Start Development Server

```bash
python manage.py runserver
```

**Expected output:**
```
Starting development server at http://127.0.0.1:8000/
```

### Access the Application

Open your browser and navigate to:
- **Main Application**: http://127.0.0.1:8000/
- **Admin Panel**: http://127.0.0.1:8000/admin/
  - Log in with the superuser credentials created above

### Stop the Server

Press `Ctrl+C` in the terminal

---

## Project Structure

```
workon/
├── db.sqlite3                    # SQLite database
├── manage.py                     # Django management script
├── gemini_integration.py         # AI skill extraction and matching logic
├── requirements.txt              # Project dependencies
├── .env                          # Environment variables (API keys)
├── venv/                         # Virtual environment (auto-generated)
├── matcher/                      # Main Django app
│   ├── models.py                 # Database models (User, Job, Skills, etc.)
│   ├── views.py                  # Request handlers
│   ├── urls.py                   # URL routing
│   ├── forms.py                  # HTML forms
│   ├── admin.py                  # Django admin configuration
│   ├── chatbot.py                # Chatbot implementation
│   ├── matching.py               # Job matching logic
│   ├── templates/                # HTML templates
│   │   ├── base.html             # Base template
│   │   ├── registration/         # Login/Register pages
│   │   ├── dashboard/            # User dashboards
│   │   ├── jobs/                 # Job-related templates
│   │   ├── workers/              # Worker directory
│   │   └── ...
│   ├── static/                   # CSS, JavaScript, media files
│   └── management/commands/      # Custom management commands
│       ├── create_sample_data.py
│       └── scrape_jobs.py
├── worknet_matcher/              # Django project configuration
│   ├── settings.py               # Project settings
│   ├── urls.py                   # Main URL configuration
│   ├── wsgi.py                   # Production deployment config
│   └── asgi.py                   # Async support config
└── static/                       # Static files (CSS, JS)

```

---

## Key Database Models

### User Roles
- **Worker**: Can apply for jobs, upload profile
- **Employer**: Can post and manage job requests
- **Admin**: Can manage all users and content

### Main Models
- **WorkerProfile**: Extended user profile with skills, hourly rate, location
- **JobRequest**: Job postings by employers
- **Skill**: Available skills in the system
- **WorkerSkill**: Links workers to their skills with proficiency levels
- **JobApplication**: Applications from workers to job postings
- **Rating**: Reviews and ratings from employers about workers
- **TaskHistory**: History of completed tasks
- **JobMatch**: AI-matched job recommendations
- **Notification**: System notifications for users
- **ChatMessage**: Messages for in-app chatbot

---

## Important Configurations

### Django Settings (worknet_matcher/settings.py)

**Key settings to know:**
- `DEBUG = True`: Development mode (set to `False` for production)
- `SECRET_KEY`: Change this for production!
- `ALLOWED_HOSTS`: Add domain names for production
- `DATABASES`: Currently using SQLite (configure PostgreSQL for production)
- `STATIC_URL = '/static/'`: URL for static files (CSS, images, JS)

### Environment Variables (.env)
- `GEMINI_API_KEY`: Required for AI skill extraction and matching

---

## Common Commands

```bash
# Create new migration after modifying models
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Create superuser account
python manage.py createsuperuser

# Load sample skills data
python manage.py create_sample_data

# Scrape sample jobs (with count parameter)
python manage.py scrape_jobs --count 20

# Collect static files (for production)
python manage.py collectstatic

# Run tests (if tests are created)
python manage.py test

# Open Django shell for database queries
python manage.py shell
```

---

## Troubleshooting

### Issue: "Module not found" errors
**Solution:**
- Ensure virtual environment is activated: `.\venv\Scripts\Activate.ps1` (Windows)
- Reinstall requirements: `pip install -r requirements.txt`

### Issue: Database errors or "no such table"
**Solution:**
```bash
python manage.py migrate
```

### Issue: Gemini API errors
**Solution:**
- Verify `GEMINI_API_KEY` is set in `.env` file
- Check API key is valid at [Google AI Studio](https://aistudio.google.com/app/apikey)
- Ensure internet connection is active

### Issue: Static files not loading (CSS/JS missing)
**Solution:**
```bash
python manage.py collectstatic --noinput
```

### Issue: Port 8000 already in use
**Solution:**
```bash
python manage.py runserver 8001  # Use a different port
```

### Issue: Permission denied on activation script (macOS/Linux)
**Solution:**
```bash
chmod +x venv/bin/activate
source venv/bin/activate
```

---

## Development Workflow

### 1. Start Development
```bash
# Activate virtual environment
.\venv\Scripts\Activate.ps1  # Windows
source venv/bin/activate     # macOS/Linux

# Run development server
python manage.py runserver
```

### 2. Make Model Changes
```bash
# If you modify any models.py files:
python manage.py makemigrations
python manage.py migrate
```

### 3. Access Django Admin
- Visit http://127.0.0.1:8000/admin/
- Log in with superuser credentials
- Manage users, jobs, skills, ratings

### 4. Test the Features
- Register as Worker or Employer
- Create job postings (Employer)
- Apply for jobs (Worker)
- View matches and recommendations
- Rate and review workers

---

## Production Deployment

⚠️ **IMPORTANT: Before deploying to production:**

1. **Change DEBUG setting:**
   ```python
   # settings.py
   DEBUG = False
   ```

2. **Update SECRET_KEY:**
   - Generate a new secure key
   - Never hardcode sensitive data

3. **Set ALLOWED_HOSTS:**
   ```python
   ALLOWED_HOSTS = ['yourdomain.com', 'www.yourdomain.com', '127.0.0.1']
   ```

4. **Use PostgreSQL instead of SQLite:**
   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.postgresql',
           'NAME': 'worknet_db',
           'USER': 'db_user',
           'PASSWORD': 'db_password',
           'HOST': 'localhost',
           'PORT': '5432',
       }
   }
   ```

5. **Collect static files:**
   ```bash
   python manage.py collectstatic
   ```

6. **Use production servers:**
   - Gunicorn: `pip install gunicorn`
   - Nginx for reverse proxy
   - Apache alternative

---

## Support & Resources

- **Django Documentation**: https://docs.djangoproject.com/
- **Google Gemini API**: https://ai.google.dev/
- **Project Repository**: (add your repo URL)
- **Issue Tracker**: (add your issue tracker URL)

---

## Notes for Future Development

### Database Backup
- Regularly backup `db.sqlite3` (development)
- Use professional backup strategies for production

### API Rate Limiting
- Google Gemini API has rate limits
- Implement caching for repeated requests

### Security
- Never commit `.env` file to version control
- Use `.gitignore` to exclude sensitive files
- Keep dependencies updated

### Performance
- Consider using Celery for async tasks
- Implement caching layer (Redis)
- Optimize database queries

---

**Last Updated**: 2026-03-25
**Python Version**: 3.10+
**Django Version**: 4.2.7
