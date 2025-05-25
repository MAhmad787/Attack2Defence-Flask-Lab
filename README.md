# 🖥️ Flask Attendance System Deployment on Ubuntu Server

## Description

This project demonstrates how to deploy a Flask-based attendance system on an Ubuntu Server using Gunicorn and Nginx. The Flask application is connected to an SQLite database and served to a network using production-level tools. Nginx acts as a web server and reverse proxy, while Gunicorn serves the Flask app.

---

## 🔧 Steps to Deploy Flask App

### 1. Install Ubuntu Server on my machine

Ubuntu Server is installed on a local VM.

---

### 2. SSH into the Server

Logged into it using SSH because copy-pasting is not easy in VMware that's why I logged in here to do the work easily.

```bash
ssh flask_attendance@<server_ip>
```

---

### 3. Install required packages

I then install the required packages for the app such as python3, python3-venv, python3-pip, git.

```bash
sudo apt update
sudo apt install python3 python3-venv python3-pip git nginx -y
```

---

### 4. Clone the Flask App Repository

```bash
git clone https://github.com/MAhmad787/Student-Attendance-System.git
cd Student-Attendance-System
```

---

### 5. Create the virtual environment and install the requirements

Virtual environment is outside the main folder so I did:

```bash
cd ~
python3 -m venv venv
source ~/venv/bin/activate
cd Student-Attendance-System
pip install -r requirements.txt
```

---

### 6. Install Gunicorn

After that I have installed gunicorn on it.

```bash
pip install gunicorn
```

#### Gunicorn:

It is a Python WSGI HTTP server that is used to run Python Web Applications. It acts as an intermediary between the web server and the Python application, such as flask or django. It receives the request from the web server, transfers it to the application deployed on it, and sends back the response to the client.

---

### 7. Test Gunicorn

```bash
gunicorn --bind 127.0.0.1:8000 wsgi:app
```

Where `wsgi.py` is a file containing:

```python
from app import app
```

---

### 8. Create Systemd Service File

```bash
sudo nano /etc/systemd/system/attendance.service
```

Paste this (make sure the paths and user match your system):

```ini
[Unit]
Description=Gunicorn instance to serve attendance Flask app
After=network.target

[Service]
User=flask_attendance
Group=flask_attendance
WorkingDirectory=/home/flask_attendance/Student-Attendance-System
Environment="PATH=/home/flask_attendance/venv/bin"
ExecStart=/home/flask_attendance/venv/bin/gunicorn --workers 3 --bind 127.0.0.1:8000 wsgi:app

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl start attendance
sudo systemctl enable attendance
```

---

### 9. Install and Configure Nginx

```bash
sudo nano /etc/nginx/sites-available/attendance
```

Paste:

```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Then:

```bash
sudo ln -s /etc/nginx/sites-available/attendance /etc/nginx/sites-enabled
sudo nginx -t
sudo systemctl restart nginx
```

---

### 10. Final Verification

* Make sure Gunicorn and Nginx are enabled and running:

```bash
sudo systemctl status attendance
sudo systemctl status nginx
```

* Visit `http://<server_ip>` in your browser.

---

### ✅ Outcome

Now every time I start the server and type the IP address of it I can access the app, because I have enabled the services that will run automatically.

```
sudo systemctl enable attendance
sudo systemctl enable nginx
```

---

**Project complete.**
