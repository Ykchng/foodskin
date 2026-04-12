# FoodSkin — Food & Eczema Correlation Tracker

Personal tool for tracking food intake and eczema flare-ups to discover dietary triggers.

## What this project is

A PWA (Progressive Web App) that runs on a phone via browser / home screen icon. Built for a single user (personal use) based in Singapore.

## Core workflow

1. **Log food**: Take photo of meal → Gemini AI identifies food items + categories → user confirms/edits → saved with timestamp
2. **Log eczema**: Take photo of flare-up → Gemini AI assesses severity (1-5) → user picks body area (face/neck/arms/body/legs) + adds notes → saved with timestamp. Can also log manually without photo.
3. **Timeline**: Scrollable feed of all entries (food + eczema) in chronological order
4. **Insights**: Rule-based correlation engine that continuously updates. Scans 12-48h window before each flare-up, compares food category frequency in pre-flare windows vs baseline diet, flags disproportionately appearing foods as potential triggers. Needs 10+ meals, 3+ flare-ups, 2+ weeks of data.
5. **Settings**: Export/import JSON, change API key, clear data

## Tech decisions already made

- **AI backend**: Google Gemini API (free tier, model: gemini-2.0-flash). User has their own API key. App designed so Claude/Anthropic API can be swapped in later via a toggle.
- **Data storage**: All local on device (localStorage). Text only — photos are sent to Gemini for analysis but not stored.
- **Data model**:
  - Food entry: `{ id, timestamp, items: string[], categories: string[] }`
  - Eczema entry: `{ id, timestamp, severity: 1-5, bodyArea: string, description: string }`
  - Categories are broad food groups for correlation (e.g. "dairy", "gluten", "seafood", "fried food", "coconut milk", "eggs", "nuts", "caffeine", "alcohol", "spicy food", "processed food", "sugar")
- **No backend server** — everything runs client-side
- **API key stored in localStorage** on user's device only

## Current state

A working React component exists (food-eczema-tracker.jsx in this repo). It has all 5 screens built. It works as a React artifact but needs to be deployed as a real hosted PWA to use camera and API calls.

## Next step: Deploy as PWA

The immediate task is to get this running as a hosted web app the user can access from their phone. Options discussed:
- **Option A**: Vite + GitHub Pages (proper dev setup, better for iteration)
- **Option B**: Convert to single HTML file, push to GitHub Pages (simpler, faster)

The user has Git, a GitHub account, and GitHub connected in Claude Code desktop. They are a non-developer building personal tools — prefer simple, concrete, step-by-step instructions.

## Future plans (not yet built)

- Add option to swap between Gemini and Claude/Anthropic API for photo analysis
- More sophisticated analysis as data accumulates
- Potentially merge with or complement the user's existing spending tracker project (a Python Gmail transaction scraper that outputs Excel to Google Drive)

## Conventions

- Keep it simple — single user, personal tool, no auth, no multi-device sync
- Singapore context (food examples: nasi lemak, teh tarik, hawker food)
- User is non-technical — avoid jargon, give step-by-step guidance
- When in doubt, ask before building
