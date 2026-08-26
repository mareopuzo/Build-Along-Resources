# Clay Demo — Personalized Landing Pages

## Context
User is an AE at Clay.com. 5 prospects requested a demo; goal is to send each one a personalized landing page (not a generic one) to help close the deal.

## Source files (read, don't rebuild)
- `clay_icp.txt` — Clay's ICP: firmographics, tech signals, buyer personas, pain points that trigger purchase
- `clay_value_prop.txt` — Clay's value prop, stats (3x enrichment, 80% less research time, 5,000+ customers, 4.9 G2), core use cases
- `landing-page-prospects.csv` — the 5 prospects (name, email, title, company, website, LinkedIn)

## Decisions made (confirmed with user via AskUserQuestion)
- **Personalization depth:** role-tailored messaging — each page leads with the pain point most relevant to that person's title, not just company name swapped in
- **CTA:** "Book a demo call" — button currently links to placeholder `#book-demo`, user will swap in real scheduling link later
- **Research source:** was supposed to use AI Ark (mcp__ai-ark tools), but AI Ark returned `402 insufficient credit` on all 5 company lookups — fell back to WebSearch for real, current company signals (funding, revenue, growth stats) instead
- **Output format:** 5 separate static, self-contained HTML files (no build step, no external deps) — not a single template+data system
- **Visual design:** neutral/professional SaaS aesthetic (navy/indigo accent, system font stack), not Clay's actual brand assets (no logo files available)

## What's done
All 5 pages built in `landing-pages/`, each self-contained HTML:

| File | Prospect | Title | Angle used |
|---|---|---|---|
| `retool.html` | Sarah Mitchell | VP of Revenue Operations | $200M Series C / 415-employee scale → stack consolidation, CRM data hygiene |
| `linear.html` | Marcus Chen | Head of Growth | $82M raise, move upmarket → enterprise targeting, AI research at scale |
| `loom.html` | Emily Rodriguez | Director of Sales Development | Revenue → ~$150M, Intercom's 19% reply-rate lift via video+data → SDR research-time drain |
| `webflow.html` | James Okonkwo | GTM Engineer | 205% YoY growth in GTM engineering job postings → build-vs-buy, programmable enrichment layer |
| `airtable.html` | Rachel Goldstein | VP of Sales | $480M ARR, 50% YoY enterprise deal growth → pipeline coverage keeping pace |

Each page includes: role-specific headline, a "why we're reaching out now" box citing a real current stat about that company (sourced via WebSearch, not AI Ark), pain points from `clay_icp.txt` mapped to that role, Clay's value prop/stats block, logo social-proof row, and a final CTA section.

Deliberately avoided leaning on Airtable's Aug 2026 Bending Spoons acquisition news in `airtable.html` — M&A can trigger tooling/spending freezes, so that would be a bad note to strike in an active pitch. Used enterprise ARR growth instead.

## Day 2 — v3 redesign + Vercel hosting (2026-08-26)

**frontend-design skill** installed at `~/.claude/skills/frontend-design/` (from anthropics/skills). Registers in the invocable list on next Claude Code restart; content already internalized and applied.

**Clay brand assets** received (zip → `assets/Day 2 Build Along Resources/`): real Roobert fonts, `clay` claymation logos (SVG/PNG), homepage claymation video (Hero + Data/Agents/Orchestration/Execution/Footer), founder photos, plus `clay-brand-book.md` and `clay-tone-of-voice.md` (both excellent — read them before any further Clay copy/design).

**Key brand facts (supersede the old source files):**
- Palette: oat cream base (`#fefdfb`/`#f3f2ed`), ink `#1b1a18`, hero green `#035d44`, per-section accents (blueberry `#3859f9`, rust `#b53c09`, lime `#cbd810`, dragonfruit `#cc089e`). Retool's real brand (co-brand accent): near-black `#151515`, cream `#e9ebdf`, coral `#e8765e`.
- Type: Roobert, heading line-height 1.0, tracking −0.04em, weight 500–575 (not bold). Roobert Mono for eyebrows/labels/stats.
- Current proof (July 2026): **500,000+ GTM teams · $5B valuation · 200+ data providers · 140M Claygent runs/mo · 4.9★ G2**. The stats in `clay_value_prop.txt` (5,000 customers/$3.1B/150 providers/3x) are STALE — do not use.
- Voice: second person, verb-first, contractions, no exclamation/emoji; proof = named customer + number + mechanism; villain = the old way (never name a competitor). These pages **prime a booked demo, they don't re-sell**. CTA: "Confirm my demo time".

**v3 of Sarah's page** (`landing-pages/retool.html`) — full rebuild on Clay's real system: `Clay × Retool` co-brand, dark-green hero + Hero claymation video, current stats + customer marquee, **signature stacked-card scroll** (4 cards = systems we build in her demo, each with a Clay feature video + named proof), "no slides, we build" 01/02/03 agenda, ball-pit footer CTA. Self-critiqued desktop + mobile in-browser. Shared assets in `landing-pages/assets/{fonts,video,img}` (~26MB, used by all future pages). The other 4 pages are still v2 (old indigo) — redo them on this system next.

**Hosting (LIVE on Vercel):**
- Project `landing-pages` (team `okhiriamario-9385`), deployed from `landing-pages/` with `vercel.json` (`cleanUrls`).
- **Stable public URL: https://landing-pages-okhiriamario-9385s-projects.vercel.app/retool**
- Vercel **Deployment Protection (ssoProtection) was ON by default and was DISABLED via API** so prospects don't hit a login wall. If a redeploy re-enables it, PATCH `v9/projects/{id}` with `{"ssoProtection":null}` (token in CLI auth.json).
- Redeploy after edits: `cd landing-pages && vercel deploy --prod --yes`. Stable URL stays the same.
- Local preview server (this session): `python3 -m http.server 8787` in `landing-pages/` → http://localhost:8787/retool.html
- Fonts are Roobert **trial** + logos are press assets: fine for a 1:1 AE preview, but a truly public page needs a proper Roobert license + Clay press permission.

## Remaining / open items
1. **Swap `#book-demo` placeholder** in all 5 files for the real scheduling link (Calendly or similar) before sending.
2. **AI Ark credit** — if the user wants the "why we're reaching out now" data re-sourced from Clay's own data pipeline (AI Ark) instead of open web search, AI Ark credit needs to be topped up and the 5 company_search calls re-run (calls attempted: `mcp__ai-ark__company_search` by domain for retool.com, linear.app, loom.com, webflow.com, airtable.com — all failed with 402).
3. **Fact-check pass** — the "why we're reaching out now" stats came from web search summaries, not primary sources directly read. Worth a quick verification pass on the specific numbers (funding amounts, ARR, employee counts) before sending, especially anything that could go stale or be wrong.
4. **Hosting** — pages are static HTML files sitting in `landing-pages/`. Not yet uploaded/hosted anywhere. User will need to host these (e.g. Vercel, Netlify, S3) and send the resulting URLs to each prospect.
5. **No branding assets used** — if user gets Clay's actual logo/brand kit, pages could be upgraded to use real brand assets instead of a text wordmark.
