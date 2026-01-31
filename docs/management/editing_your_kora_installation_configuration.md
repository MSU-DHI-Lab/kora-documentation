---
title: Editing your Kora Installation Configuration
---

# Editing your Kora Installation Configuration

The configuration file controls core settings for your Kora site. You can change the site address, email details, upload limits, and service keys here. You do not need deep server knowledge, but take a quick backup before you start.

## Before you change settings

1. Sign in as an installation administrator.
2. Let teammates know you will save changes. It only takes a few minutes, but it is best if no one else is editing.
3. Save a copy of your current `.env` file if you can. In cPanel you can download it with File Manager. Over SSH you can run `cp .env .env.backup`.

## Open the configuration page

1. Sign in to Kora.
2. Open the main menu in the top right.
3. Choose Management, then choose Kora Configuration File. A page opens with text boxes for each setting.

## Update common settings

- **Site URL (APP_URL)**  
  Type the full web address for your Kora site. Use `https://` if you have a certificate. Example `https://kora.example.org`.

- **Mail settings (MAIL_HOST, MAIL_FROM_ADDRESS, MAIL_FROM_NAME, MAIL_USER, MAIL_PASSWORD)**  
  Fill these only if your installation still uses an SMTP server. Use the host name, the address you want to appear in messages, and the login details from your email provider. If your institution has disabled email, leave these as they are.

- **reCAPTCHA keys**  
  Paste the public and private keys you created in the Google reCAPTCHA console. Make sure the keys match the domain you set in APP_URL.

- **Upload size**  
  If your host allows it, adjust the upload size to match your needs. Set the PHP limits in your hosting control panel (`upload_max_filesize` and `post_max_size`) and keep these values in sync with the fields on this page. Ask your host if you are unsure.

- **API tokens**  
  Rotate tokens in the Management area if one is ever exposed. Update any external tools that rely on those tokens after you rotate them.

## Save and apply

1. When you finish editing, click Update Configuration File at the bottom of the page.
2. Wait for the success message. If you see an error, check for typos and try again.
3. If you changed the site URL, sign out and sign back in to confirm it works.

## If something goes wrong

- If the site stops loading after a change, restore the `.env` backup you made and try again.
- If email stops working, put the previous mail values back and send a single password reset to test.
- If you see a cache warning, clear it with `php artisan config:clear` over SSH, then reload the site.

Keep a short note of what you changed and when. It will help you and other administrators later.
