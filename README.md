# Ders Programı Oluşturma Sistemi

Laravel 11 tabanlı ders programı oluşturma ve yönetim uygulaması. Okullar için ders çizelgesi, öğretmen ve sınıf yönetimini kolaylaştırır.

🌐 **Canlı Site:** [https://136.altekbilisim.com](https://136.altekbilisim.com)

---

## 🚀 Özellikler

- 📅 **Ders Programı Oluşturma** - Otomatik ders çizelgesi oluşturma
- 👨‍🏫 **Öğretmen Yönetimi** - Öğretmen bilgileri ve ders atamaları
- 🏫 **Sınıf/Teşkilat Yönetimi** - Okul teşkilat yapısı
- 🔐 **Kullanıcı Girişi** - Güvenli authentication sistemi
- 📊 **Dashboard** - Anasayfa ve tüm programları görüntüleme
- ⚙️ **Ayarlar** - Uygulama ayarları

---

## 🛠️ Teknoloji Stack

- **Backend:** Laravel 11 (PHP 8.2+)
- **Frontend:** Blade + TailwindCSS 4
- **Build Tool:** Vite 8
- **Database:** MySQL (production) / SQLite (local)
- **Deploy:** GitHub Actions → FTP

---

## 📦 Kurulum (Local Development)

### Gereksinimler
- PHP 8.2+
- Composer
- Node.js 22+
- NPM

### Adımlar

```bash
# Repo'yu klonla
git clone https://github.com/kaano09/dersprogram-laravel.git
cd dersprogram-laravel

# Composer paketlerini yükle
composer install

# NPM paketlerini yükle
npm install

# .env dosyasını oluştur
cp .env.example .env

# Uygulama anahtarını oluştur
php artisan key:generate

# Veritabanını oluştur (SQLite)
php artisan migrate

# Asset'leri derle
npm run build

# Sunucuyu başlat
php artisan serve
```

Site `http://localhost:8000` adresinde açılacaktır.

---

## 🌍 Production Deploy

Proje, `main` branch'ine her push'ta otomatik olarak FTP üzerinden canlı sunucuya deploy edilir.

### Deploy Yapısı (Shared Hosting)

```
public_html/          → Site root (https://136.altekbilisim.com/)
  ├── index.php       → Laravel'i başlatır
  ├── .htaccess
  └── css, js, img

laravel_app/          → Laravel core (web'den erişilemez)
  ├── app/
  ├── config/
  ├── routes/
  ├── vendor/
  └── .env
```

### GitHub Secrets

Deploy için repo'nun **Settings → Secrets and variables → Actions** kısmında 3 secret olmalı:

| Secret | Değer |
|--------|-------|
| `FTP_SERVER` | FTP sunucu adresi |
| `FTP_USERNAME` | FTP kullanıcı adı |
| `FTP_PASSWORD` | FTP şifresi |

### Deploy Workflow

`.github/workflows/deploy.yml` dosyası şunları otomatik yapar:

1. ✅ PHP 8.2 ve Node.js 22 kurulumu
2. ✅ `composer install` + `npm install && npm run build`
3. ✅ Laravel dosyalarını shared hosting yapısına göre düzenleme
4. ✅ Production `.env` dosyası oluşturma
5. ✅ `php artisan key:generate` ile APP_KEY üretme
6. ✅ FTP ile `public_html/` ve `laravel_app/` klasörlerini gönderme

---

## 📁 Proje Yapısı

```
.
├── app/
│   ├── Http/Controllers/    # Controller'lar (Auth, Page)
│   ├── Models/              # User model
│   └── Providers/
├── bootstrap/
├── config/                  # Laravel konfigürasyon
├── database/
│   ├── migrations/          # DB migration dosyaları
│   ├── factories/
│   └── seeders/
├── public/                  # Public assets (css, js, img)
├── resources/
│   ├── css/                 # TailwindCSS
│   ├── js/                  # JavaScript
│   └── views/               # Blade template'ler
│       ├── auth/login.blade.php
│       ├── layouts/app.blade.php
│       ├── home.blade.php
│       ├── schedule.blade.php
│       ├── teachers.blade.php
│       ├── ayarlar.blade.php
│       └── view-all.blade.php
├── routes/
│   └── web.php              # Web rotaları
├── .github/workflows/
│   └── deploy.yml           # CI/CD deploy config
├── composer.json
├── package.json
└── vite.config.js
```

---

## 🗄️ Veritabanı

### Production (MySQL)
- **Database:** `alt300iliscomtr_136`
- **Connection:** MySQL 127.0.0.1:3306

### Local (SQLite)
- `database/database.sqlite` (otomatik oluşturulur)

### Migration Çalıştırma
```bash
php artisan migrate           # Tabloları oluştur
php artisan migrate:fresh     # Tümünü sıfırla
php artisan migrate:rollback  # Son migration'ı geri al
```

---

## 🔧 Geliştirme Komutları

```bash
# Development sunucusu + queue + vite
composer dev

# Asset izleme (watch mode)
npm run dev

# Asset derleme (production)
npm run build

# Test çalıştırma
php artisan test

# Cache temizleme
php artisan cache:clear
php artisan config:clear
php artisan view:clear
php artisan route:clear
```

---

## 📝 Lisans

Bu proje MIT lisansı ile lisanslanmıştır.

---

## 👨‍💻 Geliştirici

**Kaan Orhan** - [GitHub](https://github.com/kaano09)
