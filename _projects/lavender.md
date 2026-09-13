---
title: "Lavender"
date: 2025-01-01
stack: "Python · Django REST Framework · Docker · SQLite · JavaScript"
status: "Team course project"
tags:
  - "Python"
  - "Django REST Framework"
  - "Federation"
  - "AuthN/AuthZ"
  - "Docker"
summary: "A federated social platform where independent servers push posts to each other's followers."
# Uncomment and point at the real repo to add a "View source" button:
# repo: "https://github.com/jenniferwang2/lavender"
---

Lavender is a federated social platform, co-developed as a team project. Each
node runs independently and pushes content to followers on other servers, so
the interesting problems are all at the trust boundary between nodes rather
than inside any one of them.

## Federation model

The platform uses an inbox-based model: when someone posts or comments, their
node delivers that object to the inboxes of followers on remote servers.
That means every node is simultaneously a client of its peers and a server
accepting unsolicited inbound content — which is exactly where the
authentication work went.

## Authentication across a trust boundary

I implemented a custom authentication class that handles two very different
kinds of caller on the same endpoints:

- **Local users**, authenticated normally.
- **Remote nodes**, authenticated with per-node credentials.

On top of that sits an allowlist controlling which federated servers are
permitted to push inbound content at all. An open inbox is an open door; the
allowlist is what decides whose requests are even worth authenticating.

## Authorization

Two layers, because "who are you" and "what may you touch" are separate
questions:

- Three-tier post visibility — public, unlisted, and friends-only.
- Object-level permissions restricting edits to the author of the content.

## Hardening

Authentication is required by default on every endpoint, so a new route is
closed until someone deliberately opens it. Beyond that, the HTTP layer sets
Content-Security-Policy and X-Frame-Options, and keeps CSRF protection and a
deliberate CORS configuration in place.

The whole thing is containerized with Docker behind a Caddy reverse proxy,
which keeps TLS and header handling in one place rather than scattered
through the application.
