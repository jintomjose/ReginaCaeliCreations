# Deploy runbook — Regina Caeli Creations

The site is a zero-build static site at the **repo root**. Three steps: push to
GitHub → deploy to Vercel → point the Strato domain at Vercel.

Status:
- [x] **1. Pushed to GitHub** — https://github.com/jintomjose/ReginaCaeliCreations
- [x] **2. Deployed to Vercel** — https://regina-caeli-creations.vercel.app
      (project `regina-caeli-creations`, GitHub-linked → every push auto-deploys)
- [x] **3. Strato DNS connected** — https://reginacaelicreations.com is **live** with HTTPS
- [x] **4. Vercel Web Analytics enabled** — script in `index.html`, toggle enabled in dashboard

---

## 1. Push to GitHub — DONE

Code is on `main` at https://github.com/jintomjose/ReginaCaeliCreations.
To publish future changes, just commit and push:

```bash
cd "/Users/jintojose/Tech_Projects/Regina Caeli Bakes"
git add -A && git commit -m "your message" && git push
```

Vercel rebuilds and redeploys automatically on every push to `main`.

---

## 2. Deploy to Vercel — DONE

- Project: **regina-caeli-creations** (team: Notio Spiritus)
- Linked to the GitHub repo, so pushes auto-deploy.
- Live preview URL: **https://regina-caeli-creations.vercel.app**
- The custom domains `reginacaelicreations.com` and `www.reginacaelicreations.com`
  are already **added to the project** in Vercel — they go live the moment the
  Strato DNS records below resolve. Vercel issues the HTTPS certificate
  automatically.

---

## 3. Connect the Strato domain `reginacaelicreations.com` — DONE

These records are set at Strato and resolving; the site is live at
https://reginacaelicreations.com with HTTPS (www also works). For reference,
the records added were:

| Type  | Host / Name | Value / Points to      |
|-------|-------------|------------------------|
| A     | `@` (root)  | `76.76.21.21`          |
| CNAME | `www`       | `cname.vercel-dns.com` |

### Steps at Strato
1. Log in at **strato.com** → **Domains / Domainverwaltung** → select
   `reginacaelicreations.com`.
2. Open **DNS settings** (German: *DNS-Verwaltung* / *DNS-Einstellungen*).
   If asked, choose **"use your own DNS settings"** (*eigene DNS-Einstellungen
   verwenden*).
3. **Edit/replace the root A record:**
   - Host/Name: `@` (or blank — the root domain)
   - Type: `A`
   - Value: `76.76.21.21`
4. **Add a CNAME for www:**
   - Host/Name: `www`
   - Type: `CNAME`
   - Value: `cname.vercel-dns.com`
5. **Remove conflicts:** delete any default Strato A record (e.g. an
   `81.169.x.x` parking address) and any existing `www` redirect, so they don't
   fight the records above.
6. Save.

> If the DNS fields are greyed out, a Strato "website package" / domain parking
> is active on this domain — turn that off for `reginacaelicreations.com` first,
> then the DNS fields become editable.

### Verify
DNS propagation takes minutes to a couple of hours. Check with:

```bash
dig reginacaelicreations.com +short        # should return 76.76.21.21
dig www.reginacaelicreations.com +short     # should return cname.vercel-dns.com
```

When it resolves, Vercel's **Settings → Domains** shows a green check, issues
HTTPS, and **https://reginacaelicreations.com** is live (with `www` redirecting
to the root).

---

## 4. Vercel Web Analytics — DONE

Privacy-friendly, cookieless visitor analytics is enabled.

- The tracking script is in `index.html` (just before `</body>`):
  ```html
  <script defer src="/_vercel/insights/script.js"></script>
  ```
- Web Analytics is toggled **on** in Vercel → project → **Analytics**.
- View traffic anytime in the **Analytics** tab. Data comes from real visitors
  (your own visits may be filtered) and first numbers can take a few minutes.
- No cookie banner needed — it doesn't use cookies or collect personal data.
