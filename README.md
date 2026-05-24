# Metaballo

> *μεταβάλλω* — to change, to turn about, to transform.

A static website for **Metaballo**, a high-end Greek-Mediterranean fire kitchen, cocktail bar, and late-night club concept in Camps Bay, Cape Town. The design philosophy mirrors the brand: raw materials — flame, spirit, typography — refined into something considered.

Live: **[metaballo-9d0db.web.app](https://metaballo-9d0db.web.app)**  
Repo: **[github.com/StevenChristie/Metaballo](https://github.com/StevenChristie/Metaballo.git)**

---

## Pages

| File | Route | Description |
|---|---|---|
| `index.html` | `/` | Main landing page — hero, philosophy, heritage, menu, bar, lounge, visit |
| `club.html` | `/club.html` | The Club — vinyl, jazz & late-night programme |
| `reservations.html` | `/reservations.html` | Table reservation form |
| `404.html` | `*` | Custom branded 404 page |

---

## Project structure

```
Metaballo/
├── index.html            # Main restaurant page
├── club.html             # The Club (speakeasy / late-night)
├── reservations.html     # Reservation form
├── 404.html              # Custom 404
│
├── styles.css            # Main stylesheet (index.html)
├── club.css              # Club page styles
├── reservations.css      # Reservations page styles
│
├── assets/
│   ├── hero.avif                  # Main hero image (AVIF for performance)
│   ├── heritage.jpg               # Heritage section
│   ├── lounge.jpg                 # Lounge / reservations aside
│   ├── speakeasy.jpg              # Lounge teaser section (index)
│   ├── cocktailmetamorphosis.jpg  # Bar — Metamorphosis cocktail
│   ├── cocktailcatharsis.jpg      # Bar — Catharsis cocktail
│   ├── cocktailapotheosis.jpg     # Bar — Apotheosis cocktail
│   ├── club-bar.jpg               # Club hero background
│   ├── club.jpg                   # Club photography
│   ├── club1.jpg                  # Club photography
│   ├── house.jpg                  # Club photography
│   ├── house1.jpg                 # Club photography
│   └── roof.jpg                   # Club wide bar shot
│
├── firebase.json                  # Firebase Hosting config
├── .firebaserc                    # Firebase project alias
└── .github/
    └── workflows/
        └── deploy.yml             # CI/CD — auto-deploy on push to main
```

---

## Design system

### Colour tokens

| Token | Hex | Usage |
|---|---|---|
| `--bg` | `#0d0807` | Page background (restaurant) |
| `--bg-soft` | `#140c0a` | Elevated surfaces, menu, footer |
| `--cream` | `#ead8c6` | Primary text |
| `--cream-dim` | `rgba(234,216,198,0.72)` | Body text, secondary |
| `--cream-faint` | `rgba(234,216,198,0.45)` | Tertiary, captions |
| `--peach` | `#f1b89a` | Accent — CTAs, labels, prices |
| `--peach-hover` | `#f5c6ac` | Accent hover state |
| `--rule` | `rgba(234,216,198,0.18)` | Dividers and borders |

The Club page uses a separate dark red palette (`--red: #bf2318`) to distinguish the space from the restaurant.

### Typography

| Role | Font | Usage |
|---|---|---|
| Display | Cormorant Garamond | Titles, pull quotes, menu items, italic body |
| UI | Inter | Navigation, labels, buttons, captions |

Loaded via Google Fonts. Weights: Cormorant 400/500/600 (regular + italic), Inter 300/400/500/600.

### Breakpoints

| Breakpoint | Target |
|---|---|
| `≥ 1700px` | Large monitors — wider content cap |
| `≤ 1180px` | Laptop / small desktop |
| `≤ 1024px` | Narrow desktop |
| `≤ 900px` | Tablet — mobile nav, single-column grids |
| `≤ 560px` | Phones |
| `≤ 360px` | Small phones |

---

## Running locally

No build step. Open directly in a browser or use VS Code's **Live Server** extension for hot-reload.

```bash
# If you have the Live Server CLI
npx live-server .
```

Or just open `index.html` in your browser.

---

## Deployment

Hosted on **Firebase Hosting**. Deployments are automatic via GitHub Actions on every push to `main`.

```bash
# Manual deploy
firebase deploy
```

The workflow lives at `.github/workflows/deploy.yml` and uses a `FIREBASE_TOKEN` secret stored in the repository settings.

**To set up the token:**
```bash
firebase login:ci   # prints a token
# Add the token to GitHub → Settings → Secrets → FIREBASE_TOKEN
```

---

## Key interactions

- **Mobile nav** — full-screen overlay with staggered link entrance, closes on link click, Escape key, or resize above 900px
- **Scroll reveals** — IntersectionObserver fades elements in as they enter the viewport; respects `prefers-reduced-motion`
- **Active nav highlight** — underline tracks the current section as you scroll
- **Lounge transition** — clicking "Enter" on the lounge section triggers a zoom + fade before navigating to `club.html`; the club page fades in to match
- **EQ animation** — animated equaliser bars on the club hero; paused if reduced motion is preferred
- **Newsletter form** — client-side only (no backend); shows a confirmation message on submit
- **Reservation form** — client-side only; shows a Greek confirmation screen on submit

---

## Notes

- All images use `loading="lazy"` except the above-fold hero (which loads eagerly for LCP)
- The hero uses `.avif` format for optimal compression
- No frameworks, no bundler — plain HTML, CSS, and vanilla JS
- The `404.html` is served automatically by Firebase Hosting on unmatched routes

