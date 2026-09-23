# Becky the Bat — status (gh-pages)

**Live product branch:** `gh-pages` → [beckythebat.com](https://beckythebat.com)  
**Repo:** [Siddharth09/Pinkybat](https://github.com/Siddharth09/Pinkybat)  
**Last security fix pass:** 2026-09-17 (Australia/Sydney)

## Ops for Sid (cannot finish via git alone)

1. **Enforce HTTPS on GitHub Pages** for the custom domain `beckythebat.com`:
   - GitHub repo → **Settings** → **Pages** → enable **Enforce HTTPS**.
   - Confirm `http://beckythebat.com/` redirects to `https://` (today HTTP can still serve 200 without upgrade).
   - HSTS is only meaningful after HTTPS is enforced end-to-end on the custom domain.
2. Optional: re-check response headers after enforce (expect redirect on HTTP; CSP meta tags are already in HTML as a Pages-friendly fallback).

## Shipped in `fix/becky-payment-integrity` (2026-09-17)

| Priority | Change |
|----------|--------|
| **P0** | Disabled web Stripe buy + forgeable `?stripe_success` / `session_id` credit in `play.html`. Native IAP (`NativePurchases`) unchanged. Web buy CTA points to App Store / in-run hearts. |
| **P0** | `recoverPendingTransaction` only credits on native platforms; web clears pending without granting hearts (pending TX is client-writable). |
| **P1** | `privacy.html` rewritten for web + share + network honesty; Stripe noted as legacy/disabled web path; Apple IAP for app. |
| **P1** | Meta `Content-Security-Policy` + `referrer` on `play.html` / `index.html` / `privacy.html` / `support.html`. Marketing iframe `sandbox` + `referrerpolicy`. |
| **P2** | HUD: `heartProgress` consistently shows banked `/100 to continue`; run hearts stay on `heartScore` during play; `cityTier` shows loop/night instead of always-empty. |
| **Docs** | This `STATUS.md`. `support.html` aligned with disabled web checkout. |

## Explicitly deferred (follow-up)

- **Unify `main` ↔ `gh-pages`:** `main` is still the Capacitor “Pinky Bat” skeleton (`com.pinkbat.game`); live Becky product lives only on `gh-pages`. Full product unify / CI pointing at Becky is a separate migration — not in this PR.
- **Server-side Stripe Checkout Session verify:** needed before any web Payment Link credit path can return. No Becky backend today (Redis-like session store N/A).
- **Server-side IAP receipt validation:** native path still trusts the Capacitor plugin result + local dedup (honor-system local heart bank remains forgeable via DevTools; accepted for cosmetic continue currency until a backend exists).
- **GitHub Pages security headers** beyond meta (HSTS, CSP as HTTP headers): depend on Pages/Enforce HTTPS and platform limits.

## Base SHA before this fix

`gh-pages` tip at audit: `a8b8ce6aaab2cf46d1e36b40bac78760dd92a09c`

## Free SEO / LLM visibility (2026-09-23)

- Added `robots.txt`, `sitemap.xml`, `llms.txt`, `llms-full.txt`
- Canonical + FAQPage JSON-LD + visible FAQ on `index.html`
- AI crawlers explicitly allowed
- Added page-specific descriptions and canonicals to `play.html`, `privacy.html`, and `support.html`; support FAQ schema now mirrors its visible questions
