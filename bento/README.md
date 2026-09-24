# Bento (Hootsuite design system) — engineering export

Source: **Official Bento — Hootsuite Design System**, HS-Bento gallery
snapshot, Aug 2026, from DX. This export is a build handoff: real token
files, the real `.hs-*` class library, a component gallery, an icon
inventory, and a standard app-shell skeleton — copied and re-documented,
nothing re-authored from scratch and nothing invented. Where the system
itself has a gap, it is called out below rather than filled in.

## Files

| File | What |
|---|---|
| `tokens.css` | Single import point over `tokens/*.css` (copied verbatim). Grouped, commented, states the real theme-switching mechanism (see "Known gaps"). |
| `tokens/*.css` | The unmodified source: `colors.css`, `typography.css`, `layout.css`, `fig-tokens.css`, `aliases.css`, `chart-alias.css`. |
| `components.css` | Single import point over `css/components-base.css` + `components-ext.css` + `fig-typography.css` (copied verbatim, 1,540 lines combined; folder named `css/`, not `components/`, to avoid a stem collision with this file). |
| `components.html` | Gallery: every component below, in every state its CSS actually defines, plain HTML, class names visible under each example. |
| `icons.md` | Full icon inventory: Material Symbols usage + the two brand-mark SVG sources, with their real overlap/gap. |
| `shell.html` | Standard app shell — rail, banner, nav drawer, content — built from the real `.hs-rail` / `.hs-suite-banner` / `.hs-navdrawer` / `.hs-header` classes, with real pixel measurements in comments. |
| `assets/` | Copied brand mark + the 6 flat network SVGs referenced by `icons.md`. |

## Component → class → file map

Grouped by the Confluence Components-hub category, matching the design
system's own coverage table. "Class" is the top-level class you mount;
each also has nested/state classes documented inline in `components.css`'s
import comments and shown live in `components.html`.

| Component (Confluence) | Top-level class(es) | Defined in |
|---|---|---|
| Button | `.hs-btn` (`--primary/secondary/outlined/ghost/icon/sm`) | css/components-base.css |
| Icon button | `.hs-btn--icon` · overlay: `.hs-ovly-icon` | components-base.css / -ext.css |
| Split button | *(no dedicated class shipped — compose `.hs-btn` + a chevron; see "Known gaps")* | — |
| Button info | `.hs-info` | components-ext.css |
| Badge | `.hs-badge` (`--neutral/positive/warning/negative/discovery/info/square/dot/interactive`) | components-base.css |
| Avatar | `.hs-avatar` (`--xs/sm/md/lg/xl`) | components-base.css |
| Avatar stack | `.hs-avatar-stack` | components-ext.css |
| Card surface | `.hs-card` (`--quiet`) | components-base.css |
| Panel | `.hs-panel` (`--bare`) | components-ext.css |
| Tooltip | `.hs-tooltip-wrap` / `.hs-tooltip` (`--top/bottom/left/right`) | components-ext.css |
| Spinner | `.hs-spinner` (`--inverse`) | components-ext.css |
| Hyperlink | `.hs-link` | components-ext.css |
| Chip | `.hs-chip`, chip filter: `.cf` (`.open/.selected/[disabled]`) | components-base.css |
| Chip assist | `.hs-chip-assist` | components-ext.css |
| Tag | `.hs-input-tag`, list: `.hs-tag-list` / `.hs-chip-list` | components-base.css / -ext.css |
| Input-text | `.hs-input` (`--error`) inside `.hs-field` (`-label/-desc/-hint`) | components-base.css |
| Input-search / -password / -payment | `.hs-input` + markup pattern; payment: `.hs-input-payment` | components-base.css / -ext.css |
| Textarea | `.hs-textarea`, counter `.hs-char-count` | components-base.css / -ext.css |
| Control-checkbox | `.hs-check` (`.is-on/.indeterminate/.is-disabled`) — see "Known gaps" | components-base.css |
| Control-radio | `.hs-radio` (`.is-on`) | components-base.css |
| Control-switch | `.hs-toggle` (`.is-on`) | components-base.css |
| Control-stepper | `.hs-stepper` | components-ext.css |
| Select | `.hs-select` (`.focused/[disabled]`) | components-base.css |
| Combobox / Tree select | `.hs-tree-select` (`-trigger/-menu/-row/…`) | components-ext.css |
| Date picker | `.hs-cal-grid` / `.hs-cal-day` (`--muted/today/range/selected`) | components-ext.css |
| Time picker | `.hs-tp-input` / `.hs-tp-opt`, `.hs-time-input` / `.hs-time-seg` | components-ext.css |
| Profile picker | `.hs-profile-picker` | components-ext.css |
| File uploader | `.hs-uploader`, uploaded row `.hs-file-row` | components-ext.css |
| Form control (Field/Hint) | `.hs-field`, `.hs-control-list` / `.hs-control-row` | components-base.css / -ext.css |
| Label | `.hs-label-row` (`-req/-opt`) | components-ext.css |
| Alert / banner / toast | `.hs-alert` (`--positive/warning/negative`) | components-base.css |
| Notification / Snackbar | `.hs-snackbar` (undocumented on Confluence — see coverage note in the design-system guide) | components-ext.css |
| Progress (bar/stepped) | `.hs-progress` (`--sm/lg`), `.hs-steps` | components-ext.css |
| Progress listed | `.hs-listed-progress` / `.hs-listed-step` (`--active/done`) | components-ext.css |
| Skeleton | `.hs-skeleton` (`--circle/text`) | components-ext.css |
| Feedback status / empty state | `.hs-empty` | components-ext.css |
| Tabs | `.hs-tabs` / `.hs-tab` (`.is-active`) | components-base.css |
| Accordion | `.acc-list` (`--outline`) / `.acc-item` (`.open/.disabled/.compact`) | components-base.css |
| Breadcrumb / Pagination | *(no dedicated class found in either CSS file — see "Known gaps")* | — |
| Header / sub-header | `.hs-header` (`--flush`) / `.hs-subheader` | components-ext.css |
| Main nav (Suite rail) | `.hs-rail` (`-brand/-group/-item/-glyph/-label`) | components-ext.css |
| Navigation drawer | `.hs-navdrawer` (`-head/-title/-body/-item/-section/-footer`) | components-ext.css |
| Suite banner | `.hs-suite-banner` (`--stack`) | components-ext.css |
| Bottom nav bar (mobile) | `.hs-mobile-navbar` (`-item/-inner/-hint/-counter`) | components-ext.css |
| Button docked / bottom sheet (mobile) | `.hs-mobile-sheet-action` / `.hs-mobile-sheet-bottom` | components-ext.css |
| Action bar | `.hs-action-bar` (`--floating/outlined`) | components-ext.css |
| Menu button / Dropdown menu | `.hs-menu` / `.hs-menu-item` (`-sep/-label`), `.hs-dd-item`, `.hs-submenu` | components-ext.css |
| Modal | `.hs-modal` — see "Known gaps" (elevation) | components-ext.css |
| Drawer | `.hs-drawer` (`-header/-body`) | components-ext.css |
| Popover | `.hs-popover` (undocumented on Confluence) | components-ext.css |
| Table | `.hs-table` (+ `.hs-table-wrap/-bulkrow/-selectall/-result/-emptyrow`, `tr.is-selected`) — see "Known gaps" | components-ext.css |
| Thumbnail | `.hs-thumb` | components-ext.css |
| List item / Listbox | `.hs-list-item`, `.hs-option` (listbox row) | components-ext.css / -base.css |
| Link preview | `.hs-link-preview` (`-media/-body`) | components-ext.css |
| Toggle group / Display toggle | `.hs-toggle-group` | components-ext.css |
| Carousel | `.hs-carousel` | components-ext.css |
| Media / message media | `.hs-msg-media` (`--mine`) | components-ext.css |
| Conversation | `.hs-conversation` (`-day`), bubbles `.hs-msg` (`--in/out`) | components-ext.css |
| Emoji button / reaction | `.hs-emoji-btn`, `.hs-reaction` (`.is-selected`), `.hs-reaction-group`, picker `.hs-emoji-cat`/`.hs-emoji-cell` | components-ext.css |
| Overlay display (media) | `.hs-ovly` (`--filled/ghost/icon/inverse`) | components-ext.css |

**Not found as a dedicated class in either CSS file**, despite appearing on
the design system's own component list: **Split button**, **Breadcrumb**,
**Pagination**, **Combobox** (only its Tree-select sibling is styled),
**Option-trigger** (`.hs-option-trigger` exists, but there is no distinct
Combobox trigger class), **ButtonChoice** (`.hs-choice` exists and covers
it), **CardPost**, **CalendarCard** (`.hs-cal-card` exists — this one *is*
covered, listed here only because it's easy to miss), **Tree** (`.hs-tree`
exists as a bare root — no `.hs-tree-row` indent/expand chevron rule beyond
what's shown). If your build needs one of the genuinely missing ones
(Split button, Breadcrumb, Pagination, Combobox-proper), that is new CSS to
write, not a lookup you missed here — both files were read in full for this
export.

## Known gaps

Three specific questions, answered from reading the actual component source
(`.jsx`) and the actual CSS, not from the documentation prose:

### 1. Is Control-checkbox a real keyboard-accessible checkbox control, or only a checkbox visual?

**Neither, cleanly — it's a real custom widget, not a native input, and not
a static picture either.** `Checkbox.jsx` and `Table.jsx`'s row/select-all
checkboxes both render:

```html
<span class="hs-check is-on" role="checkbox" aria-checked="true"
      tabindex="0" onClick="…" onKeyDown="…"></span>
```

That *is* operable from the keyboard: it's in the tab order (`tabIndex={0}`,
or `-1` when disabled), it has `role="checkbox"` and `aria-checked`
(including `"mixed"` for indeterminate), and the component's own `onKeyDown`
handler treats Space and Enter as activation and calls
`e.preventDefault()` so Space doesn't also scroll the page. The visual glyph
itself is drawn in pure CSS — `.hs-check::before` — as a Material Symbols
character (`check_box_outline_blank` / `check_box` / `indeterminate_check_box`),
not an image or a static square.

What it is **not**: a native `<input type="checkbox">`. That means:
- No native form participation — it won't submit a value with a
  surrounding `<form>`, has no `name`/`value`/`checked` DOM property, and
  browser autofill/form-validation APIs don't see it.
- No `:checked` CSS pseudo-class to hook into from outside this component.
- No native `<label for>` association — `Checkbox.jsx`'s optional label is
  a `<label>` that *wraps* the control, which works, but only because the
  component builds it that way every time; a label written separately
  elsewhere won't associate with the control unless you replicate that
  wrapping.
- It depends entirely on the ARIA role + manual key handling staying
  correct; there is no browser-native fallback if either is ever dropped
  from a future edit.

Confluence's own Control-checkbox page (`11909988353`) documents no states
at all, including no indeterminate state — the indeterminate handling shown
above is this project's own addition, not a spec it followed.

### 2. Is bulk row-selection styling reusable outside its own table class, or trapped inside it?

**Mostly reusable — the action bar is a standalone class; the selected-row
tint is not.** Two different things both get called "bulk selection," and
they land differently:

- **The bulk action bar itself — reusable.** `.hs-bulk-bar` (the pill that
  says "2 selected" plus action buttons) is defined as its own top-level
  rule in `components-ext.css`, with no ancestor selector requiring a
  table. `Table.jsx` renders it by importing the *separate* `BulkActionBar`
  component (`components/navigation/BulkActionBar.jsx`) and dropping it into
  a `<tr class="hs-table-bulkrow"><th colspan>` — the one table-specific
  rule (`.hs-table-bulkrow .hs-bulk-bar`) only strips the bar's own
  border-radius/shadow/max-width so it fits flush in a header cell; the bar
  itself is unchanged. There is also a second, independent reusable wrapper,
  `.hs-bulk-overlay` (from `BulkSelectionOverlay.jsx`), for floating the same
  bar over the bottom of a scrolling list instead of a table. Both are
  legitimately usable in a non-table context with no extra work.
- **The selected-row tint — table-scoped, not reusable as a class.** The
  visual "this row is checked" tint is written as `.hs-table tbody
  tr.is-selected`, i.e. it only fires inside a `<table class="hs-table">`.
  There's no standalone `.is-selected`-for-rows utility class you can drop
  onto a `<div>` list row and get the same tint — you'd have to copy the
  declaration (`background: var(--bento-component-table-selected-fill)`) or
  reuse the *token* rather than the class. (Other components — dropdown
  items, list items, listbox rows — each define their **own**
  `.is-selected` rule scoped to their own class, at their own token; none of
  them share one generic selected-row class with the table.)
- **The checkbox itself is fully reusable.** `.hs-check`/`.hs-radio` are
  the same class Checkbox.jsx and Table.jsx both use, unscoped to any
  container — no gap here.

### 3. Does a confirm-dialog elevation token exist?

**No — Modal reuses the generic overlay shadow token; there is no elevation
tier that distinguishes a confirm dialog (or any modal) from a dropdown
menu.** `.hs-modal` in `components-ext.css`:

```css
.hs-modal{ …; box-shadow: var(--bento-theme-elevation-shadow-overlay-bottom); … }
```

`--bento-theme-elevation-shadow-overlay-bottom` is the *same* token used by
`.hs-menu` (dropdown menus), `.hs-popover`, `.hs-alert-toast`, and
`.hs-snackbar`/`.hs-bulk-bar` (via the identical hand-written value in the
snackbar comment block). Bento's elevation scale
(`tokens/layout.css`) has exactly five shadow tokens total —
`shadow-raised`, `shadow-overlay-top`, `shadow-overlay-bottom`,
`shadow-overflow-{top,bottom,left,right}`, and the drawer-directional
aliases — and none of them is named or scoped for "modal" or "confirm
dialog" specifically. `Modal.jsx`'s own component doc comment says "16px
radius, overlay shadow" — accurate, but it is describing a re-used tier, not
a dedicated one. If your product needs a confirm dialog to read as more
urgent/elevated than a dropdown menu, that visual distinction does not
exist in Bento today and would be new token work, not a lookup.

---

*This export was built by reading the actual `.css`/`.jsx` source in the
attached design-system project, not from its prose documentation alone —
every claim above (including every "not found") was checked against the
file, not inferred from the component list. Where the system's own
documentation and its shipped code disagree (theme scopes in `tokens.css`;
Split button/Breadcrumb/Pagination classes above), the code is what's
exported, and the disagreement is called out rather than silently resolved
in either direction.*
