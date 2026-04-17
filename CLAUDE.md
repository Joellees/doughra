# Doughra — Project Instructions

## Live URL
https://doughra.vercel.app

## What This Is
Single-page marketing + menu site for Doughra, a Dubai-based Arab micro bakery. Static HTML/CSS/JS — no framework, no build step.

## Stack
- **Frontend**: Single `index.html` (all CSS + JS inline)
- **Deploy**: Vercel (static)
- **Backend**: None yet — Formspree handles workshop interest form. When a backend is needed, use Railway + `railway.toml`.
- **Mobile app**: Expo (React Native) — see `../doughra-app/`

## Design Principles
- Dark background (`#0A0A0A`), gold accent (`#C9A96E`), warm white text
- Fonts: Cormorant Garamond (headlines) + Inter (body)
- No clutter. No stock photos. CSS/SVG-generated placeholders only.
- Mobile-first, fully responsive (375 / 768 / 1280px breakpoints)

## Key Interactions
- **WhatsApp order composer**: Cart state in `window.cart` JS object. `buildWhatsAppURL()` encodes all selected items into a `wa.me` link.
- **Workshop form**: POSTs to Formspree. Replace `XXXXXXXX` in the action URL with a real Formspree form ID.
- **Google Maps**: Basic iframe embed, no API key required.

## WhatsApp Number
Placeholder: `+971500000000` — replace in `buildWhatsAppURL()` and the Find Us section.

## Instagram Handle
Placeholder: `@doughra.ae`

## Deployment
```bash
vercel --cwd doughra   # deploy
vercel --prod          # promote to production
```

## Railway (future backend)
Add `railway.toml` to the backend service folder when introducing a server. Connect to Railway project via `railway link`.

## Commits
Commit after each section is added or changed. Use conventional commit messages.
