# Semester Seminar Series — Jekyll Site

A markdown-driven site for posting seminar announcements. Each seminar is one
markdown file with front matter (title, speaker, date, location, flyer image).
The homepage, archive page, and calendar are all generated automatically from
those files — you never edit HTML or maintain a separate calendar.

## ⚠ Please review before publishing

This starter set was pre-filled from the flyers/abstracts/bios in your
`MECH797_seminars` folder. A few things need a human check before this goes
live:

- **Khaled Noubani's talk** (`_seminars/2026-01-21-noubani.md`) — the flyer
  text says "Wednesday, January 21, 2026," but the original file name implied
  January 29. Jan 21, 2026 really is a Wednesday and Jan 29 is a Thursday, so
  the printed date was used — please confirm with the organizers.
- **Serge Maalouf's talk** (`_seminars/2026-03-26-maalouf.md`) — the source
  documents never state a room/venue or an end time. Location is marked
  `TBD — location to be confirmed with the Mechanical Engineering Department`
  and end time defaults to a placeholder 1 hour after the start. Please fill
  in the real values once known.
- **Speaker photos** — real headshots were found for 9 of the 12 speakers
  (3 cropped from their own flyer, 6 found on official university/personal
  pages). Three speakers had no usable photo available (Marwan Hariz, Nura
  Habbaba, Elie Ghossain) and currently show a plain maroon initials
  placeholder in `assets/speakers/` — swap in a real photo for these
  whenever you have one, by replacing the image file (same filename) or
  updating the `photo:` path in that seminar's front matter.

## Structure

```
_config.yml           site settings
_seminars/             ← one .md file per seminar (this is what you edit each week)
  TEMPLATE.md           copy this to add a new seminar
assets/flyers/          flyer images referenced by seminars
assets/css/style.css    styling
index.md                homepage (upcoming / past, auto-generated)
calendar.md             calendar view (auto-generated from seminar dates)
archive.md              full list of every seminar with flyer thumbnails
_layouts/                page templates (you shouldn't need to touch these)
```

## Adding a new seminar (the only regular task)

1. Copy `_seminars/TEMPLATE.md` to a new file named `_seminars/YYYY-MM-DD-short-slug.md`
   (the date in the filename doesn't have to match `date:` in front matter, but
   keeping them the same avoids confusion).
2. Fill in the front matter: `title`, `speaker`, `affiliation`, `date`,
   `start_time`, `end_time` (24-hour `HH:MM`, e.g. `"15:00"` — these drive the
   calendar and the "Add to Outlook/Google" links), `location`, `flyer`,
   `photo`, `abstract`, `bio`, `tags`. **Delete the `published: false` line**
   that came from the template — that line is only there to keep the blank
   template itself from showing up as a fake seminar on the live site.
3. Drop the flyer image (PDF-exported PNG/JPG works best) into `assets/flyers/`
   and point `flyer:` at it, e.g. `/assets/flyers/2026-10-15-doe.png`. Drop a
   square headshot of the speaker into `assets/speakers/` and point `photo:`
   at it, e.g. `/assets/speakers/2026-10-15-doe.png` — it appears next to the
   seminar details and as a thumbnail on the homepage/archive. If you don't
   have a headshot yet, just omit `photo:` and the page still works fine.
4. Save. The homepage, calendar, archive page, and calendar subscription feed
   all update automatically — nothing else to edit.

## Converting a PDF flyer to an image

If a flyer only exists as a PDF, convert its first page to an image (macOS
has Preview: open the PDF, File → Export → PNG). From the command line with
`poppler` installed: `pdftoppm -png -r 150 -f 1 -l 1 flyer.pdf out`.

## Before you deploy: set your real site URL

Open `_config.yml` and set `url:` to your site's actual address, e.g.
`url: "https://yourdept.github.io"`. This is required for the calendar
subscription link and the "Add to Outlook/Google" links to point at the
right place — without it they'll be broken.

## Running it locally

```bash
gem install bundler
bundle install
bundle exec jekyll serve
```

Then open http://localhost:4000

## Publishing for free with GitHub Pages

1. Push this folder to a GitHub repo.
2. In the repo's Settings → Pages, set the source to the `main` branch (root).
3. If your site will live at `username.github.io/repo-name` (not a root
   `username.github.io` repo), set `baseurl: "/repo-name"` in `_config.yml`.
4. Your site will be live at the URL GitHub Pages shows you within a minute
   or two of pushing.

GitHub Pages builds Jekyll sites automatically — no build step to configure.

## Calendar sync (Outlook, Google, Apple)

`calendar.ics` is a live subscription feed, auto-generated from every
seminar's `date`/`start_time`/`end_time`. Point Outlook, Google Calendar, or
Apple Calendar at `https://yoursite/calendar.ics` (see the "Sync the whole
semester" section on the `/calendar/` page for exact steps per app) and new
seminars appear automatically as you add them — no re-subscribing needed.

Each individual seminar page also has one-click "Add to Google Calendar" /
"Add to Outlook" links for people who just want that one event.

Note: events are generated in "floating" local time (no explicit timezone
embedded), which is fine as long as everyone attending is in your
institution's timezone. If you ever need to support attendees across time
zones, that's a small addition — just ask.

## Notes

- The calendar (`calendar.md`) reads `seminars.json`, which Jekyll generates
  automatically from every file in `_seminars/`. You don't edit `seminars.json`
  or `calendar.ics` directly — both are generated from the same seminar files.
- "Upcoming" vs. "past" on the homepage is based on comparing each seminar's
  `date` to today — no manual sorting needed.
- Speaker headshots live in `assets/speakers/`, separate from the flyers in
  `assets/flyers/`. A few seminars in this starter set use a plain
  maroon "initials" placeholder image instead of a real photo — see the
  note at the top of this README (or the summary you received with this
  site) for which ones, and swap in a real photo whenever you have one.
