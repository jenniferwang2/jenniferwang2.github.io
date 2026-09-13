---
title: "Return — HTB"
date: 2026-02-10
platform: "HackTheBox"
difficulty: "Easy"
kind: "Writeup"
summary: "Printer admin panel leaks LDAP creds; ServerOperators to SYSTEM."
scope: "Retired HackTheBox machine. All output is from my own lab session against the retired box; no third-party systems involved."
---

Return is a good example of a whole compromise hinging on one badly designed
web feature. The printer admin panel wants LDAP credentials to test a
connection, and it will happily send them to a server *you* control.

## Recon

Standard sweep first. Full TCP, then service versions on what answered.

```
nmap -p- --min-rate 2000 -oN scans/all.txt TARGET
nmap -sCV -p 53,80,88,135,139,389 -oN scans/svc.txt TARGET
```

Port 80 serves a printer administration panel. Kerberos, LDAP and DNS on
their usual ports say this is a domain controller — so a foothold here is
likely a foothold everywhere.

## Enumeration

The settings page has an LDAP section: server address, username, and a
password field that is pre-filled and masked. The "update" action makes the
server connect *out* to whatever address you give it, authenticating with
the stored credentials.

That is the whole vulnerability. Point it at myself.

## Foothold

Listener up, then change the LDAP server field to my IP and submit.

```
sudo nc -lvnp 389
```

The panel connects back and sends the service account credentials in the
clear. With a valid domain account I get a shell over WinRM.

```
evil-winrm -i TARGET -u svc-printer -p '<redacted>'
```

## Privilege escalation

`whoami /groups` shows the account sits in **Server Operators**. That group
can manage services — including reconfiguring one to run a binary of my
choosing as SYSTEM.

```
services              # confirm control
# repoint a service binary, restart it, catch SYSTEM
```

## Lessons

- A "test connection" button that authenticates outbound is a credential
  disclosure primitive. I now check every such feature for where it points.
- Server Operators is effectively local admin on a DC. Group membership is
  worth reading closely before reaching for an exploit.
- The masked password field still submitted the real value — masking is not
  protection.
