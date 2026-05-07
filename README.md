# StaySync — Reservation Automation Demo

Public, no-login demo of the property-reservation tool that powers the production **StaySync** app (private repo: `staysync-prod`). Tracks short-term rental guests, sends door codes via email, and previews how the same UI behaves for different staff roles.

The whole app lives in [`index.html`](index.html) — open it directly in any browser. No build step, no install, no server required. It talks to a shared demo Google Sheet for reads and a deployed Apps Script for writes.

## What's in here

- **Reservations dashboard** — arriving today, upcoming (7 days), current occupancy, leaving today.
- **Occupancy calendar** — month or week view with per-apartment bars; mobile shows a 7-day "This Week" agenda instead.
- **Send door code** — pick an arriving reservation, confirm the code, fire an email via EmailJS.
- **EN / ES** — language toggle in the header (first visit shows a language splash).
- **Guided tour** — step-by-step overlay walkthrough on first load.
- **Admin panel** — Add / Reservations / Rooms tabs.
- **Demo role-switcher** — Owner / Tech Staff / Staff dropdown in the header (see below).

## How to run

- **Locally:** double-click `index.html` (or open it from your browser's File menu). The status pill in the header should switch to "Sheets: connected" within a few seconds.
- **GitHub Pages:** if Pages is enabled on this repo, the deployed URL serves the same file.

If the Google Sheet is unreachable for any reason, a small built-in demo dataset loads automatically so the UI is never empty.

## Demo role-switcher

Real authentication doesn't fit a public, zero-login demo, so the header includes a **role dropdown** (Owner / Tech Staff / Staff) that flips a client-side `currentRole`. It re-runs the same `hasPermission()` gating the production app uses, so you can preview what each role sees without signing in.

| Role        | Door codes              | Edit / delete reservations | Rooms tab | Admin panel |
|-------------|-------------------------|----------------------------|-----------|-------------|
| Owner       | Visible                 | Yes                        | Yes       | Yes         |
| Tech Staff  | Visible                 | Yes                        | Yes       | Yes         |
| Staff       | Always blurred          | No (buttons hidden)        | Hidden    | Yes         |

Because there's no real auth, switching role is not a security boundary — anyone could flip it from devtools. It's purely a preview affordance.

## Differences from the production StaySync app

| Feature                | Demo                              | Production                        |
|------------------------|-----------------------------------|-----------------------------------|
| Backend                | Google Sheets + Apps Script       | Supabase Postgres + Auth          |
| Authentication         | None                              | Email + password, magic-link invites, password reset |
| User management        | Demo role-switcher (client-side)  | Full USERS tab with per-user permissions, suspend/restore |
| Telegram notifications | Not included                      | Bot pings on code-sent / email-failed |
| Credentials            | Inline in `index.html`            | `config.js` (gitignored)          |

The two apps share the same UI shell, calendar, send-code flow, i18n strings, and guided tour. This demo is a snapshot of that shell on the original Sheets backend.

## Files

```
index.html   # The whole app (~2,250 lines, ~124 KB)
README.md    # This file
```

## Versions

| Tag         | Description                                                       |
|-------------|-------------------------------------------------------------------|
| `v1.0-demo` | Original frozen demo (March 2026) — pre-i18n, no role-switcher    |

To roll back to the original:

```bash
git checkout v1.0-demo
```
