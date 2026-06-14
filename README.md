# Bitweb Pool UI

A standalone lightweight web interface with PWA support for [MiningCore Fork](https://github.com/bitweb-project/miningcore) pools, built and maintained by [Bitweb Core](https://bitwebcore.net).

---

## Features

- Real-time pool stats via WebSocket push
- Blocks table with status badges (confirmed / pending / orphaned)
- My Miner dashboard — balance, workers, payments, payout settings
- Command generator for CPU (cpuminer-opt) and GPU (OpenCL / CUDA)
- Interactive API documentation page
- 14 UI languages: DE, EN, ES, FR, IT, JA, KO, PL, PT, RO, RU, TR, UK, ZH
- Light / Dark / Auto theme
- PWA — installable, offline-ready service worker
- Zero dependencies at runtime — vanilla JS, Bootstrap 5 bundled

---

## Deploy to Cloudflare Pages

### 1. Fork or clone this repository

```bash
git clone https://github.com/bitweb-project/miningcore-ui.git
```

### 2. Connect to Cloudflare Pages

1. Open [Cloudflare Dashboard](https://dash.cloudflare.com/) → **Workers & Pages**
2. Click **Create Application** → **Continue with Github** → **Chose project**
3. Authorize GitHub and select this repository
4. Set the **build configuration**:

| Setting | Value |
|---|---|
| Framework preset | None |
| Build command | *(leave empty)* |
| Build output directory | `website` |

5. Click **Save and Deploy**

### 3. Connect a custom domain

In your Pages project → **Custom domains** → **Set up a custom domain** → enter your domain → follow the DNS instructions.

---

## Rebranding / Self-hosting

If you want to run this UI against your own MiningCore API instead of falling back to the Bitweb pool, replace all hardcoded references to `pool-api.bitwebcore.net` with your own API hostname.

Locations to update:

| File | Line | What |
|---|---|---|
| `website/assets/js/pool.js` | ~22 | Default API base URL (fallback when nothing is saved in localStorage) |
| `website/assets/js/pool.js` | ~1965 | Placeholder text in the connection settings input |
| `website/assets/js/docs.js` | ~11 | Default API base URL for the API docs page |
| `website/assets/js/docs.js` | ~94 | WebSocket fallback URL |
| `website/assets/js/docs.js` | ~672 | Example WebSocket URL in the docs code snippet |

If you leave these as-is, users who haven't configured a custom API URL will connect to the Bitweb pool API by default.

---

## Project structure

```
website/
├── index.html                  # Main SPA shell
├── api.html                    # API documentation page
├── manifest.json               # PWA manifest
├── sw.js                       # Service worker
├── _headers                    # Cloudflare Pages HTTP headers (CSP, caching)
├── wrangler.toml               # Cloudflare deployment config
└── assets/
    ├── css/
    │   ├── pool.css            # Custom styles
    │   └── bootstrap.min.css
    ├── js/
    │   ├── pool.js             # Main application logic
    │   ├── multilangpool.js    # All UI translations (14 languages)
    │   ├── docs.js             # API docs page logic
    │   ├── theme.js            # Theme switcher
    │   └── bootstrap.bundle.min.js
    ├── images/
    └── webfonts/
```

---

## License

MIT — see [LICENSE](LICENSE)
