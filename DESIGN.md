# boxy-legal — Design State

This document is updated each session. It is the authoritative record of current project state.
Read it at session start. Update it before /checkpoint.

## What It Does

boxy-legal is a static HTML micro-site that hosts the legal and compliance pages required for Boxy's A2P 10DLC SMS registration with Twilio. It provides publicly-accessible URLs for Boxy's Mobile Terms of Service, Privacy Policy, and SMS Opt-In Process documentation, which carriers and Twilio require when registering a toll-free number for SMS delivery.

## Architecture

Four standalone HTML files with no build system, no JavaScript, no external dependencies, and no framework. Each page is self-contained with inline CSS. The site is structured as:

- `index.html` — landing page linking to the three legal pages
- `terms.html` — Mobile Terms of Service (single-recipient, personal use program)
- `privacy.html` — Privacy Policy (covers Twilio + AWS as processors, data collection, opt-out)
- `sms-optin.html` — SMS Opt-In Process documentation (documents how the sole operator enrolled via START keyword to toll-free +1-855-410-4957)

There is no hosting infrastructure in this repo. The files are presumably served statically (no server config, no CI, no deployment scripts present).

## Current Implementation State

### Done
- Index page with navigation to all three legal pages
- Mobile Terms of Service covering program description, consent model, STOP/START/HELP keywords, carrier liability, message frequency disclosure
- Privacy Policy covering operator identity, opt-in consent data handling, data collection categories, Twilio/AWS as processors, data storage (AWS us-east-1), opt-out instructions
- SMS Opt-In Process page documenting the `LIGHTPHONE_NUMBER` env var enrollment flow and START keyword confirmation, with exact confirmation message text
- All pages updated for A2P 10DLC toll-free resubmission (as of May 2026): sole-operator framing, no third-party sharing language, campaign-specific consent language

### Not done / stubs
- No hosting config (no Netlify/Vercel/S3 config, no CNAME, no domain records)
- No HTTPS enforcement config
- No robots.txt or sitemap

## Deferred Design Decisions

- Hosting target: unknown from the repo; likely S3 static site or similar given Boxy uses AWS us-east-1, but not configured here
- Whether to add a canonical domain/URL to the pages themselves (currently no absolute URLs)

## What's Next

1. Confirm the site is live and reachable at the URL submitted to Twilio for the toll-free resubmission — verify all three pages return 200
2. If hosting is not yet set up, add deployment config (S3 static site + CloudFront, or equivalent)
3. If Twilio approves the toll-free resubmission, no further changes needed; this repo becomes stable reference material

## Session Log Reference

See `.claude/sessions.md` for session-by-session decisions and task history.
