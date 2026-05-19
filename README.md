# VPS Config

Configuration infrastructure du VPS `78.138.58.95` (Debian 12).

## Architecture

| App | Port | Route |
|-----|------|-------|
| VPS Monitor | 3020 | / |
| TP Vue API | 3003 | /B3dev-TP_VUE/api/ |
| TP Vue Front | 8080 | /B3dev-TP_VUE/ |
| SBV API | 3006 | /saintbarthvolley/api/ |
| SBV Front | 3007 | /saintbarthvolley/ |
| Lucky7 API | 3009 | /lucky7/ |
| Lucky7 Front | 3008 | /lucky7/ |
| CLB API | 3010 | /collegelaboussole/api/ |
| CLB Front | 3011 | /collegelaboussole/ |
| CineMap | 3012 | /cinemap/ |
| MongoDB | 27017 | interne |

## Reconfigurer de zéro

```bash
# 1. Cloner ce repo
git clone git@github.com:RustyRory/vps-config.git /var/www/vps-config

# 2. Créer le .env depuis le template
cp .env.example VPS-monitor/.env
nano VPS-monitor/.env  # remplir les secrets

# 3. Cloner les repos des apps
cd /var/www
git clone git@github.com:RustyRory/VPS-monitor.git
# ... autres repos

# 4. Configurer Nginx
sudo cp vps-config/nginx/sites-enabled/vps /etc/nginx/sites-enabled/vps
sudo nginx -t && sudo systemctl reload nginx

# 5. Lancer les apps
docker compose up -d
```

## Prérequis VPS

- Debian 12
- Docker + Docker Compose
- Nginx
- User `rusty` avec accès sudo et docker
