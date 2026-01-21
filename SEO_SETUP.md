# SEO & Hostinger Setup – Jeskin Media Hub

## Before you go live

### 1. Replace the domain placeholder

Replace **`YOUR_DOMAIN.com`** with your real domain in:

| File | Find | Replace with (e.g. jeskinmediahub.com) |
|------|------|----------------------------------------|
| `sitemap.xml` | `YOUR_DOMAIN.com` | your domain |
| `robots.txt` | `YOUR_DOMAIN.com` | your domain |
| `index.html` | `YOUR_DOMAIN.com` | your domain |
| `about.html` | `YOUR_DOMAIN.com` | your domain |
| `contact.html` | `YOUR_DOMAIN.com` | your domain |
| `products.html` | `YOUR_DOMAIN.com` | your domain |

Use **Find and Replace** in your editor:  
Find: `YOUR_DOMAIN.com` → Replace: `jeskinmediahub.com` (or your actual domain).

---

### 2. Submit your sitemap

- **Google**  
  - [Google Search Console](https://search.google.com/search-console)  
  - Add property → your domain  
  - **Sitemaps** → Add: `https://www.yourdomain.com/sitemap.xml`

- **Bing**  
  - [Bing Webmaster Tools](https://www.bing.com/webmasters)  
  - Add site → your domain  
  - **Sitemaps** → Submit: `https://www.yourdomain.com/sitemap.xml`

---

### 3. Clean URLs (no .html) and .htaccess

The `.htaccess` file is already set up so that:

- `/` → `index.html`
- `/about` → `about.html`
- `/products` → `products.html`
- `/contact` → `contact.html`

Old URLs like `/about.html` are **301 redirected** to `/about`.  
All internal links use extensionless URLs (`/`, `/about`, `/products`, `/contact`).

Hostinger uses Apache with `mod_rewrite`; this should work by default.  
If clean URLs don’t work, in the Hostinger **.htaccess** editor confirm that the contents of your `.htaccess` are present and that **RewriteEngine** is not disabled elsewhere.

---

### 4. HTTPS on Hostinger

1. In Hostinger: **SSL** → enable a free SSL (e.g. Let’s Encrypt) for your domain.
2. In `.htaccess`, uncomment the **“Force HTTPS”** block:

```apache
# Uncomment these two lines:
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

---

### 5. Optional: favicon

If you have a `favicon.ico`, put it in the site root and add in every `<head>`:

```html
<link rel="icon" href="/favicon.ico" type="image/x-icon" />
```

---

### 6. After going live

- Test clean URLs: `/`, `/about`, `/products`, `/contact`
- Test that `https://www.yourdomain.com/sitemap.xml` and `https://www.yourdomain.com/robots.txt` load
- In Search Console: **URL Inspection** for your homepage and main pages to request indexing

---

## Files added or changed

| File | Purpose |
|------|---------|
| `sitemap.xml` | Sitemap for Google & Bing |
| `robots.txt` | Tells crawlers what to index; points to sitemap |
| `.htaccess` | Clean URLs, 301 from .html, security headers, optional HTTPS |
| `index.html` | SEO meta, Open Graph, Twitter Card, JSON-LD (LocalBusiness), canonical, internal links |
| `about.html` | Meta, OG, canonical, internal links |
| `contact.html` | Meta, OG, canonical, internal links |
| `products.html` | Meta, OG, canonical, internal links; fixed 2 broken `img` tags |
