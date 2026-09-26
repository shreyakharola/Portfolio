# Shreya Kharola — Portfolio

A single-page Angular 19 portfolio built from your resume. Standalone components,
signals, no NgModules, no external UI kit — just plain SCSS and native Angular
control flow (`@if` / `@for`).

## Design concept

A "systems & workflows" theme, grounded in the actual vocabulary of your work
(REST APIs, request/response cycles, status logs) rather than a generic
template look:

- **Hero** — an animated terminal panel that plays out a single `GET` request
  against your own profile, typing out the response line by line on load.
- **Skills** — grouped into the same categories as your resume, laid out as a
  bordered grid rather than repeated identical cards.
- **Experience** — a real chronological timeline (your two MGS projects), with
  earlier internships tucked behind a "show more" toggle so the page doesn't
  get long.
- **Projects** — your final-year Mental Health Tracker is featured larger
  (it's the most technically interesting one); the college website sits below
  as a smaller entry.
- **Education / certifications / co-curricular** — three quiet columns at the
  bottom.
- **Contact** — direct email, phone and LinkedIn links.

Colors: deep ink-navy background, warm amber + muted teal accents (evoking
status lights / log highlighting), off-white text. Type: `Big Shoulders
Display` for headings, `IBM Plex Sans` for body, `IBM Plex Mono` for labels
and the terminal.

Animations are deliberately restrained: one orchestrated sequence in the hero
on load, plus a scroll-reveal (fade + slide up) the first time each section
enters the viewport, via a small reusable `appReveal` directive
(`src/app/directives/reveal.directive.ts`) — no animation library needed.
Everything respects `prefers-reduced-motion`.

## Running it locally

You'll need [Node.js](https://nodejs.org) 18.19+ or 20+.

```bash
npm install
npm start
```

Then open http://localhost:4200.

To build for production (outputs to `dist/portfolio`):

```bash
npm run build
```

The build output in `dist/portfolio/browser` is static HTML/CSS/JS — you can
deploy it to Netlify, Vercel, GitHub Pages, Azure Static Web Apps, or any
static host.

## Where to edit things

Almost all of your content lives in one file:

```
src/app/data/portfolio-data.ts
```

Update `PROFILE`, `SKILL_GROUPS`, `EXPERIENCE`, `INTERNSHIPS`, `PROJECTS`,
`EDUCATION`, `CERTIFICATIONS`, and `HIGHLIGHTS` there — the templates just
render whatever is in this file, so you don't need to touch the HTML to
change wording, add a project, or add a new skill.

Design tokens (colors, fonts, spacing) are in `src/styles.scss` at the top,
under `:root`.

## Structure

```
src/app/
  components/
    nav/          top navigation bar
    hero/         animated terminal hero
    skills/       grouped skills grid
    experience/   timeline + internships
    projects/     featured + secondary project cards
    education/    education / certifications / highlights
    contact/      contact links + footer
  directives/
    reveal.directive.ts   scroll-reveal animation helper
  data/
    portfolio-data.ts     all resume content, typed
```

## Suggested next steps

- Swap the LinkedIn/email links for a resume PDF download if you'd like one
  hosted alongside the site.
- If you want routing between a full "About" page and this landing page
  later, this structure drops cleanly into a router outlet.
