<div align="center">

# 🐳 Docker Development Environment

<!-- Badges -->
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Docker Compose](https://img.shields.io/badge/Docker%20Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docs.docker.com/compose/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)](https://github.com)
[![Last Updated](https://img.shields.io/badge/Last%20Updated-May%202026-blue?style=for-the-badge)](CHANGELOG.md)

**Panduan lengkap untuk setup dan menjalankan Docker environment di project ini.**

[Report Bug](../../issues) · [Request Feature](../../issues) · [Documentation](DOCUMENTATION.md)

</div>

---

## 📋 Daftar Isi

- [Overview](#overview)
- [Fitur Utama](#fitur-utama)
- [Release & Version](#release--version)
- [Quick Start](#quick-start)
- [Persyaratan Sistem](#persyaratan-sistem)
- [Instalasi Docker](#instalasi-docker)
- [Konfigurasi Environment](#konfigurasi-environment)
- [Menjalankan Container](#menjalankan-container)
- [Struktur Project](#struktur-project)
- [Perintah Dasar](#perintah-dasar)
- [Update Hosts File](#update-hosts-file)
- [SSL & Domain Setup](#ssl--domain-setup)
- [Menambah PHP Service](#menambah-php-service)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [Support](#support)
- [License](#license)

---

## 📖 Overview

Project ini menyediakan complete Docker setup untuk development environment yang mendukung:
- **PHP Versions**: 7.4, 8.0, 8.2, 8.3
- **Web Server**: Nginx
- **Databases**: MySQL, PostgreSQL
- **Cache**: Redis
- **Storage**: MinIO
- **Node.js Applications**: Multiple services

> 📌 **Catatan**: Ini adalah project pribadi untuk development dan testing.

---

## ✨ Fitur Utama

- ✅ Multi PHP Version Support (7.4, 8.0, 8.2, 8.3)
- ✅ Automated Container Orchestration
- ✅ Persistent Data Volumes
- ✅ SSL/TLS Support
- ✅ Development & Staging Environments
- ✅ Easy Configuration Management
- ✅ Comprehensive Documentation
- ✅ Troubleshooting Guide

---

## 🚀 Release & Version

| Version | Release Date | Status | Notes |
|---------|-------------|--------|-------|
| **v2.0.0** | May 2026 | Current | Multi-PHP, Production-Ready |
| v1.5.0 | April 2026 | Stable | Enhancement Release |
| v1.0.0 | January 2026 | Deprecated | Initial Release |

📝 **[See CHANGELOG.md](CHANGELOG.md)** for detailed version history

**Current Version**: `v2.0.0-alpha`  
**Docker Compose Version**: `3.8+`

---

## 🎯 Quick Start

```bash
# 1. Clone atau navigasi ke project
cd /path/to/project

# 2. Setup .env file
cd docker/
cp .env.example .env

# 3. Konfigurasi UID dan GID
# Edit docker/.env dengan output dari: id

# 4. Start containers
docker-compose up -d

# 5. Verifikasi
docker-compose ps
```

> 📖 Untuk setup lebih detail, lihat bagian [Konfigurasi Environment](#konfigurasi-environment)

## 🔧 Persyaratan Sistem

Pastikan sistem Anda memenuhi persyaratan berikut:

- **OS**: Linux, macOS, atau Windows (dengan WSL2)
- **RAM**: Minimal 4GB, disarankan 8GB+
- **Disk Space**: Minimal 10GB untuk images dan volumes
- **CPU**: Multi-core processor

## 📦 Instalasi Docker

### Linux (Ubuntu/Debian)

```bash
# Update package list
sudo apt-get update

# Install Docker
sudo apt-get install -y docker.io

# Install Docker Compose
sudo apt-get install -y docker-compose

# Tambahkan user ke docker group (opsional, untuk menghindari sudo)
sudo usermod -aG docker $USER
newgrp docker

# Verifikasi instalasi
docker --version
docker-compose --version
```

### macOS

```bash
# Install Docker Desktop dari https://www.docker.com/products/docker-desktop
# atau menggunakan Homebrew:
brew install docker docker-compose
```

### Windows (WSL2)

1. Install WSL2 dari https://docs.microsoft.com/en-us/windows/wsl/install
2. Install Docker Desktop dari https://www.docker.com/products/docker-desktop
3. Pastikan WSL2 terpilih di Docker Desktop settings

---

## ⚙️ Konfigurasi Environment

### 1. Setup .env File

Di direktori `docker/`, copy file `.env.example` ke `.env`:

```bash
cd docker/
cp .env.example .env
```

### 2. Konfigurasi UID dan GID

Cari tahu UID dan GID Anda dengan perintah:

```bash
id
# Output contoh: uid=1000(username) gid=1000(username) groups=1000(username)
```

Edit file `docker/.env` dan isi dengan UID dan GID Anda:

```bash
# docker/.env
UID=1000
GID=1000
```

> **Catatan**: Ini penting untuk menghindari permission issues antara container dan host machine.

---

## 🚀 Menjalankan Container

### Start Container

Dari direktori `docker/`:

```bash
# Build dan jalankan container
docker-compose up -d

# Jika ingin melihat logs
docker-compose up
```

### Verifikasi Container Running

```bash
# Lihat daftar container
docker-compose ps

# Lihat logs service tertentu
docker-compose logs nginx
docker-compose logs php80
```

### Stop Container

```bash
# Stop semua container
docker-compose stop

# Stop container tertentu
docker-compose stop php74
```

### Restart Container

```bash
# Restart semua container
docker-compose restart

# Restart container tertentu
docker-compose restart php82
```

---

## 📁 Struktur Project

```
project/
├── docker/                      # Docker configuration
│   ├── docker-compose.yml       # Main compose file
│   ├── .env.example             # Environment template
│   ├── .env                     # Environment file (create from example)
│   ├── docker-volumes/          # Persistent data volumes
│   │   ├── minio-data/
│   │   ├── mysql-data/
│   │   ├── postgres-data/
│   │   ├── redis-data/
│   │   └── portainer/
│   └── Dockerfile               # Custom Docker images
│
├── php/                         # PHP configuration
│   ├── docker/
│   │   ├── php74/
│   │   ├── php80/
│   │   ├── php82/
│   │   └── php83/
│   ├── nginx/                   # Nginx configuration
│   │   ├── p74.conf
│   │   ├── p80.conf
│   │   ├── p82.conf
│   │   └── p83.conf
│   ├── ssl/                     # SSL certificates
│   └── www/                     # Web root
│       ├── html/
│       ├── p74/
│       ├── p80/
│       ├── p82/
│       └── p83/
│
├── node/                        # Node.js applications
│   ├── pp-stream-api/
│   └── retts-webapp-api/
│
├── docker-tools/                # Additional Docker tools
│   ├── docker-compose-local.yml
│   ├── docker-compose-staging.yml
│   ├── db-init/
│   └── ...
│
└── README.md                    # File ini
```

---

## 📝 Perintah Dasar

### Container Management

```bash
# Build images
docker-compose build

# Build dan jalankan
docker-compose up -d

# Rebuild images (tanpa cache)
docker-compose build --no-cache
docker-compose up -d

# Remove container (jangan hilangkan data)
docker-compose down

# Remove container dan volumes (HATI-HATI: data akan dihapus)
docker-compose down -v

# View running containers
docker-compose ps

# View all containers (termasuk yang tidak running)
docker-compose ps -a
```

### Logs & Debugging

```bash
# Lihat logs real-time
docker-compose logs -f

# Lihat logs service tertentu
docker-compose logs -f nginx
docker-compose logs -f php80

# Lihat logs terakhir 100 line
docker-compose logs --tail=100
```

### Execute Commands

```bash
# Masuk ke container bash
docker-compose exec php80 bash

# Jalankan command di container
docker-compose exec php80 php -v

# Jalankan command di nginx
docker-compose exec nginx bash
```

### Network & Ports

```bash
# Lihat network
docker network ls

# Inspect network
docker network inspect dev-docker-net

# Lihat port yang dibuka
docker-compose ps
```

---
## 🌐 Update Hosts File

Agar domain lokal dapat diakses dari browser, perlu menambahkan entry ke file hosts sistem Anda.

### Daftar Domain

Sebelum update hosts, ketahui domain apa saja yang akan digunakan:

```
127.0.0.1    localhost
127.0.0.1    myapp.local
127.0.0.1    www.myapp.local
127.0.0.1    api.myapp.local
127.0.0.1    admin.myapp.local
127.0.0.1    p74.localhost
127.0.0.1    p80.localhost
127.0.0.1    p82.localhost
127.0.0.1    p83.localhost
```

### Linux / macOS

#### Method 1: Using Text Editor (Recommended)

```bash
# Buka file hosts dengan nano editor
sudo nano /etc/hosts

# Atau gunakan vim
sudo vim /etc/hosts
```

**Tambahkan baris ini di akhir file:**

```
# Development Docker Environment
127.0.0.1    myapp.local www.myapp.local
127.0.0.1    api.myapp.local
127.0.0.1    admin.myapp.local
127.0.0.1    p74.localhost
127.0.0.1    p80.localhost
127.0.0.1    p82.localhost
127.0.0.1    p83.localhost
```

**Save file:**
- **nano**: `Ctrl + O` → `Enter` → `Ctrl + X`
- **vim**: `Esc` → `:wq` → `Enter`

#### Method 2: Using Command Line

```bash
# Append domain ke hosts file
sudo bash -c 'echo "127.0.0.1    myapp.local www.myapp.local" >> /etc/hosts'
sudo bash -c 'echo "127.0.0.1    api.myapp.local" >> /etc/hosts'
sudo bash -c 'echo "127.0.0.1    admin.myapp.local" >> /etc/hosts'
sudo bash -c 'echo "127.0.0.1    p74.localhost" >> /etc/hosts'
sudo bash -c 'echo "127.0.0.1    p80.localhost" >> /etc/hosts'
sudo bash -c 'echo "127.0.0.1    p82.localhost" >> /etc/hosts'
sudo bash -c 'echo "127.0.0.1    p83.localhost" >> /etc/hosts'
```

#### Method 3: Using heredoc

```bash
sudo tee -a /etc/hosts > /dev/null << EOF
# Development Docker Environment
127.0.0.1    myapp.local www.myapp.local
127.0.0.1    api.myapp.local
127.0.0.1    admin.myapp.local
127.0.0.1    p74.localhost
127.0.0.1    p80.localhost
127.0.0.1    p82.localhost
127.0.0.1    p83.localhost
EOF
```

#### Verify

```bash
# Lihat hosts file
cat /etc/hosts

# Test DNS resolution
ping -c 1 myapp.local
ping -c 1 api.myapp.local
```

#### Clear DNS Cache (jika diperlukan)

**macOS:**
```bash
sudo dscacheutil -flushcache
```

**Linux (Ubuntu/Debian):**
```bash
sudo systemctl restart systemd-resolved
```

**Linux (Fedora/CentOS):**
```bash
sudo systemctl restart nscd
```

---

### Windows

#### Method 1: Using Notepad (Recommended)

**Buka File Explorer:**
1. Navigasi ke: `C:\Windows\System32\drivers\etc\`
2. Cari file `hosts` (tanpa extension)

**Edit dengan Notepad:**
1. Right-click file `hosts` → **"Open with..."** → **Notepad** (Run as Administrator)
2. Atau: **Notepad** → **File** → **Open** → `C:\Windows\System32\drivers\etc\hosts`

**Tambahkan di akhir file:**

```
# Development Docker Environment
127.0.0.1    myapp.local www.myapp.local
127.0.0.1    api.myapp.local
127.0.0.1    admin.myapp.local
127.0.0.1    p74.localhost
127.0.0.1    p80.localhost
127.0.0.1    p82.localhost
127.0.0.1    p83.localhost
```

**Save:** `Ctrl + S`

#### Method 2: Using PowerShell (Admin)

```powershell
# Buka PowerShell as Administrator

# Tambahkan domain ke hosts file
Add-Content C:\Windows\System32\drivers\etc\hosts "`n127.0.0.1    myapp.local www.myapp.local"
Add-Content C:\Windows\System32\drivers\etc\hosts "`n127.0.0.1    api.myapp.local"
Add-Content C:\Windows\System32\drivers\etc\hosts "`n127.0.0.1    admin.myapp.local"
Add-Content C:\Windows\System32\drivers\etc\hosts "`n127.0.0.1    p74.localhost"
Add-Content C:\Windows\System32\drivers\etc\hosts "`n127.0.0.1    p80.localhost"
Add-Content C:\Windows\System32\drivers\etc\hosts "`n127.0.0.1    p82.localhost"
Add-Content C:\Windows\System32\drivers\etc\hosts "`n127.0.0.1    p83.localhost"
```

#### Method 3: Using Command Prompt (Admin)

```batch
@echo off
REM Buka Command Prompt as Administrator

REM Add domains
echo 127.0.0.1    myapp.local www.myapp.local >> C:\Windows\System32\drivers\etc\hosts
echo 127.0.0.1    api.myapp.local >> C:\Windows\System32\drivers\etc\hosts
echo 127.0.0.1    admin.myapp.local >> C:\Windows\System32\drivers\etc\hosts
echo 127.0.0.1    p74.localhost >> C:\Windows\System32\drivers\etc\hosts
echo 127.0.0.1    p80.localhost >> C:\Windows\System32\drivers\etc\hosts
echo 127.0.0.1    p82.localhost >> C:\Windows\System32\drivers\etc\hosts
echo 127.0.0.1    p83.localhost >> C:\Windows\System32\drivers\etc\hosts

pause
```

#### Verify

**Command Prompt / PowerShell:**
```powershell
# Lihat hosts file
type C:\Windows\System32\drivers\etc\hosts

# Test DNS resolution
ping myapp.local
ping api.myapp.local
```

#### Clear DNS Cache

```powershell
# PowerShell (Admin)
ipconfig /flushdns
```

---

### Verify Setup

Setelah update hosts file, test akses domain:

```bash
# Test ping
ping myapp.local
ping api.myapp.local

# Test curl
curl http://myapp.local
curl http://api.myapp.local

# Atau buka di browser
# http://myapp.local
# http://api.myapp.local
# http://p80.localhost
# https://myapp.local (dengan SSL certificate)
```

### Troubleshooting Hosts

**Domain tidak terdeteksi setelah di-add?**

1. **Restart DNS cache** (lihat section di atas)
2. **Flush browser cache**: 
   - Chrome: `Ctrl + Shift + Delete`
   - Firefox: `Ctrl + Shift + Delete`
3. **Close dan open browser kembali**
4. **Verify file hosts** sudah benar-benar ter-save:
   ```bash
   cat /etc/hosts  # Linux/macOS
   type C:\Windows\System32\drivers\etc\hosts  # Windows
   ```

**Masih error connection refused?**

1. Pastikan Docker container sudah running: `docker-compose ps`
2. Pastikan port 80/443 tidak diblokir firewall
3. Check Nginx logs: `docker-compose logs -f nginx`

---
## � SSL & Domain Setup

### Setup Local Domain dengan SSL

Untuk development environment dengan HTTPS, ikuti langkah berikut:

#### 1. Update Hosts File

**PENTING:** Sebelum lanjut, pastikan sudah update hosts file agar domain bisa diakses.

Lihat section **[Update Hosts File](#update-hosts-file)** untuk panduan lengkap setup domain lokal di sistem operasi Anda.

Quick reference:

```bash
# Tambahkan ke /etc/hosts:
127.0.0.1    myapp.local www.myapp.local
127.0.0.1    api.myapp.local
127.0.0.1    admin.myapp.local
```

#### 2. Generate Self-Signed SSL Certificate

Jika belum ada sertifikat di `php/ssl/`:

```bash
cd php/ssl/

# Generate private key
openssl genrsa -out myapp.local.key 2048

# Generate certificate (valid 365 hari)
openssl req -new -x509 -key myapp.local.key -out myapp.local.crt -days 365 \
  -subj "/C=ID/ST=State/L=City/O=Organization/CN=myapp.local"

# List sertifikat
ls -la *.crt *.key
```

#### 3. Configure Nginx untuk Domain

Edit Nginx config file (misal `php/nginx/p80.conf`):

```nginx
server {
    listen 80;
    listen 443 ssl http2;
    
    server_name myapp.local www.myapp.local;
    
    # SSL Configuration
    ssl_certificate /etc/nginx/ssl/myapp.local.crt;
    ssl_certificate_key /etc/nginx/ssl/myapp.local.key;
    
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    
    # Redirect HTTP ke HTTPS
    if ($scheme != "https") {
        return 301 https://$server_name$request_uri;
    }
    
    root /var/www/p80/public;
    index index.php;
    
    location ~ \.php$ {
        fastcgi_pass php80:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
    
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
}
```

#### 4. Restart Nginx Container

```bash
cd docker/
docker-compose restart nginx
```

#### 5. Access dengan HTTPS

```
https://myapp.local
https://api.myapp.local
```

> **Catatan**: Browser akan menampilkan warning "Not Secure" karena self-signed certificate. Klik "Advanced" → "Proceed" untuk melanjutkan.

#### 6. Trust Self-Signed Certificate (Opsional)

Untuk menghilangkan warning:

**macOS:**
```bash
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain php/ssl/myapp.local.crt
```

**Linux (Ubuntu):**
```bash
sudo cp php/ssl/myapp.local.crt /usr/local/share/ca-certificates/
sudo update-ca-certificates
```

**Windows:**
1. Open "Manage user certificates" (certmgr.msc)
2. Right-click "Trusted Root Certification Authorities" → "All Tasks" → "Import"
3. Select `php/ssl/myapp.local.crt`

---

## 🐘 Menambah PHP Service

### Menambah Versi PHP Baru (Contoh: PHP 8.4)

Ikuti langkah-langkah di bawah untuk menambahkan PHP version baru:

#### 1. Buat Dockerfile untuk PHP Baru

Buat file `php/docker/php84/Dockerfile`:

```dockerfile
FROM php:8.4-fpm-alpine

# Install essential packages
RUN apk add --no-cache \
    curl \
    git \
    zip \
    unzip \
    libzip-dev \
    oniguruma-dev \
    postgresql-dev

# Install PHP extensions
RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    mbstring \
    zip \
    bcmath

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www

CMD ["php-fpm"]
```

#### 2. Edit `docker/docker-compose.yml`

Tambahkan service baru setelah service `php83`:

```yaml
  php84:
    build: ../php/docker/php84
    container_name: dev-php84
    user: "${UID}:${GID}"
    volumes:
      - ../php/www:/var/www
    networks:
      - default
    restart: always
    environment:
      - PHP_IDE_CONFIG=serverName=php84
```

#### 3. Buat Nginx Config untuk PHP 8.4

Buat file `php/nginx/p84.conf`:

```nginx
server {
    listen 80;
    server_name p84.localhost;
    
    root /var/www/p84/public;
    index index.php;
    
    location ~ \.php$ {
        fastcgi_pass php84:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
    
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
}
```

#### 4. Update Main Nginx Config

Edit `php/nginx/p80.conf` (atau config utama) untuk include PHP 8.4 config:

```nginx
include /etc/nginx/conf.d/p84.conf;
```

#### 5. Buat Web Root Directory

```bash
# Buat folder untuk aplikasi
mkdir -p php/www/p84/public

# Buat file index.php untuk testing
cat > php/www/p84/public/index.php << 'EOF'
<?php
phpinfo();
?>
EOF
```

#### 6. Update docker-compose.yml

Pastikan nginx bergantung pada php84:

```yaml
nginx:
    depends_on:
      - php74
      - php80
      - php82
      - php83
      - php84  # Tambahkan ini
    restart: always
```

#### 7. Build dan Restart Container

```bash
cd docker/

# Build image baru
docker-compose build php84

# Restart container
docker-compose down
docker-compose up -d

# Verify
docker-compose ps
```

#### 8. Test PHP 8.4

```bash
# Akses PHP 8.4 melalui browser
http://p84.localhost

# Atau test via terminal
docker-compose exec php84 php -v
```

### Quick Script untuk Menambah PHP Service

Atau gunakan script ini untuk otomasi:

```bash
#!/bin/bash
# Script untuk menambah PHP service baru

PHP_VERSION=$1
PHP_PORT=$2

if [ -z "$PHP_VERSION" ] || [ -z "$PHP_PORT" ]; then
    echo "Usage: ./add-php-service.sh <version> <port>"
    echo "Example: ./add-php-service.sh 8.5 85"
    exit 1
fi

PHP_DIR="php/docker/php${PHP_VERSION}"
mkdir -p "$PHP_DIR"

# Create Dockerfile
cat > "$PHP_DIR/Dockerfile" << EOF
FROM php:${PHP_VERSION}-fpm-alpine

RUN apk add --no-cache \
    curl git zip unzip libzip-dev oniguruma-dev postgresql-dev

RUN docker-php-ext-install \
    pdo pdo_mysql pdo_pgsql mbstring zip bcmath

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www
CMD ["php-fpm"]
EOF

# Create Nginx config
cat > "php/nginx/p${PHP_PORT}.conf" << EOF
server {
    listen 80;
    server_name p${PHP_PORT}.localhost;
    
    root /var/www/p${PHP_PORT}/public;
    index index.php;
    
    location ~ \.php$ {
        fastcgi_pass php${PHP_VERSION}:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME \$document_root\$fastcgi_script_name;
        include fastcgi_params;
    }
    
    location / {
        try_files \$uri \$uri/ /index.php?\$query_string;
    }
}
EOF

# Create web root
mkdir -p "php/www/p${PHP_PORT}/public"

cat > "php/www/p${PHP_PORT}/public/index.php" << 'EOF'
<?php
phpinfo();
?>
EOF

echo "✅ PHP ${PHP_VERSION} service files created!"
echo "📝 Now edit docker-compose.yml to add the service and rebuild"
```

Gunakan:
```bash
chmod +x add-php-service.sh
./add-php-service.sh 8.5 85
```

#### Tips Menambah Service

1. **Duplicate Service** - Copy config dari PHP version terdekat
2. **Update Dependencies** - Pastikan nginx bergantung pada PHP service baru
3. **Test Connection** - Verify dengan `docker-compose exec php84 php -v`
4. **Check Logs** - `docker-compose logs -f php84`
5. **Volume Sharing** - Semua PHP service menggunakan volume `../php/www`

---

## �🐛 Troubleshooting

### Port Already in Use

Jika port 80 atau 443 sudah digunakan:

```bash
# Cari proses yang menggunakan port
sudo lsof -i :80
sudo lsof -i :443

# Ubah port di docker-compose.yml
# ports:
#   - "8080:80"      # Map port 8080 host ke 80 container
#   - "8443:443"
```

### Permission Denied

Jika mendapat error permission:

```bash
# Tambahkan user ke docker group
sudo usermod -aG docker $USER

# Logout dan login kembali, atau jalankan:
newgrp docker

# Verifikasi
docker ps
```

### Container Restart Terus-menerus

```bash
# Lihat logs untuk error
docker-compose logs -f container_name

# Rebuild container
docker-compose down
docker-compose build --no-cache
docker-compose up -d
```

### Volume Permission Issues

```bash
# Check UID/GID di .env
cat docker/.env

# Jika perlu fix permissions di host
sudo chown -R $USER:$USER docker/docker-volumes/

# Atau gunakan docker-compose exec
docker-compose exec php80 chown -R www-data:www-data /var/www
```

### Out of Disk Space

```bash
# Bersihkan unused images dan containers
docker system prune

# Bersihkan lebih agresif (hati-hati)
docker system prune -a --volumes
```

### Service Not Starting

```bash
# Check logs detail
docker-compose logs service_name

# Rebuild specific service
docker-compose build --no-cache service_name
docker-compose up -d service_name

# Check dependencies
docker-compose ps
```

---

## 🔐 Security Tips

1. **Jangan commit `.env`** - Selalu gunakan `.env.example`
2. **Change default passwords** - Update credentials di `.env`
3. **Update images regularly** - Run `docker-compose pull` secara berkala
4. **Limit container resources** - Set memory/CPU limits di compose file
5. **Use strong SSL certificates** - Di production, gunakan certificate yang valid

---

## 📚 Referensi

- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Docker Hub](https://hub.docker.com/)

---

## 📞 Support & Community

### Mendapatkan Bantuan

Jika mengalami masalah:

1. Periksa logs: `docker-compose logs -f`
2. Lihat section [Troubleshooting](#troubleshooting)
3. Check Docker documentation

### Frequently Asked Questions (FAQ)

**Q: Port 80 already in use, gimana?**  
A: Lihat section [Port Already in Use](#port-already-in-use) di Troubleshooting

**Q: Bagaimana cara menggunakan PHP 8.3?**  
A: Edit `docker/docker-compose.yml` dan uncomment service `php83`

**Q: Bisa ganti database engine?**  
A: Ya, edit `docker/docker-compose.yml` dan tambahkan service database yang diinginkan

---

## 🤝 Contributing

Kontribusi sangat diterima! Berikut cara berkontribusi:

### Development Setup
1. Fork repository ini
2. Clone ke local machine
3. Create feature branch: `git checkout -b feature/amazing-feature`
4. Commit changes: `git commit -m 'Add amazing feature'`
5. Push to branch: `git push origin feature/amazing-feature`
6. Open Pull Request

### Guidelines
- ✅ Follow existing code style
- ✅ Update documentation
- ✅ Test perubahan sebelum submit PR
- ✅ Tulis commit message yang jelas

---

## 📄 License

Project ini dilisensikan di bawah **MIT License** - lihat [LICENSE](LICENSE) file untuk detail.

---

## 🙏 Acknowledgments

Terima kasih kepada:
- [Docker](https://www.docker.com/) - Container platform
- [Docker Compose](https://docs.docker.com/compose/) - Orchestration tool
- [PHP](https://www.php.net/) - Programming language
- [Nginx](https://nginx.org/) - Web server

---

## 🔗 Related Resources

| Resource | Link |
|----------|------|
| **Issues** | [Issues](https://github.com) |
| **Discussions** | [Discussions](https://github.com) |
| **Releases** | [Releases](https://github.com) |

---

<div align="center">

## ⭐ Catatan

Project ini adalah repository pribadi untuk development dan testing environment.

<!-- WATERMARK -->

<img src="https://img.shields.io/badge/Made%20with%20%F0%9F%92%A7%20by-Personal%20Project-blue?style=flat-square" alt="Made with love"/>

**Docker Development Environment** © 2026  
*Personal Development Setup*

---

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Docker Compose](https://img.shields.io/badge/Docker%20Compose-2496ED?style=flat&logo=docker&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat&logo=php&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat&logo=nginx&logoColor=white)
![License MIT](https://img.shields.io/badge/License-MIT-green?style=flat)

**Last Updated**: May 6, 2026 | **Version**: v2.0.0-alpha

<!-- END WATERMARK -->

</div>  
