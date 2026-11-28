# OnboardX (FlexiPay car installments)

Arabic-first AI eKYC onboarding for a car showroom installment product (Egypt, EGP, +20 mobiles).

Live site (GitHub Pages): https://ahmdelsayed.github.io/onboardx/

One site, one entry point: the root page is the sign-in screen where you pick a role
(عميل / موظف / مدير). Each role sees only its own area.

Pages:
- `index.html` — sign-in / role pick (the entry point)
- `app.html` — customer: catalogue, plan calculator, ID + selfie capture, apply
- `track.html`, `status.html`, `contract.html` — customer follow-up and e-contract
- `review.html`, `review-case.html`, `cases.html` — staff review desk (employee/manager)
- `showroom.html`, `analytics.html` — manager dashboards
- `tour.html`, `architecture.html`, `security.html`, `docs.html`, `assistant.html` — project documentation and AI assistant

Notes:
- The backend is a single n8n Cloud workflow; pages call its webhooks (`/webhook/ox-*`) as an API only, with CORS enabled for this site. Staff sign-in is real (username + password, hashed, session token).
- While the backend is offline, any page works with `?demo=1` (clearly marked demo data; sign-in accepts ahmed / shenouda / maryam with any password).
- Showroom QR opens https://ahmdelsayed.github.io/onboardx/app.html?m=SHOW-001
- Demo ID/selfie images under `assets/demo/` are generated placeholders watermarked DEMO, not real people or documents.
