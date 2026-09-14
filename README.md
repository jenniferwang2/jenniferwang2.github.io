# jenniferwang2.github.io

Personal site. Jekyll on GitHub Pages — no build step beyond what GitHub runs.

## Publish

Push to `main` in the repo named `jenniferwang2.github.io`, then
Settings → Pages → Source: `main` / root. Live in about a minute.

## Keeping it current

- `_data/experience.yml` holds the three roles. Newest first.
- `assets/resume.pdf` is the one-page resume, shown inline on `/resume/`
  (`resume.html`) with a download button beside it. **Re-copy it whenever
  you update the LaTeX resume** — nothing syncs it automatically.
- To hide every Resume button, clear `resume_pdf` in `_config.yml`.
- Writing is empty for now. Until `_writeups/` or `_posts/` has an entry,
  the Writing nav link, homepage section, RSS links, and the 404 page's
  "Browse writing" button all stay hidden; adding one brings them back.

## Structure

The homepage is one scrolling page. Sections in order, each with an `id`
the nav anchors to: hero, `#overview`, `#experience`, `#leadership`,
`#skills`, `#projects`, `#writing`, `#contact`.

| Path | What it is |
| --- | --- |
| `index.html` | The whole homepage. Skills and the four focus cards are inline here |
| `_data/experience.yml` | Work timeline |
| `_data/leadership.yml` | Leadership timeline |
| `_projects/*.md` | One file per project card; each also gets its own page |
| `writing.html` | `/writing/` index over `_writeups/` and `_posts/` |
| `blog/index.html` | `/blog/` — one card per series |
| `blog/<series>/` | A series: `index.html` (the series page) plus its posts |
| `resume.html` | `/resume/` — the PDF embedded in the site, plus download |
| `assets/css/main.css` | All the styling, hand-written, sectioned |
| `_includes/scripts.html` | The only JavaScript. Progressive enhancement only |

Nav items come from `nav:` in `_config.yml`. A url containing `#` is
treated as a homepage anchor and gets scroll-spy highlighting; anything
else is treated as a separate page.

## Adding content

**A role** — edit `_data/experience.yml`. Newest first. Community roles go
in `_data/leadership.yml`, same shape, its own timeline.

**A writeup** — new file in `_writeups/`, no date prefix in the filename
(the URL comes from the filename, the date comes from front matter):

```yaml
---
title: "Machine — Platform"
date: 2026-03-01
platform: "HackTheBox"
difficulty: "Easy"
summary: "One line that makes someone want to read it."
scope: "Retired machine. All output from my own lab session."
---
```

**A note or research post** — new file in `_posts/` named
`YYYY-MM-DD-title.md`. Front matter needs `title`, `date`, `summary`.

**A blog post** — the blog is organised into series. Posts are complete,
self-styled HTML documents with **no front matter**, so Jekyll copies them
byte-for-byte (no Liquid runs over them). Drop the file into its series
folder, e.g. `blog/backend-from-first-principles/04-something.html`, then add it to the
`posts:` list in that folder's `index.html`, in reading order:

```yaml
posts:
  - file: 04-something.html
    title: "Post title"
    summary: "One line for the series page."
    kind: "Walkthrough"
```

Posts link to each other with relative `./NN-name.html` hrefs, and their
series header links to `./` (the series page). Images go in the series'
`images/` folder as real files, named `NN-MM-slug.ext` — not as base64
`data:` URIs, which bloat the HTML and can't be cached or lazy-loaded.

**A blog series** — new folder `blog/<name>/` with an `index.html`:

```yaml
---
layout: series
title: "Series name"
permalink: /blog/<name>/
order: 2                 # position on /blog/
eyebrow: Blog series
summary: "Shown on the card and as the series page lede."
tags: ["Tag", "Tag"]
posts: []
---
```

**A project** — new file in `_projects/`:

```yaml
---
title: "name"
date: 2026-03-01
stack: "Python · asyncio"
status: "Maintained"
tags: ["Python", "asyncio"]   # rendered as #tags on the card
summary: "One line on what it does."
repo: "https://github.com/jenniferwang2/name"   # optional, adds a GitHub icon
---
```

Cards have no screenshots by design — each leads with a monogram plate
generated from the first two letters of the title.

Both `kind: "Writeup"` and `kind: "Note"` are applied automatically by
`_config.yml` defaults; they drive the filter buttons on `/writing/`.

## Design notes

Eyebrow over a large
heading, alternating vertical timeline, tag-carrying project cards, 
rendered in a white Apple-ish palette.

White base, one accent blue plus four tag hues, hairline rules, Geist.
Motion is deliberate and limited: the hero arrival, a scroll-reveal rise,
timeline cards entering from the side they sit on, and hover states. Every
one is disabled under `prefers-reduced-motion`, and the page is complete
with JavaScript off (including the nav, which falls back to plain
anchors).

## Local preview (optional)

Needs Ruby 3.x; the system Ruby on macOS is too old to build Jekyll's
native dependencies.

```
gem install bundler jekyll
jekyll serve
```

## The one rule for writeups

Retired, lab-only, or authorized targets. No real client, employer, or
bounty names, IPs, or hostnames. Redact flags and credentials.
