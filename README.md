# ChatGent

Your AI dating coach. Upload a screenshot of your dating app chat and get natural UK‑English replies and smart date ideas near you. ChatGent is built on Google Gemini and a simple credit system so there is no subscription.

![Screenshot](https://storage.googleapis.com/aistudio-project-files/55a9b895-5f56-4217-a16f-d1222e039433/Wingman-Screenshot.png)

---

## Features

* **Screenshot understanding**: send a JPG or PNG and the AI extracts the recent context, tone and interests.
* **Multi‑style replies**: 3 to 5 short options, for example playful, sincere or curious.
* **Local date ideas**: optional search for restaurants, parks and events near a saved location.
* **Credit system**: starter credits for free use, then top up with packs. Repeated searches in the same area within 24 hours do not spend more credits.
* **Respect and safety**: British English tone, avoids manipulative or sexual content, encourages consent and honesty.

---

## Tech stack

* **Framework**: Next.js with React and TypeScript
* **UI**: Tailwind CSS
* **AI**: Google Gemini (1.5 Flash or newer)
* **Search providers**: Google Places API for restaurants and parks, Ticketmaster Discovery for events (optional)
* **Payments**: Stripe Checkout for one‑off credit packs (optional)
* **Storage**: swap the in‑memory credit ledger for Firestore, Supabase or Postgres in production

---

## Architecture

* `pages/api/analyse.ts` calls Gemini with the image and returns structured JSON: reply suggestions, interests and search intents.
* `pages/api/places.ts` and `pages/api/events.ts` perform optional local searches and charge credits only on successful results.
* `lib/credits.ts` implements a simple ledger with idempotency. Replace with your database adapter before launch.
* `pages/index.tsx` is the minimal web app. `landing.html` (or your chosen route) is the marketing page.

---

## Getting started

### Prerequisites

* Node 18 or newer
* A Google Gemini API key
* A Google Maps Platform key with Places enabled (optional but recommended)
* A Ticketmaster API key for events (optional)
* Stripe account and Price IDs if you want real payments (optional)

### 1. Clone and install

```bash
git clone https://github.com/your-username/chatgent.git
cd chatgent
npm install
```

### 2. Configure environment

Create `.env.local` in the project root:

```dotenv
# Gemini
GEMINI_API_KEY=your_gemini_key

# Places and events (optional)
GOOGLE_MAPS_API_KEY=your_google_maps_key
TICKETMASTER_API_KEY=your_ticketmaster_key

# Stripe (optional if selling credits)
STRIPE_SECRET_KEY=sk_live_or_test
STRIPE_WEBHOOK_SECRET=whsec_...
# Use your Stripe Price IDs for each pack
NEXT_PUBLIC_PACK_TASTER=price_...
NEXT_PUBLIC_PACK_STARTER=price_...
NEXT_PUBLIC_PACK_REGULAR=price_...
NEXT_PUBLIC_PACK_PRO=price_...
```

Notes:

* Do not commit `.env.local` to version control.
* If you see code referencing `MAPS_API_KEY`, set it to the same value as `GOOGLE_MAPS_API_KEY` or update the code to use a single name.

### 3. Run the dev server

```bash
npm run dev
# open http://localhost:3000
```

### 4. Stripe webhook for local testing (optional)

If you enable real purchases, run an HTTPS tunnel and forward the webhook:

```bash
# example with Stripe CLI
stripe listen --forward-to localhost:3000/api/billing/webhook
```

Create four Prices in Stripe for the credit packs and paste the IDs into your env file. The webhook grants credits after payment.

---

## Credit system defaults

* Starter credits on sign up: 30
* Monthly free top up: 15 per month
* Streak bonus: 1 per day, up to 5 per week
* Costs per action: AI analysis 1, restaurant 3, park 2, event 1
* Cache rule: repeating the same keyword in the same area within 24 hours is free
* Refund rule: if a search returns zero results the debit is reversed automatically

These values are easy to change in `lib/credits.ts` and the UI copy.

---

## Commands

```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  }
}
```

---

## Project structure

```
chatgent/
├─ pages/
│  ├─ index.tsx              # App UI
│  ├─ api/
│  │  ├─ analyse.ts          # Gemini image analysis
│  │  ├─ places.ts           # Restaurants and parks
│  │  ├─ events.ts           # Events search (optional)
│  │  └─ billing/
│  │     ├─ create-checkout-session.ts
│  │     └─ webhook.ts
├─ components/               # UI bits like Balance, BuyCredits, CostPill
├─ lib/
│  ├─ credits.ts             # Credit ledger abstraction
│  ├─ geo.ts                 # Helpers for location
│  └─ types.ts               # Shared types
├─ public/
├─ landing.html              # Marketing page (dark gradient background)
└─ README.md
```

---

## Privacy and safety

* Avoid storing raw screenshots unless absolutely necessary. If you must, encrypt at rest and delete quickly.
* Redact e‑mail addresses and phone numbers in logs and prompts.
* The model should refuse disrespectful, manipulative or sexual content and encourage consent and safety.

---

## Deployment

* **Vercel**: import the repo, set environment variables in Project Settings, then deploy.
* **Render, Fly.io or Railway**: create a service, add env vars, run `npm run start` after `npm run build`.
* Add a cron or scheduled job to run the monthly credit top up endpoint.

---

## Roadmap

* Proper database store for credits and user profiles
* Sign in with Google or Apple
* Feedback buttons to rate suggestions and improve prompts
* More providers for events and experiences
* In‑app A/B tests for credit costs and pack pricing

---

## Contributing

Issues and pull requests are welcome. Please keep the tone and copy British and respectful.

---

## Licence

MIT. See `LICENCE` for details.
