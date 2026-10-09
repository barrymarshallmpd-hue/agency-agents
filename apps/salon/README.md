# Debbie's Chair

A simple salon app for one stylist: today's clients, the schedule, phone calls to return, client cards with color formulas, and prices. It installs on a phone like a regular app and works without a signal.

Built from this repo's **Rapid Prototyper**, **UI Designer** and **UX Architect** agent prompts: ship the smallest thing that's useful, design it as a system, and keep it simple enough to use with one thumb between clients.

## What it does

| Tab | What Debbie sees |
|---|---|
| **Today** | Who's next and how soon, allergy warnings, clients today, calls waiting, money earned in the last 7 days, regulars who are 6+ weeks out with nothing booked (one tap to text them) |
| **Schedule** | Week strip and day list. Open gaps show between appointments, so when someone calls asking "when can you fit me in?" the answer is on screen. Tap a gap to book it. Warns before double-booking or booking outside hours. |
| **Calls** | Log a call in a few seconds: who, number, what they want, what happens next. "Call back" calls stay on the list with Call / Text / Book buttons until handled. |
| **Clients** | Search by name or phone. Each card has the phone number, allergies, patch-test date (flags it after 6 months), notes, **color formula history** (shade, ratio, developer, time, result), upcoming visits and history. |
| **Settings** | Salon name, hours, open days, services & prices, the pre-written text messages, light/dark look, backup & restore. |

Texts open her own Messages app with the words already filled in. She reviews and sends them herself, so nothing goes out without her seeing it.

## Running it

It's one HTML file with no build step and no server code.

- **Try it:** open `index.html` in a browser. It starts with sample clients; Settings → *Clear sample clients* wipes them.
- **Put it on her phone:** host this folder on any HTTPS static host (GitHub Pages, Netlify, Cloudflare Pages are all free), open the link in Safari, then Share → *Add to Home Screen*. The service worker (`sw.js`) keeps it working offline.

## Where the data lives (read this)

Everything is stored **on the phone, in the browser** (`localStorage`). Nothing is sent anywhere.

- Good: no monthly cost, no account, no server to get breached, client info never leaves her phone.
- The catch: it lives on **one device**. If the phone is lost or Safari's website data is cleared, the data goes with it. **Settings → Save a backup** once a week and email it to herself. Restore puts it back.
- Lock the phone with a passcode/Face ID. That's the real security on client allergy info and phone numbers.

## What it does *not* do yet, and how we'd add it

| Want | How | Rough cost |
|---|---|---|
| **The app answers the phone** | A browser app can't answer calls. Get a business number (Twilio or Google Voice) that forwards to her cell, sends a "sorry I missed you" text, and drops missed calls into this app. Or add an AI receptionist on that number that books into this calendar. | Twilio ≈ $1–2/mo per number plus ~1¢/min and text; an AI receptionist adds a few cents per call |
| **Same data on phone and iPad/computer** | Move storage to a hosted database with a login (Supabase or Firebase). | Free tier covers one salon |
| **Clients book themselves online** | Public booking page that only shows open gaps, writes to the same database. Needs the sync above first. | Free–$25/mo |
| **Automatic reminder texts** | Scheduled job + Twilio SMS, the night before. Needs the sync above. | ~1¢ per text |
| **Card payments, deposits, no-show fees** | Square or Stripe payment links. | Their standard fees |

Honest take: off-the-shelf tools (Square Appointments, Vagaro, GlossGenius) already do all of the above for $0–$50/month. This app is worth it if Debbie wants something simple, her own, with color formulas front and center and no monthly bill. If she wants online booking plus auto-reminders plus payments tomorrow, one of those tools is cheaper than building all of it.

## Files

```
index.html            the whole app (HTML + CSS + JS, no dependencies)
manifest.webmanifest  home-screen install info
sw.js                 offline support
icon.svg, icon-*.png  app icons
```
