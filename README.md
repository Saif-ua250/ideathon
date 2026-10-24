# ZeroDrop OPAC

ZeroDrop OPAC is a deterministic, authority-grounded search middleware demo for Koha MARC21 holdings and Indian ETD records. It is intentionally a static Vercel application: no model downloads, no API keys, and no generated catalogue results.

## What is implemented

The browser pipeline has five explicit stages:

1. Academic acronym and course-jargon lookup (`CLRS`, `Sedra Smith`, `PK Nag`, `BJT/MOSFET`).
2. Indian transliteration/name variant expansion.
3. Token-level edit-distance repair constrained to terms present in the local catalogue.
4. LCSH expansion with a live `id.loc.gov` probe and an offline cache for the demo concepts.
5. Verified scoring over local MARC-style records, including biblionumber, call number, subjects, location, and RFID/access status.

It also includes a 20-query benchmark, catalogue view, explainable trace, and zero-result escalation links for IndCat, DELNET, and a purchase suggestion.

## Run locally

Because this is static, any HTTP server works:

```powershell
python -m http.server 3000
```

Open `http://localhost:3000`.

## Deploy to Vercel

Import this repository at [vercel.com/new](https://vercel.com/new). Vercel detects the static `index.html` automatically. No build command or environment variable is required.

The included `vercel.json` keeps clean routes pointing to the single-page app. Replace the demo `CATALOGUE` in `app.js` with records from a protected Koha middleware before production use; do not expose Koha credentials in the browser.
