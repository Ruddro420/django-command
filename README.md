# Django Setup Guide (Windows + Git Bash)

A complete step-by-step guide to set up a Django development environment on **Windows using Git Bash**, create a project, create an app, configure SQLite, and run the development server.

---

# Table of Contents

- Prerequisites
- Step 1: Create Project Folder
- Step 2: Create Virtual Environment
- Step 3: Activate Virtual Environment
- Step 4: Upgrade pip
- Step 5: Install Django
- Step 6: Verify Installation
- Step 7: Save Requirements
- Step 8: Create Django Project
- Step 9: Run Development Server
- Step 10: Create Django App
- Step 11: Register App
- Step 12: Configure URLs
- Step 13: Create First View
- Step 14: Create Model
- Step 15: Make Migrations
- Step 16: Apply Migrations
- Step 17: Register Model in Admin
- Step 18: Create Superuser
- Step 19: Login to Admin Panel
- Step 20: Create Templates
- Step 21: Create Static Files
- Step 22: Install Useful Packages
- Step 23: Update Requirements
- Step 24: Deactivate Virtual Environment
- Final Project Structure
- Daily Django Workflow

---

# Prerequisites

Install the following:

- Python 3.x
- Git for Windows
- VS Code (Recommended)

Verify Python:

```bash
python --version
```

or

```bash
python3 --version
```

Verify pip:

```bash
pip --version
```

---

# Step 1: Create Project Folder

```bash
mkdir DjangoProject
```

Go inside the folder:

```bash
cd DjangoProject
```

---

# Step 2: Create Virtual Environment

```bash
python -m venv venv
```

Project structure:

```
DjangoProject/
│
└── venv/
```

---

# Step 3: Activate Virtual Environment (Git Bash)

```bash
source venv/Scripts/activate
```

If activated successfully, your terminal will look like:

```bash
(venv) user@computer MINGW64 ~/DjangoProject
```

Deactivate anytime:

```bash
deactivate
```

---

# Step 4: Upgrade pip

```bash
python -m pip install --upgrade pip
```

---

# Step 5: Install Django

```bash
pip install django
```

---

# Step 6: Verify Installation

Check Django version:

```bash
python -m django --version
```

---

# Step 7: Save Requirements

```bash
pip freeze > requirements.txt
```

Example:

```
Django==5.x.x
```

---

# Step 8: Create Django Project

Recommended:

```bash
django-admin startproject config .
```

Or

```bash
django-admin startproject myproject
```

Project structure:

```
DjangoProject/
│
├── config/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── manage.py
├── requirements.txt
└── venv/
```

---

# Step 9: Run Development Server

```bash
python manage.py runserver
```

Open:

```
http://127.0.0.1:8000/
```

Stop server:

```
CTRL + C
```

---

# Step 10: Create Django App

Example:

```bash
python manage.py startapp students
```

App structure:

```
students/
│
├── admin.py
├── apps.py
├── migrations/
├── models.py
├── tests.py
├── views.py
└── urls.py
```

---

# Step 11: Register App

Open:

```
config/settings.py
```

Add:

```python
INSTALLED_APPS = [
    ...
    "students",
]
```

---

# Step 12: Configure URLs

Create:

```
students/urls.py
```

```python
from django.urls import path
from . import views

urlpatterns = [

]
```

Now open:

```
config/urls.py
```

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path("", include("students.urls")),
]
```

---

# Step 13: Create First View

**views.py**

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello Django")
```

**students/urls.py**

```python
from django.urls import path
from .views import home

urlpatterns = [
    path("", home),
]
```

Visit:

```
http://127.0.0.1:8000/
```

Output:

```
Hello Django
```

---

# Step 14: Create Model

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()

    def __str__(self):
        return self.name
```

---

# Step 15: Make Migrations

```bash
python manage.py makemigrations
```

---

# Step 16: Apply Migrations

```bash
python manage.py migrate
```

SQLite database:

```
db.sqlite3
```

will be created automatically.

---

# Step 17: Register Model in Admin

**students/admin.py**

```python
from django.contrib import admin
from .models import Student

admin.site.register(Student)
```

---

# Step 18: Create Superuser

```bash
python manage.py createsuperuser
```

Example:

```
Username: admin
Email: admin@example.com
Password: ********
```

---

# Step 19: Login to Admin Panel

Run server:

```bash
python manage.py runserver
```

Visit:

```
http://127.0.0.1:8000/admin/
```

Login using your superuser credentials.

---

# Step 20: Create Templates

Folder:

```
students/
    templates/
        home.html
```

Example:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Home</title>
</head>
<body>

<h1>Hello Django</h1>

</body>
</html>
```

Render:

```python
from django.shortcuts import render

def home(request):
    return render(request, "home.html")
```

---

# Step 21: Create Static Files

```
students/
│
└── static/
    ├── css/
    ├── js/
    └── images/
```

---

# Step 22: Install Useful Packages

Django REST Framework

```bash
pip install djangorestframework
```

CORS Headers

```bash
pip install django-cors-headers
```

Image Processing

```bash
pip install pillow
```

Filtering

```bash
pip install django-filter
```

---

# Step 23: Update Requirements

```bash
pip freeze > requirements.txt
```

---

# Step 24: Deactivate Virtual Environment

```bash
deactivate
```

---

# Final Project Structure

```
DjangoProject/
│
├── config/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── students/
│   ├── migrations/
│   ├── templates/
│   │   └── home.html
│   ├── static/
│   │   ├── css/
│   │   ├── js/
│   │   └── images/
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
│
├── db.sqlite3
├── manage.py
├── requirements.txt
└── venv/
```

---

# Daily Django Workflow

Open Git Bash

Go to project

```bash
cd DjangoProject
```

Activate virtual environment

```bash
source venv/Scripts/activate
```

Run server

```bash
python manage.py runserver
```

After changing models

```bash
python manage.py makemigrations
python manage.py migrate
```

Create a new app

```bash
python manage.py startapp app_name
```

Install a package

```bash
pip install package_name
```

Update requirements

```bash
pip freeze > requirements.txt
```

Deactivate environment

```bash
deactivate
```

---

# Useful Commands

| Command | Description |
|----------|-------------|
| `python manage.py runserver` | Run development server |
| `python manage.py startapp app_name` | Create a new app |
| `python manage.py makemigrations` | Generate migration files |
| `python manage.py migrate` | Apply migrations |
| `python manage.py createsuperuser` | Create admin user |
| `python manage.py shell` | Open Django shell |
| `python manage.py showmigrations` | View migrations |
| `python manage.py collectstatic` | Collect static files |
| `python manage.py test` | Run tests |
| `python manage.py check` | Check project for issues |

---

# License

This project is open-source and available under the **MIT License**.

Happy Coding! 🚀
