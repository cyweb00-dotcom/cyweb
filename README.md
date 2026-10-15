# CYWEB

The CYWEB website — one self-contained page. Everything is in `index.html`:
markup, styles and script, with no build step and nothing to install. Open the
file in a browser and it runs.

## What is in here

| File | What it is |
| --- | --- |
| `index.html` | The whole site |
| `logo-nav.png` | Logo for the header, footer and loading screen (white, transparent) |
| `logo-invoice.png` | Logo for the invoice, two-tone on white |
| `logo-mark-white.png` | The CY sub-mark alone — for a favicon or a social avatar |
| `logo-primary.png` | The full stacked logo including the tagline |
| `logo-horizontal-white.png` | The horizontal lockup including the tagline |

## The pages

Home, Packages, Get a price, Why Us, Our Work, How it works, Account,
My account, Admin, Contact and Legal. They are sections in the one file,
switched by `go(name)` — there is no router and no server.

## Settings

These are plain variables near the top of their sections in `index.html`.

| Setting | What it does |
| --- | --- |
| `SITE_URL` | This site's own address, e.g. `https://cywebdev.com/`. The "view invoice online" link is built from it. While empty, no link is put in any message — deliberately, so customers never get a link they cannot open. |
| `GOOGLE_CLIENT_ID` | Google OAuth client ID. With it set, **Send by Gmail** writes the email into Gmail as a draft with the invoice PDF attached. Without it, that button opens the compose window and you attach the PDF yourself. |
| `WHATSAPP_NUMBER` | The business WhatsApp number, digits only with country code. |
| `ADMIN_EMAIL` | The address the admin area is gated on. |
| `PREVIEW_OPEN` | `true` leaves the admin area open without signing in, for looking around. Set to `false` to put the gate back. |
| `REVIEWS` / `REVIEWS_URL` | Real customer reviews. Empty, so the reviews section does not render at all. Add real ones and it appears. |
| `CYWEB_DETAILS` | Business details on the invoice — logo, email, phone, address, registration number, VAT number, bank. |

## Never commit to this repository

It is public. Anything in it is readable by anyone.

- No Stripe secret key, no webhook signing secret
- No Supabase service-role key or database password
- No Google OAuth **client secret** (the client **ID** is public by design and
  belongs in the page; the secret does not, and this browser flow has no use
  for one)
- No customer data

Anything of that kind belongs in environment variables on whatever hosts the
site, never in the source.

## Known limits

The admin area is a working interface on top of browser storage, not a
database: records survive a refresh on one browser and nowhere else, and the
sign-in gate is cosmetic because the check happens in the browser. Real
accounts, a real database and server-side admin checks are the next step.

The legal documents are a draft and still carry `{{PLACEHOLDER}}` markers.
They need a Cyprus-qualified lawyer before the site goes live.
