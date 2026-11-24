# CLAUDE.md — billuyadavg.github.io

Personal landing page for **Billu Yadav**, served by GitHub Pages at **https://billuyadav.com/** (custom domain; the repo is still `billuyadavg.github.io`, which now redirects to it).

**Positioning:** a startup leader with 13 years' experience, now an independent consultant. He is a digital partner to idea-stage and seed to Series A B2B SaaS founders (especially sales teams), available for startup partnerships and idea discussions, and builds agentic AI workflows for business requirements. Every change should support one goal: getting the visitor to **book a call**.

> This repo is public and `.nojekyll` serves every file, including this one, at billuyadav.com/CLAUDE.md. Never commit tokens, passwords, phone numbers or private notes.

## Stack and files

A static site with no build step, framework or package manager. Pages deploys straight from `main` / root.

| File | Purpose |
|---|---|
| `index.html` | The whole site: markup, inline `<style>` and inline `<script>` in one file |
| `404.html` | Branded not-found page (`noindex`) with links home and to `/#book` |
| `og-image.png` | 1200×630 link-preview image (LinkedIn, WhatsApp, X) |
| `apple-touch-icon.png` | 180×180 home-screen icon |
| `billu-yadav.webp` | 360×360 headshot for the hero card and mobile name row |
| `robots.txt`, `sitemap.xml` | Crawl rules and the single-URL sitemap |
| `.nojekyll` | Tells Pages to skip Jekyll; keep it |
| `CNAME` | Custom domain `billuyadav.com`; keep it, or Pages drops the domain |

Keep everything in single files with inline CSS and JS. Don't add a build tool, a CSS framework or extra JS libraries unless asked.

## Page structure (`index.html`)

Sections run in this order. Their `id`s are the nav and link anchors, so keep them stable:

1. Hero: badge "Now taking on new projects" (matches the LinkedIn banner), H1 "Billu Yadav" + "Upgrade your business with agentic AI workflows.", a lede for founders and business owners, CTAs ("Book a free 30-min call", "See what I've built"), and an "at a glance" card with a 72px avatar. The card is hidden below 680px.
2. Proof strip: 4 result stats plus "Built at Zime.ai · Credihealth · TravelTriangle".
3. `#services`: two offers (startup partnership, agentic workflows) and `#agentic`, the 4-step build process.
4. `#work`: "Selected work", three case studies (problem, what I built, results).
5. `#engage`: "Ways to work together", four engagement cards.
6. `#experience`: condensed role timeline, recommendation quote, education.
7. `#skills`: one toolkit card with AI & Agents first and highlighted, then Integrations. Below 680px only the first two groups show, behind a "Show full toolkit" button.
8. `#faq`: six `<details>` questions. Keep the visible text and the `FAQPage` JSON-LD identical.
9. `#book`: intro, Calendly embed and `#contact` (email, copy button, LinkedIn). On mobile the calendar comes before the contact box (CSS grid areas).

Nav items are Services, Work, Engagements, Experience and FAQ, plus the Book a call button. Desktop and mobile share one `<nav id="navLinks">`. The mobile menu closes on Esc, on an outside click and after choosing a link, and the nav highlights the section in view with `aria-current`.

Icons come from one inline SVG sprite at the top of `<body>` (`<use href="#i-check">` and so on). Add new icons there rather than inlining SVG paths.

## Calendly

- The link is set in one place, near the bottom of `index.html`: `const CALENDLY_URL = "https://calendly.com/billuyadav/30min-meeting-with-billu";`
- The widget script loads only when `#book` scrolls near the viewport (IntersectionObserver).
- If the URL is empty or invalid, the page shows a "Request a slot by email" fallback. If Calendly's script fails to load, it shows an "Open booking page" button. Keep both fallbacks.

## Design rules

- Light theme with **Inter only**. Billu asked for a simple font, so don't add a second typeface.
- Colours come from CSS variables on `:root`: accent `#2563eb`, text `#111827`, soft background `#f7f7f8`, green for availability. Reuse them instead of hard-coding new colours.
- Must work at 375px wide with no horizontal scroll. Breakpoints are at 900px and 680px, and below 680px the nav collapses to a hamburger.
- Respect `prefers-reduced-motion`. Keep the skip link and visible focus styles.
- Billu rejected an earlier dark, serif-heavy design ("doesn't look good"). Keep the clean, light consultant style.

## Content rules and sources

- **Experience is always "13 years".** The resume and LinkedIn say "12+", but Billu chose 13 for the site.
- Sources, in priority order: Billu's instructions, then his resume (`Billu_Yadav_RoR_Resume.pdf`), then LinkedIn (linkedin.com/in/billuyadav). Don't invent metrics. Every number on the page comes from the resume or LinkedIn.
- **Current role:** Independent Consultant — Agentic AI & Startup Technical Partner (Nov 2026 – present). Clients are confidential; the AI model training work may be mentioned only in general terms. He is setting up a consulting company; rename the role once it has a name.
- **Zime.ai:** title **Founding Team Member**, Jan 2024 – Oct 2026 (Billu's choice, matching LinkedIn). Never "Engineering Manager" for Zime. He led the team and owned integrations and the meeting pipeline (calendar sync → recording → transcripts → playbook checks, plus CRM sync).
- **Location:** Jaipur, India (IST). Remote.
- The public email is `itisme.billuyadav@gmail.com`. Don't publish a phone number.
- Keep the copy outcome-focused for founders and business owners. Rails-specific detail (ActiveRecord, jQuery and so on) adds little to the agentic-AI pitch.
- **Case studies are anonymised.** Use "B2B SaaS · Sales AI", "Healthtech marketplace" and similar labels, never Zime.ai or Credihealth by name. Company names are fine elsewhere (hero, Built at, experience).
- **Engagement types (all four are offered):** free 30-minute intro call, paid advisory (hourly or monthly), fractional CTO / tech co-founder (terms, including equity, case by case), and fixed-scope agentic workflow builds. No prices on the site.
- **Photo:** `billu-yadav.webp` (360×360 WebP, cropped around the face from the photo Billu sent in Nov 2026). It appears in the hero card (`.avatar`, 72px, BY monogram behind it as fallback) and as a 40px `.m-photo` next to the name on mobile, and is the JSON-LD `Person.image`. Keep it small (under ~15 KB).
- **Decided against for now:** analytics. Don't add it without asking.

## SEO checklist (keep these in sync when content changes)

- `<title>` stays under about 60 characters and the meta description at 150–160.
- The H1 includes "Billu Yadav". There is exactly one H1, and heading levels don't skip (h1 → h2 → h3).
- Open Graph and Twitter tags point to `https://billuyadav.com/og-image.png` with `summary_large_image`.
- The JSON-LD `@graph` holds `Person`, `ProfessionalService` and `WebSite`. Update `jobTitle`, `knowsAbout` and the offers when roles or services change, and make sure the JSON still parses.
- Update `<lastmod>` in `sitemap.xml` whenever page content changes.
- Canonical, `og:url`, JSON-LD `@id`/`url`, `sitemap.xml` and `robots.txt` all use `https://billuyadav.com/`. Never reintroduce the github.io URL.
- If the headline or positioning changes, regenerate `og-image.png` (1200×630, Inter, same palette; footer shows billuyadav.com) so link previews match.
- Planned but not done: a Google Search Console verification meta tag, and articles or blog posts.

## Validate before every deploy

Run headless Chromium (Playwright is available) on `index.html` at **1440×900 and 375×812** and check:

- `document.documentElement.scrollWidth <= innerWidth`, meaning no horizontal scroll
- Every `a[href^="#"]` resolves to an element
- The mobile menu opens, and closes after tapping a link
- No console errors (ignore failed font requests if the sandbox blocks Google Fonts)
- The Calendly iframe appears after scrolling to `#book`, or the fallback card does
- The JSON-LD parses, and the title and description lengths are within range
- An axe-core scan (wcag2a, wcag2aa, wcag21aa, best-practice) reports 0 violations, and tap targets on mobile are at least 44px
- Lighthouse stays at 100 for Accessibility and SEO and at least 95 for Performance. Locally, "text compression" and "console errors" fail only because the test server doesn't gzip and the sandbox blocks Google Fonts.
- Full-page screenshots at both widths look right; view them, don't just generate them

After deploying, recheck the live site with a cache-busting query (`/?v=<timestamp>`). Pages usually updates within 1–2 minutes. Also confirm that `/robots.txt`, `/sitemap.xml` and `/og-image.png` return 200 and that a random path returns the 404 page.

## Deploying

- Pages builds from `main` at the repo root. A push to `main` is a production deploy.
- Commit messages are short and imperative, for example `SEO: share image, sitemap, robots, 404, structured data`.
- Never use personal access tokens, and never store one in the repo, in commands or in chat. Deploy through the Claude GitHub connection or the GitHub web UI ("Add file → Upload files") while signed in as `billuyadavg`.

## Domain and DNS

- `billuyadav.com` is registered at GoDaddy (Billu's account). DNS: four apex `A` records `@` → 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153, and `CNAME www` → `billuyadavg.github.io`. Leave the NS, SOA, `_domainconnect` and `_dmarc` records alone.
- GitHub repo Settings → Pages holds the custom domain and "Enforce HTTPS". Domain renews Oct 2027; auto-renew was off when set up.

## Related

- Site: https://billuyadav.com/
- LinkedIn: https://www.linkedin.com/in/billuyadav/
- Booking: https://calendly.com/billuyadav/30min-meeting-with-billu
