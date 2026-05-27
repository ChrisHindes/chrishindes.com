# Welcome page for Google Cloud Run

This project contains a simple Node.js welcome page that can be deployed to Google Cloud Run.

## Run locally

```bash
npm start
```

Open http://localhost:8080/

## Deploy to Google Cloud Run

1. Build and push the container image:

```bash
gcloud builds submit --tag gcr.io/PROJECT_ID/welcome-page
```

2. Deploy to Cloud Run:

```bash
gcloud run deploy welcome-page \
  --image gcr.io/PROJECT_ID/welcome-page \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated
```

Replace `PROJECT_ID` with your Google Cloud project ID.
