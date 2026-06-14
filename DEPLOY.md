# Deploy runbook — Regina Caeli Creations

The site is a zero-build static site at the **repo root**. Three steps: push to
GitHub → deploy to Vercel → point the Strato domain at Vercel.

---

## 1. Push to GitHub

The code is already committed locally on branch `main`. To publish it:

```bash
# Authenticate once (opens a browser):
gh auth login

# Create the repo under your account and push in one go:
cd "/Users/jintojose/Tech_Projects/Regina Caeli Bakes"
gh repo create ReginaCaeliCreations --public --source=. --remote=origin --push
```

If you already have the repo **WebApp-Annus-cakes.app** on GitHub and want to
rename + reuse it instead of creating a new one:

```bash
gh repo rename ReginaCaeliCreations --repo jintomjose/WebApp-Annus-cakes.app
git remote add origin https://github.com/jintomjose/ReginaCaeliCreations.git
git push -u origin main
```

> Final repo URL: `https://github.com/jintomjose/ReginaCaeliCreations`

---

## 2. Deploy to Vercel

1. Go to **vercel.com → Add New → Project** and import the
   `ReginaCaeliCreations` GitHub repo.
2. Leave **Root Directory = `./`** (the site is at the repo root).
   Framework preset: **Other**. No build command — it's a static site.
3. Click **Deploy**. You'll get a live URL like
   `regina-caeli-creations.vercel.app`.

Every future `git push` to `main` auto-deploys.

---

## 3. Connect the Strato domain `reginacaelicreations.com`

### a) Add the domain in Vercel
Vercel → your project → **Settings → Domains** → add
`reginacaelicreations.com` **and** `www.reginacaelicreations.com`.
Vercel will then show you the exact DNS records to create. They are normally:

| Type  | Name / Host | Value                  |
|-------|-------------|------------------------|
| A     | `@` (root)  | `76.76.21.21`          |
| CNAME | `www`       | `cname.vercel-dns.com` |

(Use whatever Vercel shows if it differs — those are authoritative.)

### b) Set the records at Strato
1. Log in at **strato.com** → **Domains** → select `reginacaelicreations.com`
   → **DNS settings / DNS-Verwaltung**.
2. **A record** for the root domain:
   - Host/Name: `@` (or leave blank — the root)
   - Value/Points to: `76.76.21.21`
3. **CNAME record** for www:
   - Host/Name: `www`
   - Value/Target: `cname.vercel-dns.com`
4. If Strato auto-created default A records (e.g. an 81.169.x.x "parking"
   address) or a `www` redirect, **delete/replace those** so they don't
   conflict with the records above.
5. Save.

> Strato sometimes disables custom A/CNAME records while a "website package"
> or domain parking is active on the domain — if the DNS fields are greyed
> out, turn off parking / "Strato website" for this domain first.

### c) Wait & verify
DNS propagation takes anywhere from a few minutes to a couple of hours.
Vercel's Domains page shows a green check when it's verified, and it
provisions the HTTPS certificate automatically. Then
`https://reginacaelicreations.com` is live.

Check propagation:
```bash
dig reginacaelicreations.com +short
dig www.reginacaelicreations.com +short
```
