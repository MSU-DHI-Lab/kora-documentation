---
title: Updating your Kora Installation
---

# Updating your Kora Installation

Updating Kora keeps your site secure and gives you bug fixes and new features. You do not need to be a server expert, but you should set aside a short maintenance window and follow the steps in order.

## Before you start

1. **Check compatibility.** Confirm your server still meets the current [System Requirements](../getting-started/system_requirements.md), especially your PHP version and required extensions.
2. **Back up everything.** Save a copy of the database and the whole `kora` folder (be sure `.env` and `storage/` are included). In cPanel, use the built‑in backups; over SSH you can use `mysqldump` plus `tar`.
3. **Plan a short downtime.** Let users know the site may be unavailable for a few minutes.
4. **Read the release notes.** Each release explains what changed and if any special steps are needed.

## Choose your update method

Pick the path that matches how you installed Kora. If you installed with Git, use Method A. If you uploaded a zip or used cPanel/File Manager, use Method B.

### Method A: Update with Git (for Git installs)

1. SSH into your server and go to the Kora install directory (commonly `/var/www/kora` or `~/kora`).
2. Put the site in maintenance mode:
   ```bash
   php artisan down
   ```
3. Pull the latest tagged release (replace `vX.Y.Z` with the version you want):
   ```bash
   git fetch --tags
   git checkout vX.Y.Z
   ```
4. Install PHP dependencies and optimize:
   ```bash
   composer install --no-dev --optimize-autoloader
   php artisan migrate --force
   php artisan config:cache
   php artisan route:cache
   php artisan view:cache
   ```
5. If you previously customized front-end assets with npm, rebuild them now. If not, skip to the next step.
   ```bash
   npm install
   npm run prod
   ```
6. Bring the site back online:
   ```bash
   php artisan up
   ```

### Method B: Update from a zipped release (cPanel/File Manager)

1. Download the latest release zip from the official Kora GitHub releases page.
2. In cPanel (or your host’s file manager), upload the zip to a temporary folder (e.g., `kora_update/`) outside your live site.
3. Extract the zip. You should see a `kora` folder with the application files inside.
4. Copy your existing `.env` file and `storage/` directory from the live site into the new extracted folder so configuration and uploads are preserved.
5. Put the live site into maintenance mode:
   ```bash
   php artisan down
   ```
6. Replace the live application files with the new ones:
   - **cPanel File Manager:** rename the current `kora` directory to `kora_old`, move the new `kora` folder into place, then rename it to `kora`.
   - **SSH:** move the new files over the old directory, making sure `.env` and `storage/` stay in place.
7. From inside the new `kora` directory, run:
   ```bash
   composer install --no-dev --optimize-autoloader
   php artisan migrate --force
   php artisan config:cache
   php artisan route:cache
   php artisan view:cache
   ```
   If you do not have SSH, ask your host to run these commands for you because they are required to complete the update.
8. Turn maintenance mode off:
   ```bash
   php artisan up
   ```
9. Once you verify the site, delete the old `kora_old` directory to recover space.

## After the update

1. **Smoke test:** Log in, load the dashboard, view a project, create a test record, and run a search.
2. **Check logs:** Review `storage/logs/laravel.log` for any errors.
3. **Re-enable scheduled tasks:** If you paused cron jobs or queue workers, start them again.
4. **Back up again:** Take a fresh backup now that the update is complete.

## Troubleshooting tips

- If `composer install` fails, confirm PHP memory limit is sufficient and required extensions are enabled.
- If migrations fail, restore your database backup, resolve the error noted in the console, and rerun `php artisan migrate --force`.
- If pages serve cached errors, clear caches with `php artisan config:clear && php artisan cache:clear`.

Keeping a simple changelog of versions and dates applied at your institution will make future updates faster and safer.
