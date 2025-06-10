# Deployment Guide

## Production Deployment

### Prerequisites
- Python 3.8+ on target server
- Web server (nginx recommended)
- Process manager (systemd, supervisor, or PM2)
- SSL certificate for HTTPS

## Environment Setup

### 1. Server Preparation
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Python and pip
sudo apt install python3 python3-pip python3-venv -y

# Install pipenv
pip3 install pipenv
```

### 2. Application Deployment
```bash
# Clone repository
git clone <repository-url>
cd flask-copilot-starter

# Install dependencies
pipenv install --deploy

# Set up environment variables
cp .env.example .env
# Edit .env with production values
```

### 3. Database Setup
```bash
# Run migrations
pipenv run flask db upgrade

# Create initial data (if needed)
pipenv run python scripts/seed_data.py
```

## Configuration

### Environment Variables (Production)
```bash
# Required
export SECRET_KEY="your-super-secret-production-key"
export FLASK_ENV="production"
export DATABASE_URL="postgresql://user:pass@localhost/dbname"

# Optional
export LOG_LEVEL="INFO"
export SSL_REDIRECT="true"
```

### Database Configuration
- Use PostgreSQL for production (not SQLite)
- Set up database backups
- Configure connection pooling
- Set up read replicas if needed

## Web Server Setup

### Nginx Configuration
```nginx
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

### Gunicorn Configuration
```python
# gunicorn.conf.py
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

### Systemd Service
```ini
# /etc/systemd/system/flask-app.service
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

## Security Considerations

### Application Security
- Use HTTPS only in production
- Set secure session cookies
- Implement rate limiting
- Regular security updates
- Monitor for vulnerabilities

### Server Security
- Configure firewall (UFW/iptables)
- Set up fail2ban for SSH protection
- Regular system updates
- Monitor system logs
- Use non-root user for application

## Monitoring and Logging

### Application Logging
```python
# Configure in production
import logging
from logging.handlers import RotatingFileHandler

if not app.debug:
    file_handler = RotatingFileHandler(
        'logs/app.log', 
        maxBytes=10240000, 
        backupCount=10
    )
    file_handler.setLevel(logging.INFO)
    app.logger.addHandler(file_handler)
```

### Health Checks
- Implement `/health` endpoint
- Monitor application metrics
- Set up alerts for failures
- Monitor database performance

## Backup Strategy

### Database Backups
```bash
# Daily backup script
#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
pg_dump dbname > /backups/backup_$DATE.sql
# Keep only last 30 days
find /backups -name "backup_*.sql" -mtime +30 -delete
```

### Application Backups
- Code is in version control
- Back up uploaded files
- Back up configuration files
- Document restore procedures

## Deployment Process

### 1. Pre-deployment Checklist
- [ ] Run all tests
- [ ] Update documentation
- [ ] Update changelog
- [ ] Create database backup
- [ ] Check environment variables

### 2. Deployment Steps
```bash
# Pull latest code
git pull origin main

# Install/update dependencies
pipenv install --deploy

# Run migrations
pipenv run flask db upgrade

# Restart application
sudo systemctl restart flask-app

# Verify deployment
curl -f https://your-domain.com/api/health
```

### 3. Rollback Procedure
```bash
# Revert to previous version
git checkout previous-release-tag

# Rollback database if needed
pipenv run flask db downgrade

# Restart application
sudo systemctl restart flask-app
```

## Performance Optimization

### Application Level
- Use database connection pooling
- Implement caching (Redis/Memcached)
- Optimize database queries
- Use CDN for static files

### Server Level
- Configure proper worker counts
- Use load balancing for multiple servers
- Monitor resource usage
- Optimize database configuration

## Troubleshooting

### Common Issues
- Check application logs: `/var/log/flask-app/`
- Check system logs: `journalctl -u flask-app`
- Verify environment variables
- Check database connectivity
- Verify SSL certificate validity

### Performance Issues
- Monitor CPU and memory usage
- Check database query performance
- Review application logs for errors
- Monitor response times

---
*Last updated: June 10, 2025*
