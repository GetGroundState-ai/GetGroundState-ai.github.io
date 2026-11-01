# Handoff: GroundState Marketing Website

## Overview
A single-page marketing site for **GroundState**, an AI process and services agency. In order, the page explains the problem, the Outcome Owner model, the 90-day process, how GroundState uses AI, its commitments, the first engagement, the team and case studies, and ends with a "Book a Diagnostic call" call to action.

The signature element is a full-viewport animated **ground plane** behind all content: a perspective wireframe grid that rolls like turbulent terrain at the top of the page and flattens into a perfectly level plane as the visitor scrolls to the end. It visualises a business "reaching its GroundState".

## About the Design Files
The files in this bundle are **design references created in HTML**: a working prototype showing the intended look, copy and behavior. They are not production code to ship directly. Recreate the design in the target codebase's environment. If there is no codebase yet, a static-first framework (Astro, or Next.js with static export) fits well, with the background built as one isolated client component.

`GroundState Site.dc.html` opens in a browser when `support.js` and `image-slot.js` sit beside it. All styles are inline. The logic class at the bottom of the file holds the step data, scroll handling and canvas drawing code, which can be ported nearly verbatim.

## Fidelity
**High-fidelity.** Final copy, colors, typography, spacing and interactions. Recreate it pixel-accurately. The copy is client-approved; use it **verbatim**.

---

## Brand / Logo
Lockup = **app-icon monogram** + **two-tone wordmark**.

- **Monogram G** (viewBox `0 0 48 48`, no fill):
  - Arc: `M38.5 13.5A17 17 0 1 0 41 26`. Stroke ink, **butt** linecap.
  - Crossbar: `M24 26H41`. Stroke teal, **round** linecap. The crossbar sits *inside* the G; it does not extend past the curve.
  - Stroke width 3.6 for the plain mark, 4.6 inside the app-icon tile.
- **App icon (used on the site):** a rounded square tile, `background #1B1E21`, `border 1px solid rgba(243,240,234,0.12)`, radius ≈ 22% of its size, with the G at 70% of the tile size. The tile is slightly lighter than the page so it stays visible on `#0F1113`.
- **Wordmark:** "Ground**State**" in Newsreader 500, letter-spacing -0.02em, line-height 1. "Ground" in ink, "State" in teal. Use `text-box: trim-both cap alphabetic` so it centres optically against the icon.
- Colors: on dark backgrounds ink `#F3F0EA` and teal `#4FD0B8`; on light backgrounds ink `#0F1113` and teal `#0E7A68`.
- Exported PNGs are in `logo/` (see Assets). Favicon = `logo/groundstate-icon-dark-tile.png`.

---

## Global Layout
- Page background `#0F1113`; default text `#F3F0EA`; body font Hanken Grotesk.
- Content column `max-width:1320px; margin:0 auto;` horizontal padding `clamp(20px,4vw,56px)`.
- Section vertical padding 16vh (large sections) or 12vh (compact sections).
- Layers: canvas `position:fixed; inset:0; z-index:0; pointer-events:none` → `<main>` `position:relative; z-index:1` → fixed header and HUD `z-index:10`.
- Panels over the animation use `rgba(15,17,19,0.72)` or `0.8` to keep contrast.
- **All grids** use `repeat(auto-fit, minmax(min(100%, Npx), 1fr))`, so they collapse to one column and never overflow on small phones.
- **Breakpoint:** 760px (`isWide = innerWidth >= 760`), used for the nav, HUD, sticky heading, header CTA label and Gantt labels.

### Eyebrow label style (shared)
JetBrains Mono, `clamp(14px,1.2vw,17px)`, weight 500, letter-spacing .12em, uppercase. Teal by default; orange `#E08A63` in the hero and problem sections.

---

## Sections (top to bottom)

### Header (fixed)
- Flex, space-between, gap 24px, padding `16px clamp(20px,4vw,56px)`; background `rgba(15,17,19,0.6)` with `backdrop-filter: blur(10px)`; bottom border `1px solid rgba(243,240,234,0.08)`.
- Left: logo lockup (36px app icon, 10px gap, wordmark 26px), linking to the top.
- Middle (≥760px only): nav in JetBrains Mono 12px, uppercase, .08em, `#9EA3A8`, gap 28px: **Approach** (#approach), **Process** (#process), **AI** (#ai), **Team** (#team).
- Right: pill CTA (Mono 13px, background `#4FD0B8`, text `#0F1113`, padding 10px 16px, radius 999px). Label is **"Book a Diagnostic call"** at ≥760px and **"Book a call"** below that. Links to #book.

### System-state HUD (fixed, ≥760px only)
Bottom-right (`right:16px; bottom:16px; width:168px`), padding 10px 12px, background `rgba(15,17,19,0.7)` with blur 8px, 1px hairline border, radius 8px, Mono 10px uppercase.
- Row: "System state" and "E = 0.82" (energy to 2 decimals).
- State label at 14px: >0.8 "Excited · unmeasured", >0.55 "Measured", >0.3 "Settling", >0.02 "Near ground", else "Ground state". Orange while energy > 0.02, teal at ground state.
- A 3px bar whose width = energy %.
- Keep it behind a config flag.

### 1. Hero
- `min-height:100vh; padding-top:24vh; padding-bottom:12vh`; flex column, gap 32px.
- Eyebrow (orange): **GroundState: steady state, built on ground truth**
- H1 (Newsreader 400, `clamp(52px,8.5vw,136px)`, line-height .95, letter-spacing -.02em, max-width 1100px): **We find your GroundState,** line break, then **and improve it.** in teal (not italic).
- Paragraph (max-width 640px, `clamp(18px,1.6vw,22px)`, line-height 1.5, `#D6D2CA`): "One named Outcome Owner. We find out where your business loses time and money, agree on what should improve, then build the software and automation that fixes it."
- Button **Book a Diagnostic call**: background `#F3F0EA`, text `#0F1113`, weight 600, padding 16px 24px, pill. Beside it: "SCROLL TO REACH GROUNDSTATE ↓" in Mono 12px, .08em, `#9EA3A8`.

### 2. Problem (#approach)
- Two-column grid (min 300px per column), gap 48px.
- Left: eyebrow "The problem" (orange) and H2 **Why improvements stall:** (Newsreader `clamp(36px,4vw,56px)`). **Sticky (`top:20vh`) only at ≥760px**; static below that, because sticky overlapped the text on mobile.
- Right: four statements in Newsreader `clamp(28px,3.2vw,46px)`, line-height 1.18, spaced `clamp(48px,22vh,240px)` apart. The emphasised phrase is italic orange:
  1. The problem is never pinned down, so teams *solve the wrong thing*.
  2. The work crosses departments, so *no one owns the result*.
  3. The plan is made in a conference room. *The front line is never asked*, so the change doesn't stick.
  4. Projects run long and priorities shift, so *support fades before results arrive*.
- Source note (Mono 12px, `#9EA3A8`): "Drawn from the leading causes of failure identified in a 2024 review of 49 studies on process improvement projects (Bader et al., *International Journal of Lean Six Sigma*)." Source: https://emerald.com/insight/content/doi/10.1108/IJLSS-07-2023-0126/full/html

### 3. Outcome Owner
- Eyebrow "What we do differently". H2 **One engagement. / One Outcome Owner.** (`clamp(44px,6vw,96px)`, line-height 1).
- Three columns (min 260px), gap 48px. Each has a top border `1px solid rgba(243,240,234,0.25)` and padding-top 20px. Title in Newsreader italic 40px teal, body 19px `#D6D2CA`:
  - **Leads it.** Works inside your operation, from diagnostic to findings.
  - **Builds it.** The person who measures the result is the person who built it.
  - **Reports it.** What the evidence supports, including misses and uncertainty.
- Full-width statement with the same top border, padding-top 40px, Newsreader `clamp(30px,3.6vw,52px)`, line-height 1.15: "We take on only as much work as our Outcome Owners can personally lead, build, and measure."

### 4. Process (#process). Interactive, **not** sticky.
- Eyebrow "The proven process". H2 **90 days, six steps**.
- **Gantt panel:** padding 20px, panel background, hairline border, radius 10px.
  - Header row: week columns `1 … 12, QC` (Mono 11px, muted).
  - Grid columns: `[label] repeat(13, minmax(0,1fr))`, gap 4px. The label column is `clamp(84px,26vw,220px)` at ≥760px and `28px` on mobile.
  - Each row: label (14px, ellipsis) followed by a bar 14px tall, radius 2px, colored by phase, positioned at `left = (start-1)/13` and `width = (end-start+1)/13`.
  - **Labels:** "01  GroundState Diagnostic" on desktop, the **number only** ("01") on mobile.
  - The selected row has opacity 1; the others 0.4. Clicking a row selects it.
- **Phase cards:** an outer grid with `grid-auto-rows: auto 1fr 1fr; gap:14px 32px`. Each phase block has `grid-row: span 3; display:grid; grid-template-rows: subgrid`, which makes **every step card the same height** (a hard client requirement).
  - Phase header: 3px top border in the phase color, name in Newsreader 30px, weeks in Mono 11px uppercase muted. It wraps on narrow screens.
  - Step card: padding 20px, radius 10px, panel background. 1px border: the phase color when selected, otherwise `rgba(243,240,234,0.1)`. Contents: "01 · Weeks 1–2" (Mono 12px muted), title (20px/600), copy (16px, line-height 1.55, `#D6D2CA`). Clicking a card selects it.

| # | Title | When | Weeks (13 = QC) | Phase | Copy |
|---|---|---|---|---|---|
| 01 | GroundState Diagnostic | Weeks 1–2 | 1–2 | Find the truth | We map where time, money, and work actually go. You see your business as it really operates, sometimes for the first time. |
| 02 | Outcome Agreement, Baselines & Targets | Week 2 | 2 | Find the truth | We write down what should improve, how it's measured, and what would prove us wrong. If we can't name it, we don't start. |
| 03 | Build in weekly cycles | Weeks 3–12 | 3–12 | Move the number | Small builds, made side by side with your team inside your operation. Each one is reviewed the week it ships. No big reveals or launches. |
| 04 | Weekly scoreboard | Every week | 3–12 | Move the number | What moved, what didn't, what we changed and why. In writing, including the weeks nothing moved. |
| 05 | Steady State Outcome | Week 12 | 12 | Keep what works | Written findings, working systems, and trained owners. Your team takes it over, or GroundState keeps improving it. |
| 06 | Next GroundState | Quarter close | 13 | Keep what works | Both sides review the evidence: did the promise hold? Then we decide together on continuation, expansion, or a handover process. |

Phases: **Find the truth** (`#4FD0B8`, "Weeks 1–3"), **Move the number** (`#F3F0EA`, "Weeks 3–12"), **Keep what works** (`#E08A63`, "Week 12 & quarter close").

### 5. How we use AI (#ai)
- Eyebrow "How we use AI". H2 **AI is a tool, / not a religion.**
- Three panels (min 280px), gap 24px, padding 28px, radius 10px, hairline border. Each has a Mono 11px label, a Newsreader 32px title and 17px body:
  - BUILD (teal label): **Software first**. AI made builders faster. We spend that speed on straightforward automation and software that moves your business forward.
  - IN THE WORKFLOW (ink label): **AI where it fits**. Next-step guidance for your frontline. Approvals and denials. Fraud and anomaly detection. Deployed in the process, when the process calls for it.
  - JUDGMENT (orange label): **Not where it doesn't**. Plenty of numbers move further with plain, deterministic pipelines. We ship those with the same confidence.

### 6. Commitments
- Eyebrow "Commitments". H2 **What you can hold us to** (`clamp(40px,5vw,72px)`).
- Panel (padding 8px 28px, radius 10px) with four rows separated by `1px solid rgba(243,240,234,0.12)`.
- Each row: a **44px app-icon tile** (radius 10px, G at 31px) followed by a two-column grid (min 300px per column, gap 10px 48px, baseline-aligned):
  - Left: commitment in Newsreader `clamp(26px,2.6vw,36px)`, line-height 1.1, ink, `text-wrap: balance`.
  - Right: explanation in Hanken `clamp(20px,1.7vw,24px)`, line-height 1.45, **teal `#4FD0B8`**.
- Rows:
  1. **Named owner, start to findings** · The person who measures is the person who builds.
  2. **Written kill criteria** · We record what would prove us wrong.
  3. **Weekly scoreboard** · A running record you can audit any day of the week.
  4. **Written findings at week 12** · Data-backed decisions on where to improve next.

### 7. First engagement (prominent panel)
- Panel: padding `clamp(28px,4vw,56px)`, background `rgba(15,17,19,0.8)`, border `1px solid rgba(79,208,184,0.4)`, radius 14px; grid (min 280px), gap 40px.
- Eyebrow "The first engagement". H2 **One improvement, 90 days** (`clamp(44px,6vw,96px)`).
- Three columns, each with a 3px top border (teal / ink / orange), a Mono 13px label and body text at `clamp(20px,1.8vw,24px)` in ink:
  - ENTRY: One consequential, cross-functional improvement that can be meaningfully tested in 90 days.
  - CADENCE: Weekly build cycles, a weekly scoreboard, and a review at quarter close.
  - EXIT: Steady state. Your team owns it, or we keep running it.
- CTA row (full width, top hairline, padding-top 28px, space-between, wraps): "Step one is the Diagnostic: two weeks, hard numbers, and no commitment beyond the truth." followed by a teal pill **Book a Diagnostic call**.

### 8. Team & case studies (#team)
- Eyebrow "Outcome Owners". H2 **The people who / own your outcome**.
- Two profile panels (min `min(100%,520px)`), gap 24px, padding 28px, radius 14px, hairline border. Each holds a portrait (aspect 4:5, radius 10px) and a text column: role (eyebrow style, teal), name (Newsreader `clamp(30px,2.6vw,38px)`, **no wrap**), bio (17px `#9EA3A8`).
  - **Keith Hanson**, Chief Outcome Owner: "Former City of Shreveport CTO and AI consultant with 20+ years of experience helping businesses improve operations, eliminate inefficiencies, and drive results through technology and automation."
  - **Jason Ingalls**, President: "An accomplished entrepreneur, executive, and business advisor with over 25 years of experience. As a company founder and former Chief Cybersecurity Officer, he brings expertise in business leadership, strategic growth, and building successful technology organizations."
  - Portrait photos have not been supplied yet.
- H2 **What our team has built** (`clamp(40px,5vw,72px)`), then three cards (min 280px), gap 24px, padding 24px, radius 12px.
  - Use `grid-template-rows: auto auto auto 1fr auto` so the metric strips align at the bottom.
  - Card contents, top to bottom: 16:10 image (radius 8px); category (Mono 11px uppercase teal); title (Newsreader 28px, line-height 1.1); description (16px `#D6D2CA`); metric strip.
  - Metric strip: top hairline, Mono 12px. Label in muted uppercase, then "from **→** to" with an orange arrow and the "to" value in ink at 14px.
  1. *Enterprise contact center · AI quality assurance*: **From Dozens of Call Reviews to Thousands**. "AI evaluates thousands of calls weekly against complex rules while human-reviewed verdicts continuously improve the process." Metric: COVERAGE · Dozens manual → Thousands AI-evaluated/week. Image: `images/cs-call-qa.png`.
  2. *Industrial distributor · Enterprise intelligence*: **Turning Enterprise Data Into Actionable Intelligence**. "Natural-language AI reporting backed by ERP data, historical analytics, and validated query workflows. From "can you make this report?" to "What is our profit margin for this quarter?"" Metric: AVAILABLE REPORTS · 106 reports → 2.9M+ records analyzed. Image: `images/cs-enterprise-intel.png`.
  3. *Enterprise organization · AI enablement*: **Making an Organization AI-Capable**. "Helped standardize organizational AI practices and developed hands-on agentic development bootcamps for roles ranging from project managers to software engineers." Metric: ROLES TRAINED · Project managers through software engineers (no arrow). Image: `images/cs-ai-enablement-orbit.png`.

> **Content check before launch**
> - **Card 2 metric:** the source evidence describes historical *invoice records* going from 106 to 2,923,380. "106 reports" should be confirmed with the client.
> - **Card 3:** the case-study notes flagged it as "hold for confirmation" until attendance and outcome numbers are supplied.
> - **Client names:** they are intentionally anonymised. Do not add employer or client names, screenshots or confidential details without permission.

### 9. Closing CTA (#book)
- `min-height:100vh; padding:18vh … 30vh`, content centred vertically. The tall bottom padding lets the flattened ground plane show.
- Eyebrow "Next step". H2 **Let's find your** / **GroundState.** (teal), Newsreader `clamp(52px,8vw,128px)`, line-height .95.
- Statement in Newsreader `clamp(28px,3.2vw,46px)`, line-height 1.2, ink, max-width 1000px: "Step one is the Diagnostic: two weeks, hard numbers, and no commitment beyond the truth."
- Teal pill **Book a Diagnostic call** (padding 18px 28px, 18px/600).
- **Wire every "Book" CTA to the real booking tool** (e.g. Calendly or HubSpot). In the prototype they all anchor to #book.

### Footer
Top hairline; padding `40px clamp(20px,4vw,56px) 56px`; space-between, wraps. Left: logo lockup (46px app icon, wordmark 32px). Right: "© 2026 GroundState" in Mono 12px uppercase muted.

---

## Interactions & Behavior

### Scroll progress
- `p = clamp(-rootRect.top / (rootRect.height - innerHeight), 0, 1)`. Recompute on scroll (passive, capture) and on resize.
- Settle value: `s = smoothstep(0.03, 0.93, p)`. HUD energy: `e = round((1 - s) * 100) / 100`.
- For inertia, the canvas uses a smoothed value updated every frame: `ps += (p - ps) * 0.07`.

### Ground-plane background (port `drawPlane` from the logic class)
- Canvas at viewport size × devicePixelRatio, using `setTransform(dpr, …)`. Clear and redraw every frame with `requestAnimationFrame`.
- Intensity `I = 0.35` (allowed range 0.1–1).
  - Time: `t = seconds * (0.2 + 0.6 * I)`.
  - Global alpha: `0.3 + 0.7 * I`.
- Camera: horizon `hy = H * 0.46`; focal length `f = min(W, H) * 0.9`; camera height `h = 1.1`.
- Height field:
  - Amplitude: `A = 1.1 * (1 - s) * (0.35 + 0.65 * I)`.
  - Height: `y(X, Z) = A * ( sin(0.9X + 0.5t) * cos(0.7Z - 0.35t) + 0.5 * sin(2.1X + 1.6Z + 0.8t) )`.
- Projection: `sx = W/2 + X * f / Z`, `sy = hy + (h - y) * f / Z`.
- Depth lines: Z from 2 to 16 in steps of 0.7, each drawn across X from -14 to 14 in steps of 0.35. Alpha `0.06 + 0.45 * (1 - (Z - 2) / 14)`.
- Cross lines: X from -14 to 14 in steps of 1.4, each drawn across Z from 2 to 16 in steps of 0.35. Alpha 0.12.
- Color: interpolate with `k = 1 - s` from teal (79,208,184) at k=0 to orange (224,138,99) at k=1, so the grid shifts from orange to teal as it flattens.
- Horizon line: at `y = hy + h * f / 16`, teal, alpha `0.1 + 0.6 * s`.
- Respect `prefers-reduced-motion`: freeze `t` and keep only the scroll-driven flattening.
- The prototype also contains "Energy levels" and "Signal from noise" backgrounds. The client chose **Ground plane**, so the other two do not need to be built.

### Process selection
`selectedStep` (0–5, default 0) is set by clicking a Gantt row or a step card. It controls the Gantt row opacity and the step card border color.

### Links and focus
`a { color:#4FD0B8 } a:hover { color:#F3F0EA }`. Add visible focus rings in production; the prototype defines none.

## State Management
- `scrollProgress`: drives the canvas.
- `energy`: rounded, drives the HUD.
- `selectedStep`: drives the process section.
- `isWide`: viewport ≥ 760px.

No data fetching.

## Design Tokens
**Colors**
- Background `#0F1113`
- Panels `rgba(15,17,19,0.72)` / `rgba(15,17,19,0.8)`
- Tile / image well `#1B1E21`
- Ink `#F3F0EA`
- Secondary text `#D6D2CA`
- Muted text `#9EA3A8`
- Teal `#4FD0B8` (`#0E7A68` on light backgrounds)
- Orange `#E08A63` (`#B3542E` on light backgrounds)
- Hairlines `rgba(243,240,234, .08 / .1 / .12 / .25)`
- Teal outline `rgba(79,208,184,0.4)`

**Type** (Google Fonts)
- **Newsreader** 400/500, plus italic 400
- **Hanken Grotesk** 400/500/600
- **JetBrains Mono** 400/500
- Scale:
  - H1: clamp(52, 8.5vw, 136)
  - Section H2: clamp(44, 6vw, 96)
  - Secondary H2: clamp(40, 5vw, 72)
  - Statements: clamp(28–30, 3.2–3.6vw, 46–52)
  - Card titles: 26–36
  - Body: 16–24
  - Labels: 11–17

**Radii:** 2 (Gantt bars), 8 (HUD, card images), 10 (panels, small icon tiles), 12 (case cards), 14 (feature panels), ≈22% (logo tile), 999 (pills).

**Spacing:** section padding 12vh / 16vh. Common gaps: 14, 24, 32, 40, 48, 64, 96 px.

**Shadows:** none. Depth comes from translucency and the background.

## Assets
- `logo/`:
  - `groundstate-logo-for-dark-bg.png` and `groundstate-logo-for-white-bg.png`: the plain-mark lockup, 1698×360, transparent background.
  - `groundstate-mark-for-dark-bg.png` and `groundstate-mark-for-white-bg.png`: the G alone, 1024², transparent background.
  - `groundstate-icon-dark-tile.png` and `groundstate-icon-white-tile.png`: the app icon, 1024².
  - The site uses the **app-icon** lockup, so build the header and footer logo from the SVG paths above rather than the PNGs.
- `images/`: original abstract case-study artwork, 1600×1000: `cs-call-qa.png`, `cs-enterprise-intel.png`, `cs-ai-enablement-orbit.png`. Replace with approved, sanitized screenshots if available.
- Portraits for Keith Hanson and Jason Ingalls: still to be supplied.

## Files
- `GroundState Site.dc.html`: the full design reference (markup and logic).
- `support.js`, `image-slot.js`: prototype runtime only; not needed in production. Use normal `<img>` tags instead of image slots.
- `logo/`, `images/`: assets.

## Current visual implementation

The shipped `index.html` and editable `GroundState Site.dc.html` are intentionally identical.

- The dark control-room palette, Newsreader/Hanken Grotesk pairing, teal ground signal, and orange diagnostic accents remain the visual direction.
- Desktop section spacing uses a 128px rhythm; the compact proof strip uses 64px. Mobile sections use 64px, with explicit hero and closing-CTA spacing.
- Navigation and micro-labels use sentence case with restrained tracking. Italics are not used as an emphasis system.
- The system-state HUD is hidden. The ground-plane canvas redraws on load, resize, and scroll rather than running a continuous decorative animation.
- Card surfaces use solid `#14171A` with quiet hairlines. Booking links have explicit hover transitions, and interactive elements have visible keyboard focus rings.
