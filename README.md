# GrowthSeeded: a SaaS product I built end to end

I'm a marketing strategist who builds software. This page shows my technical work through GrowthSeeded: the app, the website and how I run them in production.

This repo is the first version of the GrowthSeeded website, kept as an archive. The live site and the app have since been rebuilt on a modern stack, and that code is private for security reasons.

## What GrowthSeeded is

**GrowthSeeded: a simple follow-up tracker for LinkedIn.**

GrowthSeeded is a simple follow-up tracker for LinkedIn. Add the people you want to stay in touch with, and each day it tells you who to message, so you don't forget to follow up. No complex CRM, no automation. You send every message yourself, and it adds no risk to your LinkedIn account.

Live at [growthseeded.com](https://growthseeded.com), with free sign-up at [app.growthseeded.com](https://app.growthseeded.com).

## The app

| Layer | What it runs on |
|---|---|
| **Front end** | Next.js 15 (static export), React 19, TypeScript, Tailwind CSS 4, on Cloudflare Pages |
| **Shared rules** | One TypeScript package holds the product's rules (follow-up timing, sequences, message reading), used by the app and the server alike |
| **Back end** | Firebase Authentication, Firestore with locked-down security rules, and Cloud Functions for billing, plan changes, emails, referrals and admin |
| **Edge** | Cloudflare Pages Functions for aiWrite, with a strict Content-Security-Policy |
| **Billing** | Paddle, with plans set on the server from the verified payment and never trusted from the browser |
| **Email** | Brevo for the daily "who to follow up with" email, reminders and account emails, with daily caps |

### Engineering highlights

- **Rules you can test.** The scheduling and follow-up logic lives in one shared package, covered by more than 380 automated tests across the app and the server.
- **Reading real conversations without AI.** A user can paste a LinkedIn chat or messages copied from WhatsApp. Plain parsing rules work out who sent each message and when, handle every date format, ignore profile noise, and show whose turn it is.
- **AI that drafts but never sends.** aiWrite drafts comments and messages from the person's details and the conversation so far. Pasted conversations are passed to the model as data, never as instructions, which guards against prompt injection. The user edits and sends every message themselves. Paid plans only.
- **Security first on money.** Billing, seats and limits are enforced on the server. Firestore rules check every write.
- **Costs under control.** Budget alerts, query limits and caps, so a bug can't run up a bill.
- **User control over data.** Users export their data and delete their account themselves.
- **A safe rebuild.** I rebuilt the whole app beside the old one on the same accounts, tested it, switched the live address with no downtime, and kept a way back ready.

## The website

| Layer | What it runs on |
|---|---|
| **Framework** | Astro 7 with TypeScript, fully static output |
| **Content** | Sanity headless CMS. Copy, SEO titles, FAQs, pricing, landing pages and redirects are edited without touching code. |
| **Hosting** | Cloudflare Pages, with a private preview link for every branch that search engines never index |
| **Forms** | Cloudflare Pages Functions for support, creator and ambassador applications, with Turnstile bot checks and Brevo email. Nothing a visitor types is stored on the site. |
| **Automation** | GitHub Actions to test, publish and deploy |

### Engineering highlights

- **A migration that lost nothing.** Every address from the old sitemap was saved on moving day and is tested automatically, so old links and search results keep working. Before the DNS moved to Cloudflare, a script compared every record between the old and new hosts.
- **Security by default.** A strict Content-Security-Policy with no inline scripts or styles, HSTS, and no secrets in the repo.
- **Privacy by region.** The site works out the visitor's country at the edge and asks before turning on analytics only where the law requires it.
- **Search, including AI search.** Clean URLs, a generated sitemap, an `llms.txt` file, link-preview images generated for every page, a landing page for each audience, and a blog.
- **Checks that run themselves.** Every push is tested against the preview or the live site, and again every morning. Blog posts publish on their own only when they change content alone and every check has passed. Code changes wait for a human review.

## How I work

- Every change is a small pull request with its own preview build, and nothing merges until the preview is green.
- Tests come with every change. Typecheck and build must pass.
- Production comes first: real users are on it, so nothing broken ships.
- I build with AI-assisted development using Claude. I own the product decisions, the architecture choices, the testing and the review.

## Technical skills

**Build:** Next.js, React, TypeScript, Tailwind CSS · Astro · Firebase (Auth, Firestore, Cloud Functions) · Cloudflare Pages and Functions · Sanity, WordPress

**Production:** Paddle billing · Brevo email · GitHub Actions CI/CD · DNS and domain migrations · Content-Security-Policy and web security · privacy and consent by region

**Growth tech:** technical SEO and schema · AI search visibility (AEO/GEO) · GA4 and Tag Manager · HubSpot and n8n automation

## About me

I have more than 9 years in marketing and content, most of it in B2B and SaaS. Today I'm Marketing Lead at an Australian fintech SaaS company. Before that I led content and SEO at Discovered and marketing at REVE Chat, where I grew organic traffic 40% in 6 months and helped bring in clients including the Mexican Government. Building GrowthSeeded is where marketing and engineering meet for me: I wrote the positioning from audience research, then built the product and the site that deliver it.

## Get in touch

[LinkedIn](https://www.linkedin.com/in/anisfagun/) · anis@growthseeded.com

---

> **The archive below:** the first GrowthSeeded website, in plain HTML, CSS and JavaScript. Its README planned a move to a static site generator once the site had a blog. That's what happened.

---

# GrowthSeeded — Marketing Site

The public marketing site for [GrowthSeeded](https://growthseeded.com), a personal relationship-tracking tool for deliberate LinkedIn outreach. This repo covers the marketing site only (`growthseeded.com`). The app itself (`app.growthseeded.com`) lives in a separate repo.
<img width="452" height="332" alt="image" src="https://github.com/user-attachments/assets/9c997030-0a64-46b7-9033-e62e66c26db8" />


## Stack

Plain HTML, CSS, and JavaScript. No framework, no build step, no npm dependencies at runtime.

That's a deliberate choice, not a placeholder for something more advanced later:

- The site is nine pages of mostly static content. A framework like React solves problems (state management across dozens of components, complex client-side routing) that this project doesn't have.
- Fewer moving parts means fewer things to secure, update, and eventually break. One person maintains this.
- It loads fast and deploys anywhere, no build pipeline required.

If the site grows to the point of publishing blog posts and case studies regularly, the next step under consideration is a **static site generator** (Eleventy), which still outputs plain HTML, rather than moving to a framework.

## Structure

```
growthseeded-site/
├── site/                  # everything that gets deployed
│   ├── index.html         # homepage
│   ├── is-this-for-you.html
│   ├── pricing.html
│   ├── security.html
│   ├── contact.html
│   ├── privacy.html
│   ├── terms.html
│   ├── refund-policy.html
│   ├── 404.html
│   ├── robots.txt
│   ├── sitemap.xml
│   ├── favicon.svg
│   └── og/                # Open Graph social preview images
├── .gitignore
└── README.md
```

Each HTML file is fully self-contained: its own `<style>` block and `<script>` block, no shared CSS/JS file yet. That's the main thing worth refactoring next, since brand colors and shared components (buttons, footer) are currently duplicated across all nine files.

## Running it locally

No build step, so any static file server works. From the `site/` folder:

```bash
cd site
python3 -m http.server 8000
```

Then open `http://localhost:8000` in a browser. (Opening the HTML files directly by double-clicking also works for most pages, but a local server is closer to how it behaves once deployed, especially for the clean URLs.)

## Deployment

Hosted on Exonhost (existing cPanel plan), with Cloudflare's free plan in front for CDN and analytics. Deployment is currently manual: upload the contents of `site/` to the hosting account's public directory for the growthseeded.com addon domain.

## Page inventory

| Page | Purpose |
|---|---|
| `index.html` | Homepage |
| `is-this-for-you.html` | Persona-specific use cases |
| `pricing.html` | Plans, interactive plan-size recommender |
| `security.html` | How data isolation actually works |
| `contact.html` | Contact form (mailto-based, no backend) |
| `privacy.html` | Privacy policy |
| `terms.html` | Terms of service |
| `refund-policy.html` | Refund policy |
| `404.html` | Not-found page |

## Working on this together

This repo is also a shared learning project. A few habits worth keeping from day one:

- **One feature or fix per branch**, not direct commits to `main`. Even solo, this builds the habit and makes the history readable.
- **Commit messages describe what changed and why**, not just "update". e.g. `Fix broken pricing link in footer` rather than `fix`.
- **Open a pull request even when working alone**, and actually read the diff before merging. That's the real skill being practiced here, not just the git commands.

## License

Not currently licensed for reuse. All rights reserved.
