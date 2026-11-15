# LifeLink: Blood Donation Management System

LifeLink is a full-stack web app that connects blood donors and patients. Donors register once, patients search by blood group and city, and requests are matched and accepted in real time.

**Live demo:** https://deluxe-malasada-0fe6b7.netlify.app
*(Currently private. This link will open for everyone once the site is made public.)*

## Features

- **Public donor search** by blood group and city. Contact details stay hidden for logged-out visitors.
- **Donor registration and login** (name, email, phone, blood group, city).
- **Patient registration and login.** Logged-in patients can see donor email and phone.
- **Blood requests.** Patients post a request with contact details and an optional emergency flag, then follow its status: pending, accepted, completed.
- **Donor dashboard.** Donors toggle their availability, see open requests matching their blood group and city, and accept one.
- **Real-time updates** using Supabase Realtime, so a patient sees the moment a donor accepts.
- **Privacy rules in the database.** Row Level Security decides who can read what, so the rules still hold even if someone bypasses the web pages.

## Privacy model

| Who | Can see |
| --- | --- |
| Logged-out visitor | Donor name, city, blood group, availability (via a public view). No email or phone. |
| Donor | Only their own full profile. Cannot read other donors' emails. |
| Patient (logged in) | Full donor details, including email and phone. |

## Tech stack

- **Frontend:** plain HTML, CSS and JavaScript (no build step)
- **Backend:** [Supabase](https://supabase.com) (PostgreSQL, Auth, Row Level Security, Realtime)
- **Hosting:** Netlify

## Project structure

```
index.html     Public donor search
signup.html    Donor registration
donor.html     Donor login and dashboard
patient.html   Patient login, donor search with contacts, blood requests
schema.sql     Database tables, views, access rules and realtime setup
```

## Run it yourself

1. Create a free project at [supabase.com](https://supabase.com).
2. Open **SQL Editor**, paste the contents of `schema.sql`, and run it.
3. Go to **Authentication, Sign In / Providers, Email** and switch **Confirm email** off while testing.
4. Open **Project Settings, Data API** and copy your **Project URL** and **publishable (anon) key**.
5. In each of the four `.html` files, replace the values of `SUPABASE_URL` and `SUPABASE_KEY` near the bottom of the file with your own. The URL ends at `.supabase.co`.
6. Double-click `index.html` to open it in your browser, or drag the folder onto Netlify Drop to host it.

> Only ever use the **publishable (anon)** key in these files. Never commit the secret or service role key.

## Known limitations

- Emergency alerts by email or SMS are not built yet. Urgent requests are only highlighted on the donor dashboard.
- Email confirmation is switched off for testing and should be enabled before real use.
- Any donor can accept any request in their area. This is fine for a first version but should be tightened.
- No age check or last-donated date yet.
- This project handles contact and health-related information. Add privacy and consent wording before real people use it.

## Roadmap

- Donor profile editing (for example, updating city after moving)
- Age check and last-donated date
- Email and SMS emergency alerts
- Page-to-page polish and an admin view
