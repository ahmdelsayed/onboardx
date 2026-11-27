# OnboardX - Digital Onboarding (eKYC) for FlexiPay

Front-end for an AI-powered customer onboarding system built as a DEPI graduation project by
**OnboardX Automation Systems**, for the BNPL client **FlexiPay**.

The site is static HTML/CSS/JS (no build step) and talks to a live n8n backend with a Neon
Postgres database. Every number and case shown on the site is real data from that database.

## Pages

| Page | What it does |
| --- | --- |
| `index.html` | Arabic RTL landing: brand, QR intake, journey, capabilities, enterprise controls |
| `app.html` | Customer intake: consent, ID card (front/back) + selfie capture with quality check and retakes |
| `status.html` | Live KPI dashboard from `/webhook/onboardx-stats` |
| `cases.html` | Case tracking by application ID (`OBX-...`), full audit timeline and reviewer actions |
| `analytics.html` | Decision mix, automation vs human review, event distribution, live from the same stats endpoint |
| `architecture.html` | Five-stage pipeline and how the pieces fit |
| `security.html` | Security and compliance: controls, data lifecycle, PDPL / KYC-AML / GDPR matrix, roles, incident response |
| `assistant.html` | Arabic assistant for reviewers, answers from live data via `/webhook/onboardx-ask` |
| `docs.html` | API reference for every endpoint |
| `tour.html` | 15-minute demo script for the presentation, plus expected committee questions |

## Live endpoints used by the front-end

Base: `https://ahmed2404843.app.n8n.cloud/webhook/`

- `POST /onboardx-intake` - submit an application
- `POST /onboardx-review-action` - reviewer decision (approve / reject / more info)
- `GET /onboardx-review` - reviewer dashboard
- `GET /onboardx-stats` - aggregate stats
- `GET /onboardx-api-case?id=OBX-...` - single case with timeline
- `POST /onboardx-ask` - assistant, body `{"question": "..."}`

## Hosting

Static files, served by GitHub Pages from the `main` branch root:

`https://ahmdelsayed.github.io/onboardx/`

All internal links are relative, so the site works from any static host or a local folder.
The QR code on the landing page encodes the `/app.html` URL above.

## Demo data

The database is seeded with five fictional cases (`OBX-DEMO001` to `OBX-DEMO005`) covering
auto-approve, reject, human review, and a compliance hold with a screening hit and a reviewer
action, so the dashboard, analytics and assistant all have something to show.

## Notes

- The assistant currently runs a rules engine (`rules-v1`) over live data. The page is wired so
  an LLM-backed retrieval (RAG) engine can replace it without a front-end change.
- No real customer data is used. Screening hits are demo values.
