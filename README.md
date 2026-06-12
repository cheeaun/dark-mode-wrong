# You’re doing dark mode wrong.

A one-page site about the most common dark-mode bug on the web: the two-state theme toggle.

**The thesis:** a theme control needs three states — **Light · Auto · Dark** — with Auto (follow the system) as the default. Storage holds overrides only: no stored key *is* the Auto state.

## Why two states aren’t enough

- `prefers-color-scheme` has carried the user’s answer since 2019 — a toggle that defaults to light ignores it
- Operating systems switch themes on a schedule (sunset, sunrise, battery saver); a stored binary value can never follow
- One click on a two-state toggle stores an override forever — there is no way back to “follow my system”
- Theme is an accessibility signal (photophobia, migraines, astigmatism halation), not just a preference

## The pattern

Three pieces, each with copy-pasteable code on the page:

1. **Head** — `<meta name="color-scheme" content="light dark">` plus a tiny inline blocking script that applies a stored override before first paint, so there is no theme flash
2. **CSS** — `color-scheme: light dark` on `:root`, narrowed by `[data-theme]`; every color via `light-dark()` (Baseline 2024; classic `prefers-color-scheme` fallback included)
3. **JS** — radio buttons for Light / Auto / Dark; `localStorage` written only for explicit choices, `removeItem` on Auto; a `matchMedia('(prefers-color-scheme: dark)')` listener for everything CSS can’t reach

## The page demonstrates itself

- Defaults to Auto and follows OS appearance changes live, mid-session, no reload
- Stores exactly one localStorage key — and only when you override
- Works with JavaScript disabled: the toggle hides itself and Auto still works
- Respects `prefers-reduced-motion` and `prefers-contrast: more`
- A live “under the hood” table shows the page’s real internals as they change
- One HTML file — no build step, no frameworks, no analytics; even the syntax highlighting is baked into the markup

## Run it

Open `index.html` in a browser. That’s all.

## Reading

Start with these — the full, link-checked list is on the page:

- [Your dark mode toggle is broken](https://kilianvalkhof.com/2020/design/your-dark-mode-toggle-is-broken/) — Kilian Valkhof
- [The Quest for the Perfect Dark Mode](https://www.bram.us/2020/04/26/the-quest-for-the-perfect-dark-mode-using-vanilla-javascript/) — Bramus Van Damme
- [`prefers-color-scheme`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@media/prefers-color-scheme) and [`light-dark()`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/color_value/light-dark) — MDN

---

Set in [Fraunces](https://fonts.google.com/specimen/Fraunces), [Newsreader](https://fonts.google.com/specimen/Newsreader) & [Spline Sans Mono](https://fonts.google.com/specimen/Spline+Sans+Mono). The implementation is free to copy.
