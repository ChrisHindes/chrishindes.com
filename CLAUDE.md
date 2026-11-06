# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal welcome page for Chris Hindes (Systems Engineer: data governance, Azure, data migration, workflow automation), deployed to Google Cloud Run. It is a static site served by a small Node.js server with **no dependencies**: there is no build step, linter or test suite.

## Commands

```bash
npm start            # node server.js → http://localhost:8080 (override with PORT)
```

Deploy (replace `PROJECT_ID`):

```bash
gcloud builds submit --tag gcr.io/PROJECT_ID/welcome-page
gcloud run deploy welcome-page --image gcr.io/PROJECT_ID/welcome-page \
  --platform managed --region us-central1 --allow-unauthenticated
```

## Architecture

- `server.js`: a plain `http` server that serves files from `public/`, mapping `/` to `/index.html`. Content types come from a hardcoded `mimeTypes` table, so a new asset type (e.g. `.webp`, `.woff2`) must be added there or it is served as `application/octet-stream`. The server strips query strings, URL-decodes the path and returns 404 for anything that resolves outside `public/`.
- `public/`: everything the site serves. `index.html` holds all page content; `styles.css` holds the light, modern theme. The Inter font loads from Google Fonts, and the favicon is an inline SVG data URI.
- `Dockerfile`: `node:20-slim`, copies the whole repo and runs `npm start` on port 8080, the port Cloud Run expects.
- `aboutme.txt`: the source bio text that the page copy is based on. It is not served.
- The root `headshot.png` is **not** served and differs from `public/headshot.png`. Only the copy in `public/` appears on the site.
