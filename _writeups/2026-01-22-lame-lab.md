---
title: "SMB service enumeration, methodically"
date: 2026-01-22
platform: "Home lab"
difficulty: "Notes"
kind: "Writeup"
summary: "A repeatable SMB enumeration checklist I run before touching an exploit."
scope: "Written against VMs on my own isolated lab network."
---

Less a box, more the checklist I wish I'd had when I started. Every time I
skip enumeration to jump at an exploit, I lose more time than I saved.

## The order I run things

```
nmap -p139,445 --script smb-protocols,smb-security-mode TARGET
smbclient -L //TARGET/ -N          # null-session share listing
enum4linux-ng -A TARGET            # users, groups, policy
```

## What each answers

- Protocols script: is SMBv1 alive? That reframes the whole approach.
- Null-session listing: can I read shares without creds? Often yes.
- enum4linux-ng: gives usernames to spray and password policy to spray
  *safely*, without locking accounts.

Only after all three do I decide whether this is a creds problem or an
exploit problem. Usually it's creds.
