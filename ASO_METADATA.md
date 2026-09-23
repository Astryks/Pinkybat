# Becky the Bat — App Store Connect paste pack (FREE only)

**App:** https://apps.apple.com/us/app/becky-the-bat/id6803877783  
**Site:** https://beckythebat.com  
**Repo (gh-pages):** https://github.com/Astryks/Pinkybat  
**Prepared:** 2026-09-24 (Australia/Sydney)  
**Rules:** No Apple Search Ads · no paid ASO tools · no directory fees · honest claims only

---

## PASTE NOW — App Store Connect fields

Copy each block into Connect. Limits checked.

### Subtitle (≤30 characters) — 18 chars

```
Endless city flyer
```

### Keyword field (≤100 characters, commas, no spaces) — 99 chars

Do **not** repeat title (`Becky the Bat`) or subtitle (`Endless city flyer`) words.

```
arcade,flappy,plane,obstacles,landmarks,offline,kids,casual,travel,skyline,tap,glide,hearts,weather
```

### Promotional Text (≤170 characters) — 167 chars

Can change anytime without a new binary.

```
New: fly Becky through 100+ cities for free. Collect hearts, dodge planes & skyline obstacles. Optional one-time 100 Hearts to continue after a crash — never required.
```

### Description (full rewrite — paste entire block)

```
Fly with Becky the Bat on a nonstop journey around the world.

Take off and soar through more than 100 real-world destinations — each with its own skyline, landmarks, and weather. Tap and hold to flap and climb; release to glide and dive. Weave between buildings, planes, and obstacles high, mid, and low as the pace keeps building.

WHAT YOU GET
• Explore 100+ destinations, from famous cities to hidden gems
• Dodge obstacles that test your timing at every altitude
• Fly through rain, snow, and changing weather as the world shifts
• Collect hearts as you fly
• Difficulty ramps the further you go
• Share your best runs with friends
• Play offline once the iOS app is installed

FREE TO PLAY
Becky the Bat is free. You can always start a new run at no charge.

OPTIONAL IN-APP PURCHASE
If you crash, you can continue from where you left off by spending 100 hearts you collected in play — or by buying the optional “100 Hearts” pack through Apple In-App Purchase (one-time, handled by Apple). Hearts are never required to keep playing; they only unlock continue-from-crash. No ads. No subscription.

Privacy: Data Not Collected (see App Privacy). How far can you fly?
```

### What’s New (draft for next version / metadata update)

```
ASO polish and clearer free-to-play messaging. Becky remains free — optional 100 Hearts only continues a run after a crash. Bug fixes and performance improvements.
```

*(If shipping a binary with in-app review: add “Native review prompt after a new personal best (Apple’s system dialog, rate-limited).”)*

---

## Sid — App Store Connect checklist

Paste / set in Connect (this agent does **not** log into Connect):

1. [ ] **Subtitle** → `Endless city flyer`
2. [ ] **Keywords** → keyword field block above (replace old keywords entirely)
3. [ ] **Promotional Text** → promo block above
4. [ ] **Description** → full description block above
5. [ ] **What’s New** → draft above (when you submit next version, or if Connect allows text-only update)
6. [ ] **Secondary category** → set **Arcade** (keep primary **Casual**). Prefer Arcade over Action: endless tap-flyer / obstacle rhythm fits Arcade; Action implies combat/shooting you do not have.
7. [ ] **Screenshots / preview** → see shot list below; replace any weak frames
8. [ ] **Age rating / IAP** → confirm 100 Hearts still listed; no new IAP claimed here
9. [ ] **App Privacy** → keep **Data Not Collected** unless you add analytics (do not for this free pass)
10. [ ] **Support URL** → https://beckythebat.com/support.html · **Marketing URL** → https://beckythebat.com
11. [ ] After paste, save locale (English US) and submit for review only if Connect requires it for metadata

---

## Secondary category tip

| Choice | Verdict |
|--------|---------|
| **Arcade** (recommended secondary) | Best genre match for endless flyer, reflex tapping, escalating speed |
| Action | Weaker fit — players expect combat, weapons, or combat missions |
| Keep **Casual** as primary | Matches current listing and broad discovery |

---

## Screenshot / preview shot list (App Store)

Use existing `store-assets/screenshots/` where possible; capture missing frames on device.

| Order | Frame | On-device beat | Caption idea (optional) |
|------:|-------|---------------|-------------------------|
| 1 | Hero / title feel | Becky mid-flight over a famous landmark | Explore 100+ cities |
| 2 | Landmark beauty | Sydney Opera House (or similar) | Humans built beautiful things |
| 3 | Variety | Golden Gate / second iconic city | So many places to see |
| 4 | Weather | Rain / snow run | Every flight feels different |
| 5 | Hearts | Collecting hearts HUD visible | Collect hearts as you fly |
| 6 | Continue honesty | Keep Flying panel showing hearts **and** optional buy | Free to play · optional continue |
| 7 | (iPad if shown) | Same beat, landscape or large phone | — |

**App Preview video (optional, free to film yourself):** 15–30s — tap to flap, pass 2–3 cities, collect hearts, end on title; **do not** open IAP sheet in the preview.

Existing site assets:  
`https://beckythebat.com/store-assets/screenshots/01_explore_the_world.png` … `06_keep_flying_free.png`

---

## In-app review (SKStoreReview) — status & steps

**Shipped on gh-pages web build:** guarded helper in `play.html` that calls Capacitor `InAppReview.requestReview()` **only** when:

- native platform (`Capacitor.isNativePlatform()`),
- plugin is present,
- player just set a **new personal best**, then taps to start another run (not on the crash/paywall frame itself),
- local cooldown (~120 days) and max ~3 prompts / year (Apple also rate-limits).

**Not shipped in the App Store binary until Sid adds the free plugin and submits a build.**

### Free native steps (no paid SDK)

1. In the Capacitor iOS app project (not this static-only gh-pages tree alone):

```bash
npm i @capacitor-community/in-app-review
npx cap sync ios
```

2. Confirm `InAppReview` appears under Capacitor plugins; no StoreKit ads SDK required — this wraps Apple’s `SKStoreReviewController` / `requestReview`.
3. Ship a new App Store build that loads the updated `play.html` (or synced www).
4. **Never** call review on: crash instant, continue/paywall buttons, purchase success/fail, or web/browser.
5. TestFlight: Apple often suppresses the dialog; verify with a production or Review-prompt-friendly build.

Until the plugin is in the binary, the web helper is a no-op (safe).

---

## Character counts (verification)

| Field | Limit | Used |
|-------|------:|-----:|
| Subtitle | 30 | 18 |
| Keywords | 100 | 99 |
| Promotional Text | 170 | 167 |

---

## Out of scope (intentionally)

- Apple Search Ads
- Paid ASO / keyword tools
- Product Hunt / paid directories
- Fake ratings or incentivized reviews
