# OnboardX (FlexiPay car installments)

Arabic-first AI eKYC onboarding for a car showroom installment product (Egypt, EGP, +20 mobiles).

Live site (GitHub Pages): https://ahmdelsayed.github.io/onboardx/

- Pages are static files in this repo: index, app (apply), track, showroom, review, review-case, contract, login (role screen), assistant, architecture, security, docs.
- The backend is a single n8n Cloud workflow. The pages call its webhooks (`/webhook/ox-*`) as an API only, with CORS enabled for this site.
- Showroom QR opens https://ahmdelsayed.github.io/onboardx/app.html?m=SHOW-001
- The Admin/User role screen is a preview of the two views, not real authentication.
