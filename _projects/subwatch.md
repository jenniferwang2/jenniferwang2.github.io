---
title: "subwatch"
date: 2026-02-01
stack: "Python · asyncio"
status: "Maintained"
tags:
  - "Python"
  - "asyncio"
  - "Certificate Transparency"
  - "Recon"
summary: "Watches a domain's certificate transparency logs and alerts on new subdomains."
# Uncomment and point at the real repo to add a "View source" button:
# repo: "https://github.com/jenniferwang2/subwatch"
---

A small tool born from doing the same thing by hand too many times. It polls
certificate transparency logs for a domain and tells me when a new subdomain
shows up — useful for keeping an eye on my own attack surface.

## Why I built it

During recon I kept re-running the same CT-log queries manually. Automating
it meant I could point it at my own domains and get notified instead of
remembering to check.

## How it works

- Queries CT log endpoints asynchronously for a target domain
- Diffs the result against a local seen-list
- Sends anything new to a webhook

```
python subwatch.py --domain example.com --webhook $HOOK
```

Source is on my GitHub. It only queries public CT logs and only for domains
I own or am authorized to monitor.
