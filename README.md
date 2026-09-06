# Skill Saarthi — SIH 2026 Prototype

A longitudinal skilling-outcome platform that tracks a learner's journey from training to sustainable employment.

**Created by Rishav Raj**

---

## Tech Stack

| Layer          | Technology                            |
| -------------- | ------------------------------------- |
| Frontend       | Next.js 16, TypeScript, Tailwind v4   |
| UI Components  | shadcn/ui, Lucide Icons, Recharts     |
| Backend/DB     | Supabase (PostgreSQL)                 |
| Authentication | Supabase Auth (email/password)        |
| AI (Phase 3+)  | Gemini API                            |

---

## Getting Started

### Prerequisites

- Node.js 18+
- npm
- A [Supabase](https://supabase.com) account (free tier works)

### 1. Install Dependencies

```bash
npm install
```

### 2. Create a Supabase Project

1. Go to [supabase.com/dashboard](https://supabase.com/dashboard)
2. Create a new project
3. Copy your **Project URL** and **anon public key** from Settings → API

### 3. Configure Environment Variables

Copy the example env file and fill in your credentials:

```bash
copy .env.example .env.local
```

Edit `.env.local`:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here
```

### 4. Run the Database Schema

1. Open Supabase Dashboard → SQL Editor
2. Copy and paste the contents of `database/schema.sql`
3. Click **Run**

This will create:
- The `profiles` table with RLS policies
- Auto-profile creation trigger on user signup
- Role enum (`student` / `admin`)

### 5. Configure Supabase Auth

In Supabase Dashboard → Authentication → Settings:

- **Enable Email provider** (should be on by default)
- Set **Site URL** to `http://localhost:3000`
- Add `http://localhost:3000/auth/callback` to **Redirect URLs**
- (Optional) Disable email confirmation for easier local testing

### 6. Start Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Testing Authentication

### Create a Student Account

1. Go to `/signup`
2. Fill in name, email, password
3. Select "Student / Trainee"
4. Accept terms and submit
5. (If email confirmation is on) Check email and confirm
6. Log in at `/login`
7. You should be redirected to `/student`

### Create an Admin Account

1. Go to `/signup`
2. Fill in name, email, password
3. Select "Admin / Government"
4. Accept terms and submit
5. Log in at `/login`
6. You should be redirected to `/admin`

### Verify Role-Based Access

- Student logged in → visiting `/admin` redirects to `/student`
- Admin logged in → visiting `/student` redirects to `/admin`
- Logged out → visiting `/student` or `/admin` redirects to `/login`

---

## Project Structure

```
src/
├── app/
│   ├── (public)/          # Public pages (landing, about, faq, etc.)
│   ├── (dashboard)/       # Protected pages (student, admin)
│   ├── auth/callback/     # Supabase auth callback handler
│   ├── layout.tsx         # Root layout
│   └── globals.css        # Design tokens + theme
├── components/
│   ├── ui/                # shadcn/ui components
│   ├── navbar.tsx         # Public navbar
│   ├── footer.tsx         # Public footer
│   ├── dashboard-nav.tsx  # Dashboard sidebar
│   ├── dashboard-shell.tsx
│   └── theme-provider.tsx
├── hooks/
│   └── use-auth.ts        # Auth state hook
├── lib/
│   ├── supabase/
│   │   ├── client.ts      # Browser Supabase client
│   │   ├── server.ts      # Server Supabase client
│   │   └── middleware.ts   # Session refresh + route protection
│   └── utils.ts           # Tailwind merge utility
├── types/
│   └── database.ts        # TypeScript DB types
└── middleware.ts           # Next.js middleware entry

database/
├── schema.sql             # Full database schema
└── seed.sql               # Seed data (empty for Phase 2)
```

---

## Phases

| Phase | Status      | Description                                 |
| ----- | ----------- | ------------------------------------------- |
| 1     | ✅ Complete | Public UI, landing page, design system      |
| 2     | ✅ Complete | Auth, database, roles, protected dashboards |
| 3     | 🔲 Planned  | AI skill-gap analysis, Gemini API           |
| 4     | 🔲 Planned  | Employment tracking, follow-ups, wages      |
| 5     | 🔲 Planned  | Government analytics, deployment            |

---

## License

SIH 2026 Prototype — Not for production use.
