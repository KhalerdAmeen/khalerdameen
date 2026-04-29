# deploy guide — khalerdameen.com

## stack
- HTML/CSS — no build step needed
- GitHub — version control + Vercel trigger
- Vercel Hobby — free hosting, auto-deploys on push
- Your domain — connected via DNS

---

## step 1 — github repo

1. Go to github.com → New repository
2. Name it: `khalerdameen` (or `personal-site`)
3. Set to **Public** (required for Vercel Hobby free tier)
4. Don't add README (you already have files)

Then in your terminal:
```bash
cd khalerdameen/
git init
git add .
git commit -m "init: personal site"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/khalerdameen.git
git push -u origin main
```

---

## step 2 — vercel

1. Go to vercel.com → Log in with GitHub
2. Click **Add New → Project**
3. Import your `khalerdameen` repo
4. Framework Preset: **Other** (it's plain HTML)
5. Root Directory: `/` (leave default)
6. Build Command: leave **empty**
7. Output Directory: leave **empty** (or set to `.`)
8. Click **Deploy**

Your site is live on a `*.vercel.app` URL in ~30 seconds.

---

## step 3 — connect your domain

In Vercel dashboard → your project → **Settings → Domains**

1. Click **Add Domain**
2. Type your domain: `khalerdameen.com`
3. Vercel gives you DNS records — two options:

### option A — if your domain is on Namecheap / GoDaddy / etc.
Add these records in your registrar's DNS settings:
```
Type: A
Name: @
Value: 76.76.21.21

Type: CNAME
Name: www
Value: cname.vercel-dns.com
```

### option B — transfer DNS to Vercel (easiest long-term)
In Vercel → Domains → set nameservers to:
```
ns1.vercel-dns.com
ns2.vercel-dns.com
```
Then Vercel manages everything automatically.

SSL certificate is auto-provisioned. Usually live within 5 minutes.

---

## step 4 — updating the site later

```bash
# edit index.html or content.md
git add .
git commit -m "update: add routn link"
git push
```
Vercel auto-deploys every push to `main`. No manual steps.

---

## costs
| item | cost |
|---|---|
| Vercel Hobby hosting | $0/mo |
| Custom domain (yr 1) | ~$12/yr |
| SSL certificate | $0 (Vercel provides) |
| **total** | **~$12/yr** |

---

## folder structure reminder
```
khalerdameen/
├── index.html
├── public/
│   └── logo.svg
├── content.md
├── PROMPT.md
└── DEPLOY.md   ← this file
```
