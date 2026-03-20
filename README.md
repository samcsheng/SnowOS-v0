# SnowOS — MVP v0

Ski School Management System for Club Med Tomamu · Frontend Prototype

## Stack
- Pure HTML + CSS + Vanilla JS (zero dependencies, zero build step)
- localStorage for all data persistence
- Google Fonts (Cormorant Garamond + DM Sans + DM Mono) via CDN

## Roles
| Role | Identity | Access |
|------|----------|--------|
| Instructor | Sammy Chen | Daily schedule, lesson lifecycle, guest profiles, lesson reports |
| Supervisor | Jason (Supervisor) | Operations dashboard, instructor pool, assignment management |
| Guest | Anna Smith | Upcoming lessons, booking, history, progress profile |

## Lesson Lifecycle
```
scheduled → in_progress → completed → reported
```

## Seed Data
- 1 Resort: Club Med Tomamu
- 10 Instructors (ski & snowboard)
- 50 Guests
- 25 Lesson Templates (CLUB 1–6, SB, TRIDENT, RIDER, PRIVATE)
- ~100 Lessons across 14 days
- Bookings, instructor assignments, lesson reports

Data is generated on first load and persists in localStorage.
Use the **↺ Reset** button in the role bar to regenerate seed data.

## Deploy to Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy from this directory
vercel deploy
```

Or drag and drop this folder into vercel.com/new.

## Local Development

```bash
# No build step required — just open the file
open index.html

# Or serve locally
npx serve .
```

## Architecture Notes

All data access goes through the `Store` object, designed for clean migration to Supabase in v1:
- `Store.getLessons(filters)` → `supabase.from('lessons').select().match(filters)`
- `Store.updateLessonStatus(id, status)` → `supabase.from('lessons').update({status}).eq('id', id)`
- etc.
