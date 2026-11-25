# GrowthSeeded: a simple follow-up tracker for LinkedIn

A SaaS product I built end to end: the app, the website and how they run in production.

I'm a marketing strategist who builds software. This page shows my technical work through GrowthSeeded.

This repo is the first version of the GrowthSeeded website, kept as an archive. The live site and the app have since been rebuilt on a modern stack, and that code is private for security reasons.

## What GrowthSeeded is

GrowthSeeded is a simple follow-up tracker for LinkedIn. Add the people you want to stay in touch with, and each day it tells you who to message, so you don't forget to follow up. No complex CRM, no automation. You send every message yourself, and it adds no risk to your LinkedIn account.

- **Never forget a follow-up:** today's list shows who to message and what's next.
- **Simple, not a complex CRM:** add a name and a reason, and you're working in a minute.
- **No account risk:** no AI automation, no LinkedIn integration. You send every message yourself.

### The problem it solves

Most of LinkedIn is people who never replied, not people who said no. You connect, send one message, get busy, and three weeks later you can't remember who you talked to or what you said. The follow-up that would have worked never gets sent.

### How it works

1. **Add a person.** A name and why they matter is enough. You can paste their LinkedIn profile text to fill in the rest.
2. **Follow a few short steps.** Like a post, send a connection request, send a message once they accept, then set a follow-up date. Each step shows on your Today list when it's due.
3. **Keep the conversation in one place.** Paste the LinkedIn chat, or log a message from WhatsApp, email or a call. GrowthSeeded shows whose turn it is and when you last wrote.
4. **Follow up on time.** When a reply comes in, the person moves into a conversation. When it's not the right time, set a date to check in later, and GrowthSeeded brings them back when it comes around.

A short daily email lists who to follow up with, so you don't have to open the app to know.

### What it looks like in real life

- **Looking for a job.** You meet a hiring manager on a webinar and connect. Two weeks later, Today reminds you to check in, with your last message right there.
- **Raising money.** An investor says "come back when you have revenue." You set a follow-up for March and stop carrying it in your head.
- **Selling.** A prospect wasn't ready in spring. In autumn, GrowthSeeded tells you it's time to check in, and you know exactly where you left off.
- **Hiring.** A senior engineer passed last quarter. This quarter, you message them again at the right moment, with the full history in front of you.
- **Building a network.** You stay in touch with people before you need something, which is the only kind of networking that works.

### What it doesn't do

GrowthSeeded never sends anything for you, never logs into LinkedIn and never scrapes it. On paid plans, aiWrite can draft a comment or a message from the person's details and your conversation so far. You edit it, and you send it yourself.

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

## The first website (archive)

The first marketing site for [GrowthSeeded](https://growthseeded.com), a simple follow-up tracker for LinkedIn. This repo held the marketing site only (`growthseeded.com`). The app (`app.growthseeded.com`) lived in a separate repo.
<img width="452" height="332" alt="image" src="https://github.com/user-attachments/assets/9c997030-0a64-46b7-9033-e62e66c26db8" />

### Stack

Plain HTML, CSS and JavaScript. No framework, no build step, no npm packages at runtime.

That was on purpose:

- The site was nine pages of mostly static content. A framework like React solves problems (state across dozens of components, complex client-side routing) that this site didn't have.
- Fewer moving parts meant fewer things to secure, update and break. One person maintained it.
- It loaded fast and could be hosted anywhere, with no build pipeline.

The plan was to move to a static site generator once the site published blog posts and case studies regularly. When that time came, it moved to Astro with a headless CMS (see the top of this page).

### Structure

```
growthseeded-site/
├── site/                  # everything that got deployed
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
│   └── og/                # link preview images
├── .gitignore
└── README.md
```

Each HTML file stood on its own, with its own `<style>` and `<script>` blocks and no shared CSS or JS file. Brand colors and shared parts (buttons, footer) were repeated across all nine files. The new site fixed that with one shared set of brand tokens and components.

### Running it locally

There's no build step, so any static file server works. From the `site/` folder:

```bash
cd site
python3 -m http.server 8000
```

Then open `http://localhost:8000` in a browser. Opening the HTML files directly also works for most pages, but a local server behaves closer to the live site, especially for clean URLs.

### Deployment

It was hosted on Exonhost (a cPanel plan), with Cloudflare's free plan in front for caching and analytics. Deploys were manual: upload the contents of `site/` to the hosting account.

### Page inventory

| Page | Purpose |
|---|---|
| `index.html` | Homepage |
| `is-this-for-you.html` | Use cases for each kind of user |
| `pricing.html` | Plans, with a tool that suggests a plan size |
| `security.html` | How each account's data is kept separate |
| `contact.html` | Contact form (mailto, no backend) |
| `privacy.html` | Privacy policy |
| `terms.html` | Terms of service |
| `refund-policy.html` | Refund policy |
| `404.html` | Not-found page |

### Working habits

This repo was also where good habits started, and they carried into the new site and app:

- **One feature or fix per branch**, never direct commits to `main`.
- **Commit messages say what changed and why**, such as `Fix broken pricing link in footer`, not just `fix`.
- **A pull request for every change, even working alone**, with the diff read before merging.

### License

Not licensed for reuse. All rights reserved.
