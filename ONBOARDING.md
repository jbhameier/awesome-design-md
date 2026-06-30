# Handoff: turn the "Your Goal" screen into a reusable mobile UI component library

## What this is

A pixel-faithful onboarding/results screen (calorie + macro goal) was recreated as a
single static HTML/CSS file, then reskinned into the **B2B Rocket** identity
(white + periwinkle). Your job: turn it into **working, reusable components** that fit
the B2B Rocket frontend, with the two color schemes expressed as a swappable **theme**.

- **Source of truth (design):** `nutrition-goal-screen/index.html` on branch
  `claude/exact-recreation-vhcxso` of `jbhameier/awesome-design-md`.
  Self-contained: Poppins is inlined as `@font-face` woff2 data URIs; all SVGs are inline.
- **Visual reference (rendered):** the screen renders identically offline — open the file
  in a browser, or compare against the published artifact you were given the link to.

## Step 0 — match the host stack BEFORE writing any component

You are (or should be) working inside the B2B Rocket frontend repo (the codebase behind
`app.b2brocket.ai`). Do this first:

1. Read `package.json` + the existing component directory. Detect framework (React/Next?),
   styling (Tailwind? CSS Modules? styled-components?), and the component/file conventions.
2. **Mirror those conventions exactly.** Place components where the project puts components,
   match its naming, import style, and test setup.
3. Only if the target is greenfield/unspecified, use this default: **React 18 + TypeScript**,
   **Tailwind CSS** with the tokens below wired into `theme.extend`, components as function
   components with typed props. Fonts via `@fontsource/poppins` (weights 500/600/700).

Do not hand-port the raw HTML. Decompose into the components in the inventory below.

## Design tokens (theme-swappable)

The screen must support both themes via a single `theme` prop / CSS-variable set. Keep
semantic names; only the values change between themes. Protein (blue) and Fat (orange) are
**data colors** — they stay constant across themes; only `accent` moves.

| Token            | B2B Rocket (default) | Original "lime" theme |
|------------------|----------------------|-----------------------|
| `--panel`        | `#ffffff`            | `#1a241e` (dark)      |
| `--ink`          | `#16181f`            | `#f4f7f1`             |
| `--muted`        | `#8d909c`            | `#8d978b`             |
| `--accent`       | `#6763d7`            | `#cdf24c`             |
| `--accent-soft`  | `#7d78e4`            | `#d7f55e`             |
| `--on-accent`    | `#ffffff`            | `#162018`             |
| `--accent-glow`  | `rgba(103,99,215,.30)` | `rgba(205,242,76,.22)` |
| `--card`         | `#f6f6fc`            | `rgba(232,240,218,.045)` |
| `--track`        | `#e9e8f6`            | `rgba(232,240,218,.10)` |
| `--data-protein` | `#4fa9e8`            | `#4fb3e3`             |
| `--data-fat`     | `#f0a23d`            | `#f0a23d`             |

Corner ambiance: a radial bloom in `--accent` at the top-right (and a fainter one top-left)
behind the heading, plus a faint concentric ring. In the B2B theme these are pale lavender
(`#b9b2f0`→transparent); in the lime theme they were olive/lime.

Type: **Poppins**. Heading 24px/700 centered; "Your Goal" 23px/700; body 14.5px/500;
calorie number 31px/700; macro label 17px/600; values 16px/500 tabular-nums; button 19px/700.
Radii: screen 46, callout 26, card 28, button 40 (px). Phone content padding 30/26/26.

## Component inventory (build these, props-driven)

1. **`ScreenFrame`** — rounded panel + corner-bloom background + concentric ring.
   Props: `theme`. Slots children. Owns the CSS variables for the active theme.
2. **`TopBar`** — `BackButton` (circular, accent-tinted, accent chevron) + **`ProgressDots`**
   (`steps`, `current`; inactive = accent@22%, active = elongated accent pill).
3. **`Heading`** — centered display text; `children`. (Allow an explicit line break.)
4. **`GoalCallout`** — accent-filled speech bubble with downward tail + falling "crumb" dots.
   Props: `icon` (defaults to the flag-on-hill SVG), `title`, `children`. Text/icon use
   `--on-accent`. The tail + crumbs are positioned decorations — keep them as part of this
   component so it stays a drop-in.
5. **`MacroRing`** — circular ring (SVG, stroke = `--accent`) with centered `value` + `unit`.
   Props: `value`, `unit`, optional `progress` (0–1) if you want a partial arc later; the
   current design is a full ring.
6. **`MacroBar`** — label + right-aligned value + track/fill bar. Props: `label`, `value`,
   `percent`, `color` (`'accent' | 'protein' | 'fat'`). Carbs uses `accent`.
7. **`PrimaryButton`** — full-width pill, `--accent` bg, `--on-accent` text, accent glow.
   Props: `children`, `onPress`/`onClick`. Visible focus ring; respect reduced-motion.

Compose them into a **`GoalScreen`** that takes the data (kcal, macros array, goal copy,
date) as props so it isn't hard-coded.

## Assets

- **Flag-on-hill icon:** inline SVG in the source (`.goal .icon svg`, viewBox `0 0 100 100`).
  Recolor via `currentColor`/`fill` so it inherits `--on-accent`. Extract to an `Icon` component.
- **Poppins:** weights 500/600/700, latin subset (`@fontsource/poppins` on npm — already
  used; ~8KB/weight woff2). Do not link Google Fonts (CSP/offline).

## Acceptance criteria

- [ ] `GoalScreen` renders pixel-faithful to the source file in the B2B theme.
- [ ] Switching `theme` to `"lime"` reproduces the original dark/lime look with no other code changes.
- [ ] Every component is reusable in isolation with typed props and no hard-coded copy/data.
- [ ] No external network deps at runtime (fonts inlined/bundled).
- [ ] Keyboard focus states visible; `prefers-reduced-motion` respected.
- [ ] Matches the host repo's lint/test/format conventions.

## How to verify

Render `GoalScreen` and compare side-by-side with `nutrition-goal-screen/index.html`
(open it in a browser). Spot-check radii, the accent glow position, the macro bar fills
(protein ~72%, carbs 100%, fat ~96%), and the callout tail/crumb placement.
