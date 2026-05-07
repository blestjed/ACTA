# ACTA

Action organized. Change proven.

This is a lean ACTA frontend prototype built from an empty repo after the Lovable prompt. It keeps the ACTA black, off-white, red, and gold identity, then leans on slate/navy and verified green for trust. The UI is intentionally modern, minimal, square, and action-first: missions, coordination, progress, and verification.

## Stack

- React + TypeScript
- Vite
- Tailwind CSS with ACTA tokens
- React Router
- Lucide icons
- Supabase client wrapper with placeholder environment values
- CSS-only motion and PWA basics

Heavy libraries from the original prompt were intentionally left out for V1: no query client, no form framework, no dropzone, no animation package. The goal is fewer moving parts.

## Run Locally

```bash
npm install
npm run dev
```

Then open the local URL Vite prints.

## Environment

Copy the sample environment file:

```bash
cp .env.example .env
```

Prototype mode works without Supabase keys:

```bash
VITE_USE_MOCKS=true
```

When ready for live data, add:

```bash
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key
VITE_USE_MOCKS=false
```

Then run `supabase/schema.sql` in the Supabase SQL editor.

## Routes

- `/` landing page
- `/login`
- `/signup`
- `/onboarding`
- `/app/feed`
- `/app/missions`
- `/app/mission/:id`
- `/app/create`
- `/app/profile`
- `/app/profile/:id`
- `/app/admin`

## File Structure

```text
.
├── public/
│   ├── icon.svg
│   ├── manifest.webmanifest
│   └── sw.js
├── src/
│   ├── components/
│   │   ├── ActivityItem.tsx
│   │   ├── AvatarStack.tsx
│   │   ├── BadgeCard.tsx
│   │   ├── CategoryBadge.tsx
│   │   ├── MissionCard.tsx
│   │   ├── MissionForm.tsx
│   │   ├── ProgressBar.tsx
│   │   ├── ProofCard.tsx
│   │   ├── ProofModal.tsx
│   │   ├── RepScore.tsx
│   │   ├── StepItem.tsx
│   │   ├── VerifiedStamp.tsx
│   │   └── index.ts
│   ├── data/mockData.ts
│   ├── layouts/AppLayout.tsx
│   ├── lib/
│   │   ├── registerServiceWorker.ts
│   │   └── supabase.ts
│   ├── pages/
│   │   ├── AdminPage.tsx
│   │   ├── AuthPage.tsx
│   │   ├── CreateMissionPage.tsx
│   │   ├── FeedPage.tsx
│   │   ├── LandingPage.tsx
│   │   ├── MissionDetailPage.tsx
│   │   ├── MyMissionsPage.tsx
│   │   ├── OnboardingPage.tsx
│   │   └── ProfilePage.tsx
│   ├── styles/index.css
│   ├── types/index.ts
│   ├── App.tsx
│   └── main.tsx
├── supabase/schema.sql
├── .env.example
├── package.json
└── tailwind.config.ts
```

## Audit Notes

- Existing code audit: the repo had no source code or dependencies, so there were no legacy bugs to preserve or regressions to isolate.
- Dependency audit: kept dependencies small and purposeful. Supabase is included only as a client wrapper; the current UI runs on mock data.
- Security audit: no secrets are committed. `.env` is ignored. Supabase RLS is included for all tables in `supabase/schema.sql`.
- SEO audit: canonical URL, title, meta description, Open Graph, Twitter Card, JSON-LD, sitemap, robots file, manifest, and preview image are included.
- Accessibility audit: interactive elements use native controls where possible, focus rings are defined globally, and motion respects `prefers-reduced-motion`.
- Product audit: the prototype is now action-first, with cause choice, age filters, mission detail pages, working local join states, action check-ins, and admin review status changes.
- Performance audit: no large bitmap media assets, no runtime animation library, no remote data calls in prototype mode, and route pages share reusable components.
- Production gap: real auth, storage uploads, mission CRUD persistence, and live action review need to be wired from the mock data layer to Supabase queries.

## Launch Checklist Status

- Built: all requested pages, responsive app shell, cause and age filters, mission cards, action check-in modal, create flow, admin queue, profile, landing story, design tokens, CSS motion, PWA manifest/service worker, Supabase schema/RLS.
- Mocked: auth session, role guards, mission CRUD, check-in uploads, GPS capture, badge awards in UI.
- Ready next: replace `src/data/mockData.ts` with Supabase reads/writes and add Supabase Storage for check-in images.

## Free Deployment

Recommended easiest path for a polished funding demo:

1. Push this folder to a GitHub repository.
2. Import the repository into Vercel, Netlify, or Cloudflare Pages.
3. Use build command `npm run build`.
4. Use publish/output directory `dist`.
5. Add the environment variables from `.env.example` only when you are ready to connect Supabase.

For the cleanest first demo, deploy the mocked frontend first. Add Supabase after funders understand the product.
