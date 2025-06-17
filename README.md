[![Laravel Web Installer](https://github.com/rashidlaasri/LaravelInstaller/assets/36804104/5fea5ade-7c97-43bb-b6a9-89cd8d2a0bdf)](https://laravel-installer.com)



# Laravel Installer - Local Installation Guide

This guide explains how to install and integrate a locally stored Laravel Installer package within your Laravel application.

---

## 1. Clone the Package Locally

Place the installer package in your Laravel project at:

```bash
packages/laravel-installer/
```

---

## 2. Configure Composer Path Repository

In your main Laravel app’s `composer.json`, add:

```json
"repositories": [
  {
    "type": "path",
    "url": "./packages/laravel-installer",
    "options": {
      "symlink": false
    }
  }
]
```

---

## 3. Include Custom Helper Functions

Inside `LaravelInstallerServiceProvider::register()` in your package:

```php
require_once __DIR__ . '/../Helpers/functions.php';
```

---

## 4. Set Directory Permissions (Required by Installer UI)

Run the following in your Laravel project root:

```bash
chmod -R 777 storage
chmod -R 777 bootstrap/cache
```

---

## 5. Auto-Publish Assets After Install

In the root `composer.json`, add this to the `scripts` section:

```json
"scripts": {
  "post-install-cmd": [
    "@php artisan vendor:publish --tag=laravelinstaller --force"
  ]
}
```

---

## 6. Install Dependencies

Run:

```bash
composer install
```

This will install your Laravel app and automatically publish the installer assets.

---

> ✅ You’re now ready to access the installer via `/install` route in your browser!

