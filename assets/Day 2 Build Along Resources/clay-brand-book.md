# Clay Brand Book (Working Reconstruction)

*Built 2026-07-21. Clay publishes an official press kit (logo files plus co-branding rules) at **clay.com/press**, but no full public brand book. This doc reconstructs the system from clay.com's actual front-end code (CSS custom properties, @font-face, keyframes, read live in the browser and re-verified against the downloaded CSS bundles), screenshots, and Clay's own "Behind the scenes of Clay's new homepage" blog post (July 2026). Structure follows the best public brand guidelines (Webflow, Shopify, Carbon, Red Hat). A designed, paginated version lives in `clay-brand-book.html` / `clay-brand-book.pdf`.*

**Status key:**
- **CONFIRMED** — read from clay.com's code or official pages, spot-checked.
- **OBSERVED** — seen in screenshots or live browsing, not extracted as a token.
- **HYPOTHESIS** — inferred; verify before treating as canon.

---

## 1. Brand foundation

Clay's brand team describes the brand as **"playful, expansive, creative"** and **"felt, not explained"** (CONFIRMED, their homepage-redesign post and brand-designer JD). Positioning: Clay invented **GTM engineering**, and the product is *infrastructure*: "Build systems to grow revenue." Their design stance, in their own words, is set against the "sea of grey websites, AI generated blurry textures." Craft is the differentiator. The visual metaphor is literal **clay**: stop-motion plasticine machines that move little colored balls (data) through pipelines.

Voice lives in the companion doc: `clay-tone-of-voice.md`.

---

## 2. Logo

- Wordmark "Clay"; official downloadable logo ZIP at **clay.com/press** (CONFIRMED, with do's/don'ts and usage restrictions: editorial use only, permission via press@clay.com).
- OBSERVED on site: monochrome wordmark. Ink on light backgrounds, cream on the dark green hero. Never gradiented, never recolored into accent hues.
- For our pages: the pilot's simple two-dot mark is our own stand-in, not Clay's real mark. Acceptable for a preview; swap in the real asset from /press if this ever ships.

### Co-brand lockup ("Clay × [Company]")
Clay's press kit includes co-branding guidance on spacing and visual balance (CONFIRMED it exists). Synthesized with public co-branding standards (Red Hat, Lucid):
- **Clay leads** (these are Clay-authored pages): Clay mark first, on the left; partner second.
- The **×** is a legitimate divider mark. Give it equal spacing on both sides and generous clear space, at least the width of the smaller mark.
- **Equal visual weight**, not equal pixel height. Never modify, recolor, or merge either logo. The partner's accent color goes into the *page*, never into either logo.

---

## 3. Color

All hex values CONFIRMED from `:root` custom properties in clay.com's CSS unless noted.

### Neutrals — the "oat" family (warm cream base)
| Token | Hex | Use |
|---|---|---|
| oat-50 | `#fffcfa` | lightest wash |
| oat-100 | `#fefdfb` | page background, headline text on dark |
| oat-200 | `#f3f2ed` | secondary button bg, card bg |
| oat-300 | `#eee9df` | tinted panels |
| oat-400 | `#dad4c8` | borders/dividers (also `#e0dedc` border token) |
| oat-500–800 | `#c0bbaf` → `#55534e` | muted text ramp |
| Ink | `#1b1a18` (also `#1d1c1a`; `#000` on buttons) | text, primary buttons |

**Hero green:** `#035D44`, the dark green hero and footer landscape background (CONFIRMED computed on the hero section, spot-checked in the CSS bundle).

### Accent families (each runs 100→900; the working shade in bold)
| Family | Working shades | Section pairing on clay.com |
|---|---|---|
| **Blueberry** (blue) | **`#3859f9` / `#395afa`**, light `#429dff`, deep `#001433` | DATA |
| **Tangerine** (orange/rust) | `#ff7614`, **CTA rust `#b53c09`**, tint `#fff3ed` | AGENTS |
| **Lime** | **`#cbd810`**, highlight `#eef773`, tint `#fcfee2` | ORCHESTRATION (also UI row highlights) |
| **Dragonfruit** (magenta) | **`#cc089e`**, tint `#f8b9e3`, `#ff7ad5` | EXECUTION |
| **Lemon** (yellow) | **`#fcbe11`**, tint `#fae188` | eyebrows/badges |
| Pomegranate (red) | `#fb4450`, `#c22e3d` | sparing |
| Ube (purple) | `#8b5cf6`, `#7934f0`, tint `#c1b0ff` | sparing |
| Slushie (cyan) | `#3bd3fd`, deep `#008aad` | sparing |
| Matcha (green) | `#078a52`, tint `#dbffe0` | sparing |

**Usage rules (OBSERVED pattern, stated as decision rules):**
1. The base is always oat cream plus ink. Accents are *per-section*: one family per card or section, never a rainbow within one block.
2. Two-line headlines put the second line in the section's accent color.
3. Accent tints (`-100/-200`) make card backgrounds; the `-400/-500` shade makes the CTA and eyebrow inside that card.
4. Dark green `#035D44` is reserved for the hero and final-CTA landscape scenes.

---

## 4. Typography

- **Primary: Roobert**, loaded as `RoobertVF` variable font, weight range 300–900, stack `Roobertvf, Arial, sans-serif` on everything (CONFIRMED from @font-face and computed styles; 60+ references in the CSS bundles). Roobert is a licensed commercial face.
- Also declared: **Roobert Mono** (secondary/mono token), **Canela Web** (serif, 300/400 plus italics — CONFIRMED declared, sparingly used), and Inter as a legacy token.
- **We now have Roobert trial files** (Displaay trial OTFs plus the variable TTF, supplied by Mhae) in `clay assets/Roobert-Font/`. Fine for internal previews and mockups; a public page needs a proper license. Free fallback where the trial won't stretch: **Schibsted Grotesk** (what the pilot uses), with Inter Tight as backup.
- **Also in `clay assets/`:** Clay's real homepage animation files — the hero mp4 and the four feature-card webm loops (Data, Agents, Orchestration, Execution, plus Reps). These can replace the hand-drawn SVG blobs on our pages.

**Scale (CONFIRMED computed at 1538px viewport):**
| Element | Size/line | Weight | Tracking |
|---|---|---|---|
| h1 | 88px / **1.0** | **575** (variable) | −0.04em |
| h2 | 72px / 1.0 | 500 | −0.03em |
| h3 | 48px / 1.0 | 500 | −0.04em |
| Body | 16px / 24px | 400 | normal |
| Nav | 14px / 21px | 500 | — |

**The signature type moves:** line-height of exactly 1.0 on headings (tighter than the pilot's 1.08), tight negative tracking, and medium weights (500–575) rather than bold. Size and tightness do the work, so the headlines hold their presence without shouting.

---

## 5. Layout & grid

- Content max-width **1280px** (`.container-regular`, CONFIRMED); fluid token up to 1440px; nav wider (2000px).
- Section vertical padding **48–64px** (CONFIRMED on sampled sections), a denser rhythm than typical SaaS.
- **Homepage wireframe (OBSERVED):** sticky rounded nav → dark green hero with 3D clay landscape and a left-aligned headline → cream logo-marquee card with stat callouts → product-tabs section → "What do you want to build?" AI prompt box → **stacked feature cards** (the signature section) → reps section → video-testimonial carousel → content cards → cream final CTA over a giant clay ball-pit scene → white rounded footer card floating on the ball-pit image.
- Use-case pages are calmer: white background, split hero (headline left, media card right), same tokens.

---

## 6. Imagery & illustration

(OBSERVED; illustrator Hudson Christie, CONFIRMED via Clay's redesign post.)
- **Claymation 3D renders**: matte plasticine with a fingerprint-ish texture, soft studio light, accents matched to the token families.
- Recurring motifs: **Rube Goldberg toy machines** (funnels, chutes, conveyors moving colored balls, which read as data through pipelines), **pastoral green hills with toy trees** (hero and footer), **ball pits**, and partner mascots re-sculpted in clay (case studies).
- Placement: inside rounded cards, or full-bleed at the very top and bottom of the page. The page opens and closes in the clay world; the middle is clean product UI.
- For our static pages: flat SVG "clay-style" blobs (the pilot approach) are the honest budget version. Keep shapes matte and rounded, with a single soft ground ellipse for shadow.

---

## 7. Motion

(CONFIRMED from code except where noted.)
| Motion | Implementation | Values |
|---|---|---|
| Button hover | background-color only, no lift or shadow | `0.3s cubic-bezier(0.075, 0.82, 0.165, 1)` (strong ease-out; 21 occurrences in the bundle) |
| **Stacked-cards scroll** (signature) | plain CSS `position: sticky; top: 72px` per card, so each card slides up over the last | no JS scrub (read live in browser) |
| Logo marquee | `@keyframes marquee { to { transform: translateX(-50%) } }` infinite | read live; vertical variants also exist |
| Entrances | `fadein` (opacity), `bouncy` (rotateZ 0→−4°→0 wobble), shimmer `load` | keyframes in page CSS (read live) |
| Prompt box | typewriter placeholder | JS-driven (HYPOTHESIS: simple interval) |
| What they *don't* do | scroll-jacking, parallax everywhere, elevation shadows | GSAP is loaded but runs 0 ScrollTriggers on the homepage |

**Motion principles:** flat color changes instead of shadows and lifts; one signature scroll moment per page (the card stack); playful easing (fast start, soft landing). Everything else stays static and composed.

---

## 8. Components

- **Buttons:** 12px radius (CONFIRMED), padding ~8px 16px, weight 500. Primary is black `#000` with white text, hover → grey-900 `#282c35`. Secondary is oat-200 cream with ink text. In-card CTAs take the card's accent (`#395afa`, `#b53c09`, `#cc089e`) with white text. **No box-shadows anywhere.** The system is flat color plus radius.
- **Cards:** large radii (~24–32px OBSERVED), accent-tinted backgrounds, pill eyebrow tag, two-line heading with the accent second line, a proof line, an accent CTA, and a 3D illustration on the right.
- **Chips/tags:** 16–18px radius, lime `#eef773` for the active or highlighted state.
- **Logo strip:** a marquee inside a cream rounded card, logos interleaved with bold stat callouts ("+140% outbound pipeline"). Proof and logos live in one component.
- **Footer:** white rounded card floating over the illustration; "Born in Brooklyn ©2026 Clay Labs Inc."

---

## 9. Proof points & scale claims (keep current)

As of July 2026 (CONFIRMED on site): **500,000+ leading GTM teams · $5B valuation (NY Times–covered tender offer) · 200+ data providers · 140M monthly Claygent runs · 4.9★ G2.** The numbers in `clay_value_prop.txt` (5,000 customers, $3.1B, 150+ providers) are stale.

---

## 10. Governance for this project

- These pages are **previews, Clay-led, one prospect each**, marked non-public (the pilot's footer note does this correctly).
- Never invent facts about the prospect (project guardrail).
- Real Clay logo assets: clay.com/press (editorial-use terms; fine for an internal AE demo asset, but get permission before anything public).
- Partner accent colors: pull real hex from the partner's live site, never from memory. **Retool (CONFIRMED from retool.com computed styles, July 2026): near-black `#151515` base, warm cream `#e9ebdf` logo and buttons (fully-rounded pills), accent orange `#e8765e`** (plus blue `#518dd2`, green `#4d9987`), font pxGrotesk. Retool has rebranded, so the old indigo `#3C3C8C` in the pilot is stale.
