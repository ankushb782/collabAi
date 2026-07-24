# CollabAI Dynamic Marketplace v4

A deployable full-stack dynamic application for a two-sided creator/brand marketplace. It combines the existing responsive marketplace UI with a Node.js API, role-based authentication, campaign/application workflows, payment-state scaffolding, social account records, historical snapshots, complaints, appeals, analytics and admin endpoints.

## Included

- Separate Brand and Creator signup/login with hashed passwords and JWT sessions
- Creator and brand discovery UI, sponsored/top results and locked profile flow
- Four social-provider connection screens: Instagram, TikTok, YouTube and Facebook
- Demo imports plus environment placeholders for approved provider apps
- JSON persistence starter (`data/db.json`) with a clean adapter file (`lib/db.js`)
- Campaign creation, applications, status workflow and audit logs
- Payment intent/funding demo endpoints designed to be replaced by Stripe/Razorpay webhooks
- Historical social snapshots and transparent authenticity-estimate endpoint
- Complaints, appeals, privacy, refund, copyright and terms pages
- Admin overview endpoint and moderation UI
- Helmet security headers, rate limiting, HTTP-only session cookie and role middleware

## Run locally

```bash
cp .env.example .env
npm install
npm start
```

Open `http://localhost:3000`.

## Important provider limitation

Real Instagram, Facebook, TikTok and YouTube imports require your own developer applications, exact redirect URLs, account authorization, approved scopes and—in many public-use cases—app review. The project keeps credentials server-side and includes demo imports so the complete interface can be tested immediately. The provider adapter routes intentionally return a setup message until approved OAuth adapters are configured.

## Before production launch

1. Replace the JSON store with MongoDB/PostgreSQL and use Redis for sessions/queues.
2. Encrypt provider access/refresh tokens using a managed key service.
3. Implement approved OAuth adapters and scheduled refresh workers.
4. Replace demo payments with Stripe Connect or Razorpay Route, signed webhooks and a legally reviewed marketplace payout flow.
5. Add email verification, password reset, 2FA, file scanning and identity/KYC processes.
6. Obtain legal review for terms, privacy, refunds, creator contracts, tax treatment and escrow language in every operating country.
7. Never market the authenticity score as proof of genuine followers; it is an estimate based on available signals.

## Deploy

Works on Render, Railway, Fly.io or a Node-compatible VPS. Set all environment variables in the host dashboard and use:

- Build command: `npm install`
- Start command: `npm start`

The local JSON database is suitable for testing only. On ephemeral hosting, data may reset after redeployment; connect a production database before accepting real users or payments.


## Dynamic v4 additions

- Database-backed creator and brand discovery
- Live profile editing for both roles
- Persistent collaboration requests and creator pitches
- Persistent shortlists, notifications and direct messages APIs
- Dynamic campaign loading and creation
- Admin user-status management endpoints
- Search results update immediately after profile changes

The included JSON adapter makes every screen dynamic for local testing. For multi-instance production deployment, replace `lib/db.js` with PostgreSQL or MongoDB while preserving the API contract.


## Creator deliverables marketplace

Unlocked creator profiles now include bookable deliverables for Instagram Reels, Stories and Posts; YouTube Shorts and long-form videos; TikTok videos; Facebook Reels/Videos/Live; LinkedIn Posts; Twitch Live and other creator-defined services. Brands can add multiple services and quantities to a persistent cart, enter campaign details and usage rights, review platform fee and tax, and proceed through the demo checkout.

Dynamic API endpoints include `GET /api/creators/:creatorId/services`, creator service CRUD under `/api/creator/services`, order creation/listing under `/api/orders`, and demo funding through `/api/orders/:id/checkout-demo`.

## Latest UI and payment fixes

- Creator email addresses and phone numbers are hidden on public and unlocked profiles.
- Contact information is represented as protected and is intended to be released only after collaboration acceptance or funded payment.
- Checkout is grouped creator-by-creator with an organised order summary, campaign details, usage rights and payment-method sections.
- Brand dashboard amounts now update from the live cart and completed demo orders.
- Creator dashboard pending earnings and funded-order activity update from completed checkout records.
- Demo order and dashboard state is persisted in browser local storage.

For production, enforce contact privacy and payment status on the server as well; browser-only checks are not sufficient security.

## Public deployment package

This package includes `render.yaml`, a health check, production environment placeholders and persistent JSON storage support through `DB_FILE`.

### Deploy on Render

1. Upload this project to a Git repository.
2. In Render, choose **New → Blueprint** and select the repository.
3. Render reads `render.yaml` and creates the Node service and persistent disk.
4. Set `BASE_URL` to the public Render URL, for example `https://your-service.onrender.com`.
5. Add social-provider and payment credentials only in Render environment variables.
6. Redeploy after updating OAuth callback URLs in Meta, TikTok and Google consoles.

The persistent JSON disk is suitable for a public demo or early private testing. Before taking real payments or supporting many concurrent users, migrate to PostgreSQL or MongoDB and Redis-backed sessions.
