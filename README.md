# Monovus Solutions — monovus.solutions

Public website for [monovus.solutions](https://monovus.solutions) — the Monovus consulting brand.

## Stack

- **Framework:** [Astro](https://astro.build/) 4.x with TypeScript
- **Styling:** [Tailwind CSS](https://tailwindcss.com/) 3.x
- **Deployment:** [Cloudflare Pages](https://pages.cloudflare.com/)
- **Forms:** [Formspree](https://formspree.io/)

## Pages

| Route | Description |
|-------|-------------|
| `/` | Home — hero, services overview, CTA |
| `/services` | Service lines — consulting, AI, infrastructure |
| `/about` | Alex Shaw bio, Monovus origin story |
| `/contact` | Contact form + email info |
| `/legal/privacy` | Privacy policy |
| `/legal/terms` | Terms of service |

## Brand

- **Primary Background:** Obsidian Blue `#0A141F`
- **Accent:** Electric Cyan `#00F2F5`
- **Fonts:** Inter (sans), JetBrains Mono (mono)
- **Tagline:** Infrastructure. Intelligence. Innovation.

## Development

```bash
# Install dependencies
npm install

# Start dev server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## Deployment

This site deploys automatically to Cloudflare Pages on push to `main`.

**Cloudflare Pages settings:**
- Framework preset: Astro
- Build command: `npm run build`
- Build output: `dist`
- Node version: 18

## Contact

- **Email:** hello@monovus.solutions
- **Status:** [status.monovus.solutions](https://status.monovus.solutions)
