# Changelog

All notable changes to this project are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Versioning follows [Semantic Versioning](https://semver.org/).

---

## [1.3.0] — 2026-04-06

### Added
- Edit and delete session functionality in teacher dashboard and admin page
- Confirmation screen before deleting a session (shows registration count)
- Past sessions section on public booking page with attendee count badge
- Past sessions section in teacher dashboard
- Chronological sorting for upcoming sessions (soonest first)
- Most-recent-first sorting for past sessions
- Open Graph and Twitter Card meta tags for social sharing thumbnail
- Dedicated `og-image.jpg` (1200×630) with bowl photo and SRMD logo overlay
- Absolute URL support for OG image (required for WhatsApp previews)
- Separate `admin.html` page (hidden teacher dashboard, not linked from public site)
- Hero banner added to `admin.html` matching the public site

### Changed
- About section text updated — therapist names removed, focus on certification credentials
- "Welcome to SRMD Yoga Sound Healing — San Francisco Chapter" em dash changed to comma
- "What to expect" bullet 2 updated to "45 minutes of live sound healing"
- OG description removed — image-only preview for cleaner WhatsApp sharing

### Fixed
- Unescaped apostrophe in "You're registered!" causing blank page on some browsers
- OG image relative path changed to absolute URL for WhatsApp compatibility

---

## [1.2.0] — 2026-04-04

### Added
- Supabase database integration — RSVPs and sessions now persist across page loads
- PIN-locked teacher dashboard (4-digit keypad)
- Lock/unlock button in dashboard header
- Demo mode — app works fully without Supabase connected, using sample data
- Verbose error messages from Supabase (shown in UI, not just console)
- Pre-deployment JS syntax validation script (`validate_html.py`)

### Changed
- Teacher dashboard moved to separate `admin.html` (hidden from public)
- Single-file version (`sound_bath_rsvp_final.html`) retains both tabs

### Fixed
- Supabase RLS policies corrected — added missing `INSERT` policy for sessions table
- `saveSession` error now surfaces real Supabase error message instead of generic text

---

## [1.1.0] — 2026-03-28

### Added
- SRMD Yoga logo in hero banner (transparent background, yellow text version)
- Maroon logo variant for About card
- About section merged into Book a Session tab
- "What to expect" steps section
- SRMD Yoga affiliation link (srmdyoga.org)
- Teacher bio and CMA/YACEP certification details
- Session instruments field
- CSV export for participant lists per session
- Remove participant button in dashboard
- Fill-rate progress bars on dashboard session cards
- Estimated revenue metric

### Changed
- Hero banner updated to use uploaded singing bowl photograph
- Black background removed from logo (transparent PNG)
- Colour scheme updated to match SRMD Yoga brand (maroon #7B2D2D, gold #F2C01B)

---

## [1.0.0] — 2026-03-20

### Added
- Initial release
- Public booking page with upcoming session cards
- RSVP form (name, email, phone, notes)
- Registration confirmation screen
- Teacher dashboard tab with session overview
- Add new session form
- Participant list per session
- Spot count badges (open / full)
- Mobile-responsive layout
- Tibetan bowl hero banner image
- Two-tab interface (Book a session / Teacher dashboard)
