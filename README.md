# Welcome page for Google Cloud Run

This project contains a simple Node.js welcome page that can be deployed to Google Cloud Run.

## Run locally

```bash
npm start
```

Open http://localhost:8080/

## Deploy to Google Cloud Run

The site runs as the Cloud Run service `chrishindes-com` in `europe-west1` (project `project-4730f157-aa81-4a28-bea`).

Deploys are automatic: a Cloud Build trigger connected to this GitHub repo rebuilds the container from the `Dockerfile` and deploys it on every push to `main`. Pushes that only change Markdown files (`*.md`) are ignored and don't deploy. To deploy manually from a local checkout instead:

```bash
gcloud run deploy chrishindes-com --source . --region europe-west1 --project project-4730f157-aa81-4a28-bea
```
