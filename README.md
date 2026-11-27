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

## Showroom installment flow (the real use case)

A car showroom shows a QR code. The customer scans it, picks a car and an installment plan, reads the ID with the phone
camera (live OCR pre-fills the form, identity fields are locked), takes a selfie, and sees every check run with its real
result. The system then prepares the installment contract, and the showroom sees its customers and their status.

| Page | What it does |
| --- | --- |
| `app.html` | Customer flow on the phone: car and plan, ID capture with frame and crop, review details, selfie, live progress and result |
| `showroom.html` | Showroom dashboard: QR, customers and status, the showroom's own editable catalogue |
| `track.html` | Status by application number, with every check and the next step |
| `contract.html` | Installment contract template with e-acceptance (project template, not legal advice) |
| `review.html`, `review-case.html` | Review desk: cases waiting for a human, extracted data, check results, reviewer decision |
| `login.html` | Staff sign-in (Google), needs a Google client ID |

Honest states: Face++ is not connected, so the face check is UNAVAILABLE and a person decides. Nothing is auto-rejected.
Catalogue prices and model codes are the showroom's own configuration. These copies call the live n8n backend.
