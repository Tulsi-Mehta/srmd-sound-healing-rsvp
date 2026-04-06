# SRMD Yoga — Sound Healing RSVP System

A lightweight, single-file RSVP and session management website for sound healing teachers. Built for the SRMD Yoga Bay Area chapter and designed to be easily forked by other chapters worldwide.

## Live demo

[srmd-sf-sound-healing.netlify.app](https://srmd-sf-sound-healing.netlify.app)

## Features

**Public booking page**
- About section with teacher credentials and affiliation
- Upcoming sessions with live spot counts
- Past sessions with attendance records
- RSVP form with name, email, phone and notes
- Mobile-friendly, no app required

**Teacher dashboard** (PIN protected)
- Add, edit and delete sessions
- View all registered participants per session
- Remove individual participants
- Export participant list as CSV
- Live fill-rate progress bars and revenue estimates

## Tech stack

| Layer | Tool |
|-------|------|
| Frontend | Vanilla HTML/CSS/JS — single file, no build step |
| Database | [Supabase](https://supabase.com) (free tier) |
| Hosting | [Netlify](https://netlify.com) (free tier) |
| Auth | PIN-based client-side lock (dashboard) |

## Quick start

### 1. Fork this repo

Click **Fork** at the top right of this page.

### 2. Set up Supabase

1. Go to [supabase.com](https://supabase.com) and create a free project
2. Open the **SQL Editor** and run the setup script below
3. Go to **Project Settings → API** and copy your Project URL and anon key

**SQL setup script:**
```sql
create table sessions (
  id bigint generated always as identity primary key,
  title text not null,
  date date not null,
  time text,
  location text,
  capacity int default 20,
  price int default 0,
  instruments text,
  description text,
  created_at timestamptz default now()
);

create table rsvps (
  id bigint generated always as identity primary key,
  session_id bigint references sessions(id) on delete cascade,
  name text not null,
  email text not null,
  phone text,
  notes text,
  created_at timestamptz default now()
);

alter table sessions enable row level security;
alter table rsvps enable row level security;

create policy "Public read sessions"   on sessions for select using (true);
create policy "Public insert sessions" on sessions for insert with check (true);
create policy "Public update sessions" on sessions for update using (true);
create policy "Public delete sessions" on sessions for delete using (true);

create policy "Public read rsvps"   on rsvps for select using (true);
create policy "Public insert rsvps" on rsvps for insert with check (true);
create policy "Public update rsvps" on rsvps for update using (true);
create policy "Public delete rsvps" on rsvps for delete using (true);
```

### 3. Configure the files

Open `index.html` and `admin.html` in a text editor. At the top of the `<script>` block, fill in your values:

```js
var SUPABASE_URL      = 'https://your-project.supabase.co';
var SUPABASE_ANON_KEY = 'your-anon-key-here';
var DASHBOARD_PIN     = 'choose-a-4-digit-pin';  // admin.html only
```

### 4. Add your images

Replace the placeholder values for your logo and bowl image:
- Open the files and search for `LOGO_PLACEHOLDER` and `BOWL_PLACEHOLDER`
- Follow the instructions in the comments to embed your own images as base64

Or simply use any publicly hosted image URL directly in the `src` attributes.

### 5. Update your site URL

In both `index.html` and `admin.html`, update the Open Graph URL:
```html
<meta property="og:url" content="https://your-site.netlify.app"/>
<meta property="og:image" content="https://your-site.netlify.app/og-image.jpg"/>
<meta name="twitter:image" content="https://your-site.netlify.app/og-image.jpg"/>
```

### 6. Deploy to Netlify

1. Go to [netlify.com/drop](https://netlify.com/drop)
2. Drag your folder containing `index.html`, `admin.html`, and `og-image.jpg`
3. Your site is live instantly

To set a custom subdomain: **Site settings → Change site name**

## Customising for your chapter

| What to change | Where |
|----------------|-------|
| Chapter name and city | Search for `San Francisco Chapter` in both files |
| Teacher names and credentials | Search for `Hinal Damani` and `Tulsi Mehta` |
| SRMD Yoga affiliation link | Search for `srmdyoga.org` |
| Hero banner image | Replace `BOWL` base64 variable |
| Logo | Replace `LOGO` and `LOGO_MAROON` base64 variables |
| Dashboard PIN | `var DASHBOARD_PIN` in `admin.html` |
| Social share thumbnail | Replace `og-image.jpg` |

## Security notes

- **Never commit your real Supabase keys or PIN to a public GitHub repo.** Use placeholder values in the repo and fill in real values only in your local deployed copy.
- The dashboard PIN is a client-side convenience lock — it is not a replacement for server-side authentication. For higher-security use cases, consider Supabase Auth or Netlify Identity.
- The Supabase anon key is intentionally limited in scope by RLS policies.

## Version history

See [CHANGELOG.md](CHANGELOG.md)

## Contributing

Pull requests welcome. Please open an issue first to discuss any major changes.

If you set this up for another SRMD chapter, we'd love to hear about it — open a Discussion and share your link!

## License

MIT — free to use, modify and distribute. Attribution appreciated but not required.

---

Built with care for the SRMD Yoga sound healing community.
