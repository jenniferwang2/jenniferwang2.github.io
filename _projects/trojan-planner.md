---
title: "Trojan Planner"
date: 2024-01-01
stack: "Java · Android Studio · Firebase · JUnit"
status: "Course project"
tags:
  - "Java"
  - "Android"
  - "Firebase"
  - "RBAC"
  - "JUnit"
summary: "An Android event-hosting app built around role-based access control for participants, hosts, and admins."
# Uncomment and point at the real repo to add a "View source" button:
# repo: "https://github.com/jenniferwang2/trojan-planner"
---

An Android app for hosting and joining events. The design problem worth
solving was access control: three kinds of user share one data model, and
each should only see and do what their role allows.

## Roles

Participants, hosts, and admins each get distinct permissions and distinct
views of the same underlying events. Getting this right meant deciding
permissions at the data layer rather than hiding buttons in the UI — a
hidden button is a UI preference, not a control.

## Firebase integration

- **Auth** for secure sign-in.
- **Realtime Database** for event state.
- **Storage** for uploaded assets.

Offline-first caching keeps the app usable without a connection and
reconciles when it returns.

## Structure and testing

Midway through, I refactored the app to MVVM, which made the view layer thin
enough to test the logic underneath it. On top of that: unit and UI tests
with JUnit, Espresso, and Mockito, plus linting in CI so style and obvious
defects get caught before review rather than during it.
