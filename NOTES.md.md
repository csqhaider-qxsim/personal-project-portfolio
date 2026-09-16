# Portfolio V1 — editing & deployment guide

## Folder structure
```
portfolio/
├── index.html          → all page content, section by section
├── css/
│   └── style.css        → design tokens + all styling
├── js/
│   └── script.js         → mobile nav toggle, footer year
├── assets/
│   ├── appraised/
│   │   └── screenshot.png   ← add a real screenshot here
│   └── reel/
│       └── screenshot.png   ← add a real screenshot here
└── README.md
```

## Before you deploy — replace these placeholders
Search `index.html` for these and swap them out:

| Placeholder | Where | Replace with |
|---|---|---|
| `Your Name` (appears 3x: `<title>`, logo, footer) | header + footer | your actual name |
| `href="#"` next to "GitHub" (2x, one per project) | project cards | your real repo URLs |
| `href="#"` GitHub/LinkedIn in footer | footer | your real profile URLs |
| `you@example.com` | footer | your real email |
| `action="https://formspree.io/f/yourFormId"` | contact form | see "Contact form" below |
| `assets/appraised/screenshot.png`, `assets/reel/screenshot.png` | project media | real screenshots (see below) |

## Adding screenshots
Take a screenshot or short GIF of each live demo (Appraised: https://device-value.netlify.app/,
Reel: https://reel-movie.netlify.app/) and drop the image file into the matching
`assets/<project>/` folder, named `screenshot.png`. Until you add one, the site shows a
plain placeholder box instead of a broken image.

## Contact form
The form uses **Netlify Forms** — no third-party account or backend needed. Netlify scans
your deployed HTML for a `<form data-netlify="true">` and wires it up automatically.

**Important — this only works after it's deployed on Netlify.** Opening `index.html`
locally (double-clicking the file, or a live-preview extension in VS Code) will always show
a "Form not found" style error, because there's no Netlify backend behind it yet. It's not
broken — it just hasn't been deployed.

Once it's live on Netlify:
1. Submit a test enquiry on the live site.
2. In your Netlify dashboard, go to **Site settings → Forms** — your submissions (and the
   sender's email, if you want a reply-to) show up there.
3. To get emailed automatically when someone submits: **Forms → Form notifications → Add
   notification → Email notification**, and enter your address.
4. A successful submission redirects to `thanks.html` (included) instead of Netlify's
   generic default confirmation page.

If you'd rather use Formspree instead (e.g. because you're not hosting on Netlify), replace
the `<form>` opening tag in `index.html` with:
```html
<form class="contact-form" action="https://formspree.io/f/yourRealFormId" method="POST">
```
and delete the `form-name` hidden input and the honeypot `<p class="hidden-field">` block
(those are Netlify-specific).

## Where each homepage section lives in index.html
- `<header class="site-header">` — sticky nav bar
- `<section class="hero">` — headline + two CTA buttons
- `<section id="work">` — the two project cards (Appraised, Reel)
- `<section id="services">` — "What I can build" (3-column grid)
- `<section id="about">` — short bio
- `<section id="skills">` — 3-column skills list
- `<section id="contact">` — the enquiry form

Each project card follows this pattern, so adding a third project later is just
copy-pasting one `<article class="project">...</article>" block and editing the content:
```html
<article class="project">
  <div class="project-media"><img src="assets/yourproject/screenshot.png" ...></div>
  <div class="project-body">
    <div class="project-heading"><h3>Name</h3><span class="project-tag-line">One-line description</span></div>
    <p class="project-desc">...</p>
    <ul class="line-items"><li><span>Feature</span><span>Detail</span></li>...</ul>
    <div class="tech-tags"><span>Tech</span>...</div>
    <div class="project-actions"><a href="...">Live demo →</a><a href="...">GitHub →</a></div>
  </div>
</article>
```

## Deploying to Netlify
Same flow you already used for Appraised and Reel:
1. Push this `portfolio` folder to a new GitHub repo.
2. In Netlify: **Add new site → Import an existing project → connect the repo.**
3. Build command: leave blank. Publish directory: `.` (or leave default — this is a static
   site with no build step).
4. Deploy. Netlify gives you a free `*.netlify.app` URL immediately.
5. Once you buy a domain (e.g. `yourname.dev`), add it under **Domain settings** in Netlify
   and follow their DNS instructions.

Netlify's free tier explicitly allows commercial/freelance use, so this is fine to run on
the free plan indefinitely for a portfolio like this.
