# Regina Caeli Creations

Single-page website for **Regina Caeli Creations** — home-baked, rum-soaked Kerala-style
Christmas plum cakes from The Hague.

- **Product:** Rum-Soaked Christmas Plum Cake · 1 KG · €35
- **Order:** WhatsApp [+31 6 2412 8946](https://wa.me/31624128946)
- **Instagram:** [@reginacaelicreations](https://www.instagram.com/reginacaelicreations)
- **Pickup:** Wateringseveld, Den-Haag Zuid
- **Live site:** https://reginacaelicreations.com

## Tech

A zero-build static site — plain HTML + CSS, no framework. It can be served by any
static host (Vercel, GitHub Pages, Strato web hosting).

```
├── index.html      # the page
├── styles.css      # brand styles (deep green / gold / cream palette)
├── vercel.json     # static hosting config
├── assets/         # logo + cake imagery
└── design-source/  # original brand artwork (not deployed)
```

## Local preview

```bash
python3 -m http.server 8080   # then open http://localhost:8080
```

## Deploy (Vercel)

The site lives at the repo root, so no Root Directory or build command is needed —
Vercel serves it as a static site and auto-deploys on every push to `main`.

Custom domain `reginacaelicreations.com` is configured in Vercel → Settings → Domains,
with DNS pointed from Strato (see [DEPLOY.md](DEPLOY.md)).
