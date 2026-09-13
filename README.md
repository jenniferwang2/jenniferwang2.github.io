# jenniferwang2.github.io

Personal site. Jekyll on GitHub Pages — no build step beyond what GitHub runs.

## Publish

Push to `main` in the repo named `jenniferwang2.github.io`, then
Settings → Pages → Source: `main` / root. Live in about a minute.

## Keeping it current

- `_data/experience.yml` holds the three roles. Newest first.
- `assets/resume.pdf` is the downloadable one-page version. **Re-copy it
  whenever you update the LaTeX resume** — nothing syncs it automatically,
  and the page content is maintained separately in `resume.html`.
- To hide every download button, clear `resume_pdf` in `_config.yml`.
- `_projects/subwatch.md` and both files in `_writeups/` came with the
  original scaffold rather than from the resume. Delete them if they
  aren't yours.

## Structure

| Path | What it is |
| --- | --- |
| `index.html` | Homepage: statement, experience, projects, resume |
| `experience.html` | Full role history, rendered from `_data/experience.yml` |
| `projects.html` | Grid of everything in `_projects/` |
| `writing.html` | One index over `_writeups/` and `_posts/` |
| `resume.html` | Readable resume + PDF download |
| `assets/css/main.css` | All the styling, hand-written, sectioned |
| `_includes/scripts.html` | The only JavaScript. Progressive enhancement only |

## Adding content

**A role** — edit `_data/experience.yml`. Newest first. `highlights` and
`stack` only render on `/experience/` and `/resume/`, not the homepage.

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

**A project** — new file in `_projects/`:

```yaml
---
title: "name"
date: 2026-03-01
stack: "Python · asyncio"
status: "Maintained"
summary: "One line on what it does."
repo: "https://github.com/jenniferwang2/name"   # optional
---
```

Both `kind: "Writeup"` and `kind: "Note"` are applied automatically by
`_config.yml` defaults; they drive the filter buttons on `/writing/`.

## Design notes

White base, one accent blue, hairline rules, Geist. Motion is deliberate
and limited to four gestures: the hero arrival, a scroll-reveal rise,
hairlines drawing themselves in on the timeline, and hover states. Every
one of them is disabled under `prefers-reduced-motion`, and the page is
complete with JavaScript off.

Keep it that way. No dark mode — the site is committed to the light palette.

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
