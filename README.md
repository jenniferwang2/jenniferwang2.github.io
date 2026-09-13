# Personal security site

Jekyll on GitHub Pages. No build step beyond what GitHub runs.

## Publish
1. Create a repo named `USERNAME.github.io`.
2. Push these files to the `main` branch.
3. Settings → Pages → Source: `main` / root. Live in ~1 min.

## Local preview (optional)
    gem install bundler jekyll
    jekyll serve

## Add content
- Writeup: new file in `_writeups/`, copy the front matter from an existing one.
- Log/cert entry: new file in `_posts/` named `YYYY-MM-DD-title.md`, set `kind:` to `Log` or `Cert`.
- Tool: new file in `_projects/`.

Set your name, handles, and URL in `_config.yml` first.

## The one rule
Retired / lab-only / authorized targets. No real client, employer, or
bounty names, IPs, or hostnames. Redact flags and creds.
