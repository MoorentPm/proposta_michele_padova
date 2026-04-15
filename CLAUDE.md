# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Behavioral Rules (Always Enforced)

- Do what has been asked; nothing more, nothing less
- NEVER create files unless they're absolutely necessary for achieving your goal
- ALWAYS prefer editing an existing file to creating a new one
- NEVER proactively create documentation files (*.md) or README files unless explicitly requested
- NEVER save working files, text/mds, or tests to the root folder
- ALWAYS read a file before editing it
- NEVER commit secrets, credentials, or .env files

## Project Overview

This is a **static single-page HTML proposal** (in Italian) for short-term rental management of an apartment in **Padova (Via Sant'Eufemia, 7 bis)**, targeted at a client named **Michele**. The entire deliverable is `index.html` — one self-contained file with embedded CSS and JavaScript.

The page covers: market analysis, competitor positioning (10 competitors for 8+ guests in Padova), revenue projections, financial calculator, regulatory framework, and service overview.

**Important rules for this project:**
- Never mention students — this is purely about short-term rental (affitto breve)
- All financial calculations must always include Moorent PM commission (20% of gross revenue)
- Do not show or reference an estimated property value
- The 10 Airbnb competitor listings for 8+ guests in Padova are documented in the `#competitors` section:
  1. Alloggio in affitto — Nicola (9 ospiti) → /rooms/1360822496647070880
  2. Grazioso appartamento a due passi dal centro (9 ospiti, Federico) → /rooms/1180549688989748449
  3. Suite IdealHome (8 ospiti, Davide) → /rooms/1376830566650531709
  4. Appartamento — Lt Portavenezia (8 ospiti) → /rooms/1391251295856948703
  5. Da verificare (8+ ospiti) → /rooms/1603782793545780999
  6. Alloggio in affitto — Mat (9 ospiti) → /rooms/1359247600118882909
  7. Alloggio in affitto — Giovanni (8 ospiti) → /rooms/1085357289037493395
  8. Casa — Francesco (9 ospiti) → /rooms/928921306822909690
  9. Alloggio in affitto — Filippo (10 ospiti) → /rooms/1354927843480361037
  10. Alloggio in affitto — Vincenzo (8 ospiti) → /rooms/26769365

## File Organization

- `index.html` — the only source file; all CSS and JS are embedded inline
- `images/` — logo and interior photos (logo-moorent.png, soggiorno.webp, camera.webp, etc.)
- No build step, no test suite, no compilation — open directly in a browser

## Tech Stack

- **Styling**: Tailwind CSS (CDN) with custom color tokens via `tailwind.config`
- **Fonts**: Google Fonts CDN — Noto Serif (headings) + Inter (body)
- **Icons**: Material Symbols Outlined (Google CDN)
- **Charts**: Chart.js 4.4 (CDN, `chart.umd.min.js`)
- **Language**: Italian (`lang="it"`)

## Development

Open `index.html` directly in a browser — no server needed.

The `package.json` lists `typescript` and `agentic-flow` as dependencies but **no npm scripts are defined**. Do not reference `npm run build`, `npm test`, or `npm run lint` — they don't exist.

## Architecture of `index.html`

Sections in order:
1. `#analysis` — Market context (Padova STR market, why city centre)
2. `#competitors` — 10 Airbnb competitors for 8+ guests, scarcity analysis
3. `#scenarios` — Monthly revenue table + chart + annual summary
4. `#calculator` — Interactive ADR/occupancy sliders
5. `#legals` — Regulatory framework (locazione turistica breve, cedolare secca)
6. `#strategy` — Moorent service description + income breakdown

Key layout decisions:
- **Nav**: fixed, scroll-spy highlights active section via `nav-active` CSS class
- **Hero**: full-viewport photo background (Padova cityscape) with dark overlay for readability
- **Charts**: Chart.js bar chart in `<canvas id="monthlyChart">`; data inline in `<script>` at bottom
- **Calculator**: sliders for ADR and occupancy; fixed deductions: OTA 15%, cedolare 21%, Moorent 20%, maintenance €360/yr
- **Responsive**: Tailwind breakpoints; hamburger menu for mobile nav

## Financial Model

- **Gross revenue**: ADR × nights × occupancy
- **Deductions applied in every calculation**:
  - OTA commissions: 15% of gross
  - Cedolare secca (flat tax): 21% of gross
  - Moorent PM fee: 20% of gross
  - Maintenance: €360/year
- **Net for Michele**: gross × 0.44 − €360/year (≈ €32.286 at base scenario)
- Base scenario: 211 nights/year (58% occupancy), €352 avg ADR
