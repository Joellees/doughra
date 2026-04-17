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
### Palette — "Refined Ivory"
Warm paper background + deep warm brown + caramel accent. Blue is reserved for focus rings.
- **Ink (primary, deepest)** `--ink` `#1A1310`. Shades: `--ink-soft` `#2E221B`, `--brown` `#5A4637`, `--brown-mid` `#8B7764`, `--brown-soft` `#B2A393`, `--brown-fog` `#D6CCBC`. Used for: wordmark, headings, body text, section labels, prices, dividers, icons, primary CTA bg.
- **Ivory / Bone (secondary, surfaces)** `--ivory-lite` `#FAF7F0`, `--ivory` `#F5F1E8` (body bg), `--bone` `#EDE6D6` (cards, footer), `--stone` `#E0D6C2` (product tile base, deeper surfaces).
- **Cognac (accent, rare)** `--cognac` `#B8865E`, `--cognac-deep` `#9A6D47`. Used for: the brand dot/bullet in the wordmark, rare highlights. **Never** for body text.
- **Blue (focus only)** `--blue` `#A9C4CE`, `--blue-soft` `#DDE6E9`. Keyboard focus rings. Nothing else.
- Legacy CSS aliases (`--bg`, `--gold`, `--text`, `--border`, `--butter*`, `--espresso`) re-map to the new palette inside `:root`. `--gold` resolves to `--brown`. `--butter-lite` resolves to `--ivory`. Component code didn't need rewriting.

### Typography
- **Display / wordmark**: **Instrument Serif** (Google Fonts, free) — elegant editorial serif, italic preferred for the wordmark (the looped `g` and swashed `r` are signature).
- **Body / UI**: **Inter Tight** (Google Fonts, free) — modern sans, tighter tracking than Inter.
- The hero wordmark is Instrument Serif *italic* at weight 400, with a subtle ink → brown vertical gradient via `background-clip: text`.
- Body text is Inter Tight 400.

### Logo / Wordmark
The brand mark is **a small cognac dot** (`::before` pseudo-element) followed by **"Doughra" in Instrument Serif italic**. The dot is the one recognizable graphic cue across nav, hero (not used), and footer.

### Minimalism
No background patterns. No film-grain overlay. No radial glow. No drop shadows on the hero. The only "texture" is typography, letterspacing, and the ivory paper background.

### Layout
CSS/SVG-generated product tiles only — no stock photos. Mobile-first, responsive (375 / 768 / 1280px breakpoints).

## Key Interactions
- **WhatsApp order composer**: Cart state in `window.cart` JS object. `buildWhatsAppURL()` encodes all selected items into a `wa.me` link.
- **Workshop form**: POSTs to Formspree. Replace `XXXXXXXX` in the action URL with a real Formspree form ID.
- **Google Maps**: Basic iframe embed, no API key required.

## Payment Flow (WhatsApp payment links)
**No on-site checkout.** The `#pay` section is an explainer only — a 3-step card explaining how payment works, with a CTA to start an order on WhatsApp.

1. Customer places an order via WhatsApp.
2. Doughra replies in the chat confirming items + total.
3. Doughra pastes a **payment link** into the chat. Customer taps it, pays (Apple Pay / Google Pay / card) on the hosted page, and we get a webhook + receipt.

To enable payment links, pick a processor and generate links from the merchant dashboard (or via API):
- **Tap Payments** — UAE native, great Apple Pay/mada support. Use "Pay by Link" from the Tap dashboard, or the `/charges` API to create a hosted redirect URL.
- **Stripe Payment Links** — one-off or reusable links via dashboard; supports Apple Pay out of the box.
- **PayMob** — UAE/Egypt, similar "Payment Link" feature.

There is no payment form on the site and no JS handler for payments. If a card-on-site flow is ever needed, add a serverless function (e.g. `/api/create-charge`) on Vercel and wire it to the chosen processor.

## WhatsApp Number
Placeholder: `+971500000000` — replace in `buildWhatsAppURL()`, the Find Us section, AND the Pay-section CTA (`.btn-whatsapp` in the `#pay` section).

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
