# WorkNet - Quick Start Guide

## ⚡ Fast Setup (5 Minutes)

### 1. Activate Virtual Environment
```bash
# Windows
.\venv\Scripts\Activate.ps1

# macOS/Linux
source venv/bin/activate
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Set API Key
Create/update `.env` file:
```
GEMINI_API_KEY=your_gemini_api_key
```

> Get key: https://aistudio.google.com/app/apikey

### 4. Setup Database
```bash
python manage.py migrate
python manage.py create_sample_data
python manage.py createsuperuser
```

### 5. Run Server
```bash
python manage.py runserver
```

## 🌐 Access Points
- **App**: http://127.0.0.1:8000/
- **Admin**: http://127.0.0.1:8000/admin/

## 📝 Project Type
- **Framework**: Django 4.2.7
- **Database**: SQLite3
- **AI Service**: Google Gemini API
- **Key Features**: Job matching, worker profiles, chatbot, ratings

## 🔧 Useful Commands
```bash
# Make model changes take effect
python manage.py makemigrations
python manage.py migrate

# Interactive database shell
python manage.py shell

# Load job data (10 jobs)
python manage.py scrape_jobs --count 10

# Deactivate environment
deactivate
```

## 📂 Main App Folder
`matcher/` - Contains models, views, templates, forms

## ⚠️ Troubleshooting
| Problem | Solution |
|---------|----------|
| Module not found | Activate virtual env & reinstall: `pip install -r requirements.txt` |
| Database errors | Run: `python manage.py migrate` |
| API errors | Check `.env` has correct `GEMINI_API_KEY` |
| Port 8000 in use | Use: `python manage.py runserver 8001` |

## 📦 What's Included
- User authentication (Workers, Employers, Admins)
- Job posting & management
- AI-powered skill extraction & matching
- Application tracking
- Rating system
- Task history
- In-app chatbot
- Notifications

## 🚀 First Steps After Setup
1. Create admin account (superuser)
2. Log in to http://127.0.0.1:8000/admin/
3. Register as Worker or Employer
4. Create a job post (Employer)
5. Apply for jobs (Worker)
6. View AI-matched recommendations

---
See **SETUP.md** for complete detailed guide.
