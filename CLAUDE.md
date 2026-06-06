# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

Personal portfolio for Emanuel Aguirre, deployed via GitHub Pages from `main` to the custom domain `emanuel.com.ar` (set in `CNAME`). The entire site is a single self-contained `index.html` (~1860 lines) with inline `<style>` and `<script>` blocks — no build step, no package manager, no framework, no separate asset files. The favicon is embedded as base64 in the `<link rel="shortcut icon">`.

## Local development & deploy

- Preview locally with any static server from the repo root, e.g. `python3 -m http.server 8000` then open `http://localhost:8000`.
- There are no install/build/lint/test commands. Editing `index.html` and reloading the browser is the dev loop.
- Deployment: `git push origin main`. GitHub Pages serves `main` directly; the `CNAME` file (contents: `emanuel.com.ar`) is what binds the custom domain — do not delete it.

## Architecture — three systems inside one file

These are the parts that require reading code in multiple locations and are easy to break in isolation.

### 1. i18n (EN / ES) — dual-dictionary invariant

Translation is custom and lives entirely in the bottom `<script>` block (around lines 1553–1856).

- Markup elements opt in with `data-i18n="some.key"`. Add `data-i18n-html` alongside it when the translated string contains HTML (e.g. `<em>`, `<span class="card-arrow">`); without that flag the script uses `textContent` and the tags will render as literal text.
- Translations live in a single `translations` object with two top-level keys: `en` and `es`. **Any new `data-i18n` key added to the markup MUST be added to BOTH `translations.en` and `translations.es`.** Missing keys are silently ignored (`if (dict[key] === undefined) return;`), so a forgotten Spanish entry will fall through to whatever HTML is hard-coded in the markup — which is usually the English copy.
- Initial language is resolved in the very early inline `<script>` in `<head>` (reads `localStorage.lang`, falls back to `navigator.language` starting with `es`). It sets `<html data-lang>` and `<html lang>` before paint so SSR-equivalent state is correct on first render.
- `applyTranslations(lang)` also updates `document.title`, `meta[name="description"]`, `og:title`, and `og:description` via the `meta.title` / `meta.description` keys — keep those in sync when changing the headline copy.

### 2. Theming (light / dark)

- All colors are CSS custom properties defined twice: under `:root` (light defaults) and under `[data-theme="dark"]` (dark overrides). A third block, `@media (prefers-color-scheme: dark) :root:not([data-theme="light"])`, mirrors the dark overrides so system dark mode works when the user hasn't made an explicit choice. **When adding a new color token, update all three blocks** or dark mode / system-dark will silently fall back to the light value.
- The early inline `<script>` in `<head>` reads `localStorage.theme` and sets `<html data-theme>` before paint to avoid a flash of wrong theme. Don't move this script lower or add async/defer to it.
- The theme toggle resolves the "current" theme by combining the `data-theme` attribute with `prefers-color-scheme`, so toggling from the system default flips to the opposite of the system preference.

### 3. Scroll behavior (reveal + nav scroll-spy)

The bottom `<script>` sets up two `IntersectionObserver`s:

- Reveal animations: any element with `data-animate` gets `.is-visible` added once it intersects. The CSS for `[data-animate]` controls the initial hidden state and the transition. There is a no-IO fallback that just sets `.is-visible` on everything — keep it; older browsers and reduced-motion test harnesses rely on it.
- Nav scroll-spy: `main section[id]` are observed with `rootMargin: '-40% 0px -55% 0px'` so the active section is roughly "what's centered in the viewport." The matching `.primary-nav a[href="#id"]` gets `.is-active`. New top-level sections must have an `id` and a corresponding nav link to participate.

## Conventions worth preserving

- Section eyebrows are numbered (`01 — About`, `02 — Experience`, …). Renumber consistently across both languages if you add or remove sections.
- The CSS uses unicode box-drawing dividers in comments (`/* ───── Header ───── */`) — match that style when adding new sections so the file stays scannable.
- Headlines that contain accented words wrap them in `<em>` and rely on `.section-title em`, `.hero-headline em`, etc. styling them with the accent color and italic display font (`Instrument Serif`). When translating, keep the `<em>` around the equivalent word and remember to mark the element with `data-i18n-html`.
- External links use `rel="noopener"`. Personal-handle links currently point to `github.com/delmicio`, `linkedin.com/in/ema-dev`, and `mailto:aguirre@emanuel.com.ar`.
