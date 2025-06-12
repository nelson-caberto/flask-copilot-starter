# Deployment Guide ⚡

> **SPEED-FIRST DEPLOYMENT** | Focus: Immediate Production Ready | No Over-Engineering

## ⚡ **AI Setup**: Say `reload_context.md` for instant project context

## ⚡ Quick Deployment (< 30 minutes total)
```bash
# IMMEDIATE DEPLOYMENT CHECKLIST - NO ANALYSIS
git pull origin main
pipenv install --deploy  
pipenv run flask db upgrade
sudo systemctl restart flask-app
curl -f https://your-domain.com/api/health  # VERIFY
```

## ⚡ Deployment Anti-Paralysis Rules

### IMMEDIATE Decision Hierarchy
1. **Standard deployment** (80% default) - Use proven patterns below
2. **Existing infrastructure** (15%) - Adapt current setup  
3. **Custom solution** (5% only) - When standards insufficient

### NO-ANALYSIS Deployment Operations
**Auto-proceed rules** - These require ZERO analysis:
- Server setup → Use Ubuntu LTS + nginx + systemd (standard stack)
- Database → Use PostgreSQL in production (never SQLite)
- SSL → Use Let's Encrypt or provided certificates
- Process management → Use systemd service (provided config)

### EMERGENCY Deployment Protocol  
**If stuck > 10 minutes on deployment decisions:**
1. ⏰ Use standard stack: Ubuntu + nginx + systemd + PostgreSQL
2. 🎯 Follow exact configurations provided below
3. 🚀 Deploy and iterate improvements later
4. 📖 Refer to existing production setups for guidance

## Production Deployment

### Prerequisites ⚡ (NO CUSTOMIZATION)
- **OS**: Ubuntu 20.04+ LTS (STANDARD - no analysis needed)
- **Python**: 3.8+ (use system package manager)
- **Web Server**: nginx (STANDARD - no alternatives analysis)
- **Process Manager**: systemd (STANDARD - no alternatives analysis)  
- **SSL**: Let's Encrypt or provided certificates (STANDARD)

## ⚡ Environment Setup (EXACT COMMANDS)

### 1. Server Preparation ⚡ (NO MODIFICATIONS)
```bash
# COPY-PASTE EXACTLY - NO ANALYSIS
sudo apt update && sudo apt upgrade -y
sudo apt install python3 python3-pip python3-venv nginx -y
pip3 install pipenv
```

### 2. Application Deployment ⚡ (NO MODIFICATIONS)
```bash
# COPY-PASTE EXACTLY - NO ANALYSIS  
git clone <repository-url>
cd flask-copilot-starter
pipenv install --deploy
cp .env.example .env
# Edit .env with production values (DATABASE_URL, SECRET_KEY)
```

### 3. Database Setup ⚡ (NO MODIFICATIONS)
```bash
# COPY-PASTE EXACTLY - NO ANALYSIS
pipenv run flask db upgrade
# Optional: pipenv run python scripts/seed_data.py
```

## ⚡ Configuration (COPY-PASTE READY)

### Environment Variables ⚡ (STANDARD - NO CUSTOMIZATION)
```bash
# PRODUCTION .ENV (copy exact template)
export SECRET_KEY="$(python3 -c 'import secrets; print(secrets.token_hex(32))')"
export FLASK_ENV="production"  
export DATABASE_URL="postgresql://user:pass@localhost/dbname"
export LOG_LEVEL="INFO"
export SSL_REDIRECT="true"
```

### Database Configuration ⚡ (NO ANALYSIS)
**MANDATORY production setup** - Use these exact settings:
- ✅ PostgreSQL (NEVER SQLite in production)
- ✅ Connection pooling enabled
- ✅ Daily automated backups  
- ✅ Read replicas (if high traffic)

## ⚡ Web Server Setup (EXACT CONFIGS)

### Nginx Configuration ⚡ (COPY-PASTE READY)
```nginx
# /etc/nginx/sites-available/flask-app (USE EXACTLY)
server {
    listen 80;
    server_name your-domain.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name your-domain.com;

    ssl_certificate /path/to/certificate.crt;
    ssl_certificate_key /path/to/private.key;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /static {
        alias /path/to/flask-copilot-starter/app/static;
        expires 1y;
        add_header Cache-Control "public, immutable";
    }
}
```

### Gunicorn Configuration ⚡ (COPY-PASTE READY)
```python
# gunicorn.conf.py (USE EXACTLY - NO MODIFICATIONS)
bind = "127.0.0.1:8000"
workers = 4
worker_class = "sync"
worker_connections = 1000
max_requests = 1000
max_requests_jitter = 50
preload_app = True
timeout = 30
keepalive = 2
```

### Systemd Service ⚡ (COPY-PASTE READY)
```ini
# /etc/systemd/system/flask-app.service (USE EXACTLY)
[Unit]
Description=Flask Copilot Starter
After=network.target

[Service]
User=www-data
Group=www-data
WorkingDirectory=/path/to/flask-copilot-starter
Environment=PATH=/path/to/flask-copilot-starter/.venv/bin
ExecStart=/path/to/flask-copilot-starter/.venv/bin/gunicorn -c gunicorn.conf.py run:app
ExecReload=/bin/kill -s HUP $MAINPID
Restart=always

[Install]
WantedBy=multi-user.target
```

## ⚡ Deployment Process (EXACT STEPS)

### 1. Pre-deployment Checklist ⚡ (< 5 minutes)
```bash
# MANDATORY CHECKS - NO SKIPPING
pipenv run pytest | grep -q "FAILED" && echo "❌ TESTS FAILING" || echo "✅ ALL TESTS PASS"
git status                           # ✅ Clean working directory  
grep -r "TODO\|FIXME" app/          # ✅ No critical TODOs
curl -f https://staging-domain.com/api/health  # ✅ Staging works
```

### 2. Deployment Steps ⚡ (< 10 minutes)
```bash
# COPY-PASTE EXACTLY - NO MODIFICATIONS
git pull origin main
pipenv install --deploy
pipenv run flask db upgrade
sudo systemctl restart flask-app
sleep 5
curl -f https://your-domain.com/api/health
```

### 3. IMMEDIATE Rollback (< 2 minutes)
```bash
# IF HEALTH CHECK FAILS - EXECUTE IMMEDIATELY
git checkout previous-release-tag
pipenv run flask db downgrade  # Only if DB migration was applied
sudo systemctl restart flask-app
curl -f https://your-domain.com/api/health  # Verify rollback
```

## ⚡ Security & Monitoring (STANDARD SETUP)

### MANDATORY Security Checklist ⚡ (NO ANALYSIS)
```bash
# COPY-PASTE SECURITY SETUP (< 10 minutes)
sudo ufw enable                          # Firewall
sudo ufw allow 22/tcp                    # SSH
sudo ufw allow 80/tcp                    # HTTP  
sudo ufw allow 443/tcp                   # HTTPS
sudo apt install fail2ban -y             # SSH protection
```

### IMMEDIATE Monitoring Setup ⚡
```python
# Add to app/__init__.py (STANDARD - NO CUSTOMIZATION)
import logging
from logging.handlers import RotatingFileHandler

if not app.debug:
    file_handler = RotatingFileHandler('logs/app.log', maxBytes=10240000, backupCount=10)
    file_handler.setLevel(logging.INFO)
    app.logger.addHandler(file_handler)
```

### AUTOMATED Backup Script ⚡ (COPY-PASTE READY)
```bash
#!/bin/bash
# /etc/cron.daily/flask-backup (USE EXACTLY)
DATE=$(date +%Y%m%d_%H%M%S)
pg_dump dbname > /backups/backup_$DATE.sql
find /backups -name "backup_*.sql" -mtime +30 -delete
```

## ⚡ Production Troubleshooting (IMMEDIATE ACTIONS)

### App Not Starting ⚡ (< 2 minutes diagnosis)
```bash
# IMMEDIATE DIAGNOSTIC COMMANDS
sudo systemctl status flask-app          # Check service status
sudo journalctl -u flask-app --since "1 hour ago" # Check logs
sudo -u www-data pipenv run flask db upgrade      # Test DB connection  
```

### Performance Issues ⚡ (< 5 minutes diagnosis)  
```bash
# IMMEDIATE PERFORMANCE CHECK
htop                                     # CPU/Memory usage
sudo journalctl -u flask-app | grep ERROR # Application errors
curl -w "%{time_total}" https://your-domain.com/api/health # Response time
```

### EMERGENCY Recovery Protocol ⚡
**If production is down > 5 minutes:**
1. ⏰ **ROLLBACK** immediately using commands above
2. 🎯 **VERIFY** rollback successful with health check
3. 🚀 **INVESTIGATE** in staging environment only
4. 📖 **DOCUMENT** issue for post-mortem analysis

---
*Last updated: June 11, 2025 - Enhanced with speed-first deployment patterns*
*Update this guide when deployment processes or infrastructure requirements change.*
