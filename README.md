# Still I Rise

A mobile-first, local-only weight, food, and activity journal. React, TypeScript, Vite, Tailwind CSS and Recharts. No backend or account is required to run it.

## Run

```sh
npm install
npm run dev
```

Production: `npm run build`, then serve `dist/` over HTTPS (or localhost for testing). The build creates a versioned service worker. PWA/offline support is available in production builds, not the Vite development server. On iPhone, open the HTTPS site in Safari, use Share → Add to Home Screen, and open it once while online.

## Data

Data lives in this browser's localStorage under `dayline-v1`. Settings → Export JSON provides a complete backup. CSV includes daily summaries, with weight in kg. JSON import validates the entire backup and asks before replacing data. Clearing browser storage deletes local records. Different devices/browsers do not sync. Manual daily calories override itemized food totals; “Use food total” removes that override. Weight is stored in kg and converted for display. Measurements use cm.

## Analytics

Seven-day moving averages use calendar windows with at least four recorded weights. Weekly, 14-day and 30-day changes compare two complete independent average windows. Missing entries are not zeros. Calorie averages prefer completed days and label the recorded-day fallback. Complete-watch step averages exclude partial, unknown and not-wearing days. Workout calories are never added to the daily Move total. Preferred pace is a display preference and never changes calorie targets. The initial 2350 kcal target can be changed or disabled; it is not medical advice.

## Checks

`npm test` runs analytical and backup-validation tests (Node 22+). `npm run build` checks TypeScript before bundling. See `VERIFICATION.md` for this delivery's checks and device limitations.

## Update and migration

Still I Rise preserves the original storage key `dayline-v1` and PWA identity. Version 1 records migrate to version 2 after complete validation; the raw original backup is retained under `dayline-v1-before-v2` and can be exported in Settings. Existing dates and values are preserved. Fresh installs and legacy migration add only a 105 kg weight entry for 2026-10-03 when absent. Calories, steps and Watch energy remain missing.

Today supports editable food estimates parsed locally from pasted text, recent foods, saved meals, separate workout and daily Watch summaries, tags, and completed-day status. JSON contains all fields and templates; CSV contains summary columns plus nested JSON fields. No GPT API or HealthKit connection is used.

## Structure

`src/types.ts`: data interfaces. `src/services/storage.ts`: repository boundary for future persistence adapters. `src/utils.ts`: calculations and import validation. `src/components.tsx`: reusable cards, inputs and charts. `src/App.tsx`: application navigation and workflows. `src/style.css`: responsive layout, safe areas and themes.

## GitHub Pages

In repository Settings > Pages choose GitHub Actions as Source. Push to main or manually run Deploy Still I Rise. The workflow builds and tests before publishing dist. Expected project URL: https://fauxxx44.github.io/StillWeRise/ . Relative asset, manifest and service worker paths support the project subdirectory.

On iPhone open the deployed HTTPS URL in Safari, choose Share > Add to Home Screen, then launch it once online. Localhost data does not transfer automatically; export JSON from the old browser and import it on iPhone.
