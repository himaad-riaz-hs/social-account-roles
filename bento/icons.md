# Bento — icon inventory

Two independent, non-identical icon systems ship in this project. Do not
merge them into one list — they have different formats, different call
sites, and different coverage.

## 1. Material Symbols Outlined (the primary icon system)

**This is what nearly every component uses.** It is Google's icon webfont,
loaded once per page:

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0..1,0..200&display=block">
```

Rendered as text content inside a span carrying the base rule from
`components/components-base.css`:

```html
<span class="material-symbols-outlined">calendar_today</span>
```

- **Weight 400, optical size 24, `FILL 0` by default.** `FILL 1` only for
  active/selected state (a checked checkbox glyph, the selected rail icon,
  a filled reaction). Toggle it with an inline
  `font-variation-settings:"FILL" 1` or the `.hs-badge .material-symbols-outlined`
  / `.is-active …` rules already written for you in components-ext.css.
- **In-app sizes:** 16 / 20 / 24 / 28px, plus 32px for the single glyph in an
  empty state or file-drop zone (`--bento-theme-icon-{sm,md,lg,xl}`).
- **This webfont is open-ended** — Google ships several thousand named
  glyphs, and any valid glyph name renders. This project does not, and
  cannot, enumerate "every icon name available": there is no closed list
  shipped in the kit, no bundled subset file, and no build step that
  restricts which names resolve. **Do not treat the list below as exhaustive**
  — it is the set of names this project's own components and templates were
  found to actually call.

### Names verified in use in this project (grep across `components/**/*.jsx`)

add · account_circle · arrow_back · arrow_upward · auto_awesome · bar_chart ·
bolt · calendar_month · check · check_box · check_box_outline_blank ·
check_circle · close · content_copy · delete · edit · edit_note ·
error · expand_less · expand_more · format_bold · gpp_good · graphic_eq ·
grid_view · groups · image · inbox · indeterminate_check_box · info ·
keyboard_arrow_down · link · more_horiz · notifications_none · open_in_new ·
radio_button_checked · radio_button_unchecked · schedule · send · star ·
view_list · warning

Five of these are **hard-coded as literal glyph code points** inside
`components-base.css` (not loaded by name at all — they are drawn via
`::before { content: "\eXXX" }` so the checkbox/radio visual works even if
the name-based lookup ever changed):

| Glyph | Code point | Used for |
|---|---|---|
| `check_box_outline_blank` | `\e835` | checkbox, off |
| `check_box` | `\e834` | checkbox, on (`FILL 1`) |
| `indeterminate_check_box` | `\e909` | checkbox, mixed (`FILL 1`) |
| `radio_button_unchecked` | `\e836` | radio, off |
| `radio_button_checked` | `\e837` | radio, on (`FILL 1`) |

## 2. Brand & network marks — TWO overlapping, not-identical sources

Material Symbols has no brand marks, so Bento ships real SVGs for those —
but as **two separate deliverables that were built independently and do not
fully overlap**. Treat them as two sources, not one "icon set."

### 2a. `assets/icons/*.svg` — 6 flat files
```
assets/icons/facebook.svg
assets/icons/instagram.svg
assets/icons/linkedin.svg
assets/icons/pinterest.svg
assets/icons/tiktok.svg
assets/icons/youtube.svg
```
Plain flat SVG files. Use directly: `<img src="assets/icons/instagram.svg" alt="Instagram">`,
or inline the markup and set `fill: currentColor`. No accompanying component
or class — you own how you mount them.

### 2b. `components/icons/Icon.jsx` + `icon-data.js` — 27 named marks
A React component reading path data out of a generated data module:

```jsx
<Icon name="Instagram" />                          {/* disc in inherited text color */}
<Icon name="Instagram" style={{color:"#E1306C"}} /> {/* disc in a brand color you supply — Bento ships no brand hexes */}
<Icon name="Instagram" mono />                      {/* glyph only, no disc */}
```

All 27 names, verbatim:

```
Amplify · Apple · Dot · Empty · Facebook · FacebookPage · GitHub · Google ·
Happy · Hootsuite · InWeb · Instagram · Line · LinkedIn · Mailgun ·
Messagebird · Paypal · Pinterest · Sad · Telegram · Tiktok · Twilio ·
Viber · WeChat · Whatsapp · X · Youtube
```

- Each mark is drawn as `path` elements with `fill="currentColor"`; the CSS
  in `components-ext.css` (`.hs-icon`) restores a two-tone disc-and-glyph
  look for the 21 marks that have a backing disc. Six (`Amplify, Apple, Dot,
  Empty, Happy, Sad`) are flat, single-tone marks — passing `mono` on those
  is a no-op.
- **Overlap with 2a is partial, not 1:1.** `Facebook`, `Instagram`,
  `LinkedIn`, `Pinterest`, `Tiktok`, `Youtube` exist in *both* sources (as a
  flat file AND as an `Icon.jsx` name) — nothing enforces that the two stay
  pixel-identical, since they were produced by different pipelines
  (fig-materialize export vs. hand-copied asset). `WhatsApp`, `WeChat`,
  `Viber`, `Telegram`, `Line`, `Messagebird`, `Mailgun`, `Twilio`, `Google`,
  `GitHub`, `Paypal`, `Apple`, `Hootsuite`, `Amplify`, `FacebookPage`, `InWeb`,
  `Happy`, `Sad`, `Dot`, `Empty`, `X` exist **only** in `icon-data.js`, with
  no flat-file equivalent. If your build can't run the `<Icon>` React
  component, you only have the 6 flat files — the other 21 marks are not
  otherwise available as static assets in this export.

## Rendering decision for engineers

- Any UI glyph that is **not** a brand/network mark → Material Symbols
  Outlined, by name, per the sizing/FILL rules above.
- A **brand or network mark** → `<Icon name="…">` (21 of the 27 names have
  no other source) if you can run the React component; otherwise the 6 flat
  files in `assets/icons/` for exactly those 6 networks, and know the
  other 21 are unavailable as static files in this export.
- Never use an emoji or a Unicode glyph as a UI icon (Bento rule, enforced
  nowhere in code — it is a content guideline, not a lint rule).
