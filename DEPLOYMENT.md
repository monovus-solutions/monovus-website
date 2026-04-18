# Deployment Guide — Monovus Website

## Push to GitHub and Set Up Cloudflare Pages

### Push to GitHub

```bash
cd monovus-website
git init
git add .
git commit -m "Initial commit: Monovus Solutions website"
git remote add origin git@github.com:monovus/monovus-website.git
git branch -M main
git push -u origin main
```

### Set Up Cloudflare Pages

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com/) → Pages
2. Click **Create a project** → **Connect to Git**
3. Select the `monovus/monovus-website` repository
4. Configure build settings:
   - **Framework preset:** Astro
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`
5. Under **Environment variables**, add:
   - `NODE_VERSION` = `18`
6. Click **Save and Deploy**
7. Wait for the first build to complete (should be under 1 minute)
8. Verify the preview URL works (e.g., `monovus-website.pages.dev`)

---

## Configure Custom Domain for Cloudflare Pages

1. In Cloudflare Pages project settings, go to **Custom domains**
2. Click **Set up a custom domain**
3. Enter `monovus.solutions` → Click **Continue**
4. Cloudflare will auto-configure the DNS CNAME record
5. Repeat for `www.monovus.solutions`
6. Wait for DNS propagation (usually instant since domain is on Cloudflare)
7. Verify HTTPS is active on both domains

---

## Create DNS Records for Website

Cloudflare Pages auto-creates these records when you add custom domains.
Verify the following exist in the DNS zone:

| Type  | Name  | Content                          | Proxy |
|-------|-------|----------------------------------|-------|
| CNAME | @     | monovus-website.pages.dev        | ✅    |
| CNAME | www   | monovus-website.pages.dev        | ✅    |

### Verification

```bash
# Verify root domain resolves
dig +short monovus.solutions

# Verify www resolves
dig +short www.monovus.solutions

# Verify HTTPS works
curl -I https://monovus.solutions
curl -I https://www.monovus.solutions
```

---

## Validate Website Deployment

### Checklist

- [ ] `https://monovus.solutions` returns HTTP 200
- [ ] `https://www.monovus.solutions` redirects to or serves the site
- [ ] All pages load correctly:
  - [ ] `/` — Home page with hero, services, CTA
  - [ ] `/services` — Three service cards
  - [ ] `/about` — Philosophy and principles
  - [ ] `/contact` — Contact form renders
  - [ ] `/legal/privacy` — Privacy policy
  - [ ] `/legal/terms` — Terms of service
- [ ] Navigation works on all pages
- [ ] Mobile hamburger menu works
- [ ] Contact form submits (update Formspree form ID first)
- [ ] Favicon displays correctly
- [ ] OG meta tags present (check with https://metatags.io/)

### Validation Commands

```bash
# Test all pages return 200
for path in "" "services" "about" "contact" "legal/privacy" "legal/terms"; do
  status=$(curl -s -o /dev/null -w "%{http_code}" "https://monovus.solutions/$path")
  echo "$path: $status"
done

# Check TLS
echo | openssl s_client -connect monovus.solutions:443 2>/dev/null | grep "TLSv1.3"

# Check response headers
curl -I https://monovus.solutions
```

### Before Going Live

1. **Update Formspree form ID:** Replace `{form_id}` in
   `src/components/ContactForm.astro` with your actual Formspree form ID
   - Sign up at https://formspree.io/
   - Create a new form
   - Copy the form ID
2. **Test contact form submission** end-to-end
3. **Run Lighthouse audit** — target 90+ performance score
