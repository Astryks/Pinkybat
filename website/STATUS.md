# Becky the Bat — status

**Canonical source:** `vicky-the-bat-final` branch, `vicky-the-bat-mobile/source/vicky.html`
**Live web deploy:** `gh-pages` → [beckythebat.com](https://beckythebat.com)
**Native app:** synced from the same source into the Capacitor iOS project
**Repo:** [Astryks/Pinkybat](https://github.com/Astryks/Pinkybat) (moved from Siddharth09/Pinkybat)
**Last reconciliation pass:** 2026-09-28

## Ops for Sid (cannot finish via git alone)

1. **Enforce HTTPS on GitHub Pages** for the custom domain `beckythebat.com`:
   - GitHub repo → **Settings** → **Pages** → enable **Enforce HTTPS**.
   - Confirm `http://beckythebat.com/` redirects to `https://` (today HTTP can still serve 200 without upgrade).
   - HSTS is only meaningful after HTTPS is enforced end-to-end on the custom domain.
2. Archive + upload a new build in Xcode so the in-app review plugin and the other native-relevant fixes below actually ship.

## 2026-09-28 reconciliation

A separate agent session shipped a real security fix and a large SEO/ASO pass directly to `gh-pages`, bypassing the normal source → build → deploy pipeline. Reconciled as follows:

- **Web Stripe checkout: kept enabled**, per Sid's explicit decision — reverted the other session's fix that disabled it (which worked by removing the feature rather than adding server-side verification). The original accepted trade-off stands: no backend to cryptographically verify the Stripe Checkout Session return, acceptable since it only unlocks in-game currency, not a real-money withdrawal. Revisit if server-side Checkout Session verification is ever added (would need a small backend — none exists today).
- **CSP + referrer-policy meta tags**: kept and merged into canonical source (`play.html`'s tag set, which is the most complete — includes `media-src`/`worker-src`/`font-src` for the game specifically). Verified via a full 177-city render sweep served over real HTTP (so the CSP is actually enforced, not just present) that inline scripts/styles still run fine.
- **`index.html` iframe sandbox**: kept, with `allow-top-navigation-by-user-activation` added — the original sandbox list omitted this, which would have silently broken the Stripe redirect from the homepage's fullscreen preview (a real bug that was fixed earlier this project).
- **`cityTier` HUD fix**: kept (`updateCityTierHud()`) — this element was dead code (always rendered `''`) before; now shows `LOOP 2`, `LOOP 3 · NIGHT`, etc. on repeat laps past all 177 destinations.
- **`heartProgress` HUD change**: **not** adopted. The other session changed it to always show banked-hearts-toward-continue (`X/100 to continue`); we kept the original design instead, where it shows this run's `heartCount` out of 300 — driving Becky's cosmetic pink color shift, a feature specifically built and explained earlier in this project. Both are valid designs; this one was already deliberate.
- **In-app review (App Store ratings prompt)**: the other session only shipped a no-op web helper (correctly gated to native + new-best + rate-limited, since `@capacitor-community/in-app-review` was never actually added to the iOS project). We adopted the same trigger logic **and installed the real plugin** (`@capacitor-community/in-app-review@8.0.0`, synced into the Xcode project's SPM package). This now needs a fresh archive/upload to actually reach the App Store binary — see Ops above.
- **`privacy.html` / `support.html`**: kept the improved structure (network-use disclosure, sharing-score section, more detail on what's stored locally) but corrected the purchases sections back to accurately describe the restored, working Stripe web checkout.
- **SEO/ASO additions**: kept as-is (see below) — none of this conflicted with the Stripe decision.

## Free SEO / LLM visibility

- `robots.txt`, `sitemap.xml`, `llms.txt`, `llms-full.txt` — AI crawlers (GPTBot, ClaudeBot, PerplexityBot, etc.) explicitly allowed
- Canonical links + FAQPage JSON-LD + visible FAQ on `index.html`, `support.html`
- Page-specific descriptions/canonicals on `play.html`, `privacy.html`, `support.html`
- Google Search Console verification (`googleed40a47e6f229092.html`) and IndexNow key (`indexnow-key.txt`) live

## Free App Store visibility / ASO

**Paste pack:** [`ASO_METADATA.md`](./ASO_METADATA.md)

- Subtitle, keywords, promotional text, full description, What's New — see `ASO_METADATA.md` for exact text and character counts
- Secondary category recommendation: **Arcade** (keep primary **Casual**)
- New `app.html` dedicated App Store landing page + strengthened App Store CTA on `index.html`
- Screenshot/preview shot list in `ASO_METADATA.md`

### App Store Connect fields — confirm pasted

Check these are set in Connect (the agent cannot access Connect directly):
1. Subtitle → `Endless city flyer`
2. Keywords → see `ASO_METADATA.md`
3. Promotional Text / Description / What's New → see `ASO_METADATA.md`
4. Secondary category → Arcade
5. Marketing URL `https://beckythebat.com` · Support `https://beckythebat.com/support.html`

## Explicitly deferred

- **Server-side Stripe Checkout Session verification**: would let web purchases be verified rather than trust-based. Needs a small backend (none exists today). Not pursued — current trade-off accepted.
- **Server-side native IAP receipt validation**: native path still trusts the Capacitor plugin result + local dedup. Accepted for cosmetic continue currency.
- **`main` branch**: still an old, unrelated Capacitor skeleton (`com.pinkbat.game`) predating this project. The live product only ever lived on `vicky-the-bat-final` / `gh-pages`. Not touched.
