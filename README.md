# GrowthSeeded — Marketing Site

The public marketing site for [GrowthSeeded](https://growthseeded.com), a personal relationship-tracking tool for deliberate LinkedIn outreach. This repo covers the marketing site only (`growthseeded.com`). The app itself (`app.growthseeded.com`) lives in a separate repo.

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
