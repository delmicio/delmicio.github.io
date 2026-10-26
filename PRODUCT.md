# Product

## Register

brand

## Users

Three audiences land here from a LinkedIn click, a GitHub click, or a recruiter handoff, and the page has to win all three in under two minutes of scanning.

- **Engineering managers and tech leads** vetting Emanuel for senior PHP/Laravel work, mostly at education or reliability-critical platforms. They read the bullets, look for production specifics (real systems, real tools, real outcomes), and want to feel a calm collaborator behind the writing.
- **Non-technical hiring managers and recruiters** scanning for keywords, role titles, years of experience, location, and language. They skim; the page has to surface the facts without forcing them to.
- **Direct clients evaluating a freelance or contract Laravel engagement.** They want trust signals (someone who has done this before, who won't break their platform) and outcomes that translate to their problem.

Job to be done across all three: in under two minutes, decide *"is this person worth a conversation?"* and have an obvious way to send that message.

## Product Purpose

A personal portfolio for Jesus Emanuel Aguirre, senior PHP / Laravel developer based in Valencia, that earns inbound "let's talk" replies for senior contract or full-time roles, especially around education platforms, performance, and platform reliability.

Success isn't traffic; it's a qualified email landing in `aguirre@emanuel.com.ar` (or a LinkedIn DM) from someone the page just convinced. Failure isn't ugliness; it's mid-tier reliability writing wearing a 2026 AI portfolio template, indistinguishable from a hundred other warm-cream-and-serif developer sites.

## Brand Personality

Three words: **specific, lived-in, calm.**

- **Specific.** Every number, project, integration, and tool is real and named. "Open English, 900ms → 250ms, Blackfire, query optimization, caching during the Laravel migration" beats "performance optimization expert." The page never lapses into generic claim language.
- **Lived-in.** Written like a senior engineer who has actually shipped this code, mentored these teams, and absorbed these incidents, not like a resume template. First-person voice. Project anecdotes welcome. Small signs of taste are good; corporate-restrained "delivered solutions" voice is not.
- **Calm.** Confidence through restraint, not noise. Reads as *"I've been here before"*, not *"look how hard I work."* No agency theatrics; no SaaS hero metric template; no shouting display type.

Warm and human, more than the current surface manages. Warmth is carried by **copy voice, typography choice, accent colour usage, and small considered details** — *not* by drifting back into the warm-neutral cream body background that lands in the saturated AI cliché.

## Anti-references

These are the failure modes specific to *this* surface. The first is the strongest signal: the current `index.html` is itself drifting into it, which means live-mode variants are explicitly allowed to depart from the present aesthetic.

- **The cream-on-cream warm minimal AI cliché.** Warm near-white body (`#fafaf6` and the entire `OKLCH L 0.84-0.97, C < 0.06, hue 40-100` band), big italic display serif headline (`Instrument Serif` em-tagged accent words), small monospace tracked uppercase eyebrows above every section, restrained-to-the-point-of-bland palette, no real images. The current site sits inside this lane. Future variants on this site should be readable as "warm and human" *without* leaning on warm body backgrounds; let warmth come from accent commitment, voice, typography choice, and small details.
- **Agency overdesign.** Scroll hijacking, parallax, look-at-me WebGL, oversized first-load motion, "I taught myself After Effects" energy. Personality must not arrive via motion theatrics; this site sells a calm, reliable engineer.
- **Bootstrap / LinkedIn-clone resume template.** Default chronological resume layout, blue underlined links, off-the-shelf card grids, "Skills" bullet list with progress bars, no point of view. The opposite trap from the cream cliché: bland by laziness rather than bland by reflex.

## Design Principles

1. **The site itself is the portfolio piece.** Production-first thinking has to be visible in the surface, not just claimed in the copy. Fast first paint, low layout shift, no broken state, real focus rings, real keyboard nav, real reduced-motion fallback. Practice what the bullets preach.
2. **Show specific work, not categories.** Replace abstract claims with named systems, named tools, named outcomes. "Cut home-dashboard from 900ms to 250ms with Blackfire profiling and strategic caching" stays; any drift toward "performance optimization expert" gets cut.
3. **Voice over template.** First-person, specific, with character. The reader should hear a single engineer, not a CV. Buzzwords (`leverage`, `streamline`, `seamless`, `enterprise-grade`, `next-generation`) are out. Em dashes are out (use commas, colons, periods).
4. **Calm confidence, not corporate restraint.** Quiet is allowed; bland is not. Restraint must read as a signature, not as a training-data reflex. When in doubt, commit further to one strong move (one accent colour, one strong type pairing, one clear hierarchy) rather than hedging in the safe zone.
5. **Bilingual symmetry (EN ↔ ES).** Spanish is not a translation afterthought; it's an equal first surface for direct LATAM and Spain clients. Anything added to EN must land in ES the same day, with the same voice. The i18n dual-dictionary invariant in `CLAUDE.md` is the contract.

## Accessibility & Inclusion

- **WCAG 2.2 AA** as the floor. Body text ≥ 4.5:1 against its background; large text (≥18px or bold ≥14px) ≥ 3:1. The current muted-grey `--text-2` on warm cream sits around 6.5:1 in light mode; future variants that introduce tinted backgrounds need re-verification before shipping.
- **Reduced motion is non-negotiable.** Every animation (current and future) needs a `@media (prefers-reduced-motion: reduce)` fallback — typically a crossfade or instant transition. The existing `IntersectionObserver` reveal already degrades to "always visible" when IO is missing; preserve that fallback shape for new motion.
- **Keyboard and focus.** Visible focus rings on every interactive element (nav, language toggle, theme toggle, buttons, links). Skip-link already exists; keep it.
- **Language parity.** EN/ES translation parity is an accessibility concern, not just a marketing one. Missing keys in `translations.es` fail silently and ship the English string to a Spanish-language reader; the CLAUDE.md invariant is load-bearing.
- **Light and dark themes.** Both must hit AA. The existing dark mode (`OKLCH`-equivalent `#0a0a0a` body with `#fb923c` accent) needs the same contrast verification as light when variants change either token.
