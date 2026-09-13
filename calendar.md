---
layout: default
title: Calendar
permalink: /calendar/
---

# Seminar Calendar

Click any event to open that seminar's page (details + flyer).

<div id="calendar"></div>

<script src="https://cdn.jsdelivr.net/npm/fullcalendar@6.1.11/index.global.min.js"></script>
<script>
  document.addEventListener('DOMContentLoaded', function () {
    var calendarEl = document.getElementById('calendar');
    var calendar = new FullCalendar.Calendar(calendarEl, {
      initialView: 'dayGridMonth',
      height: 'auto',
      events: '{{ "/seminars.json" | relative_url }}',
      eventClick: function (info) {
        info.jsEvent.preventDefault();
        if (info.event.url) { window.location.href = info.event.url; }
      }
    });
    calendar.render();
  });
</script>

## Sync the whole semester to your calendar

Subscribe once and every seminar we post — including future ones — shows up
automatically. This is a **live subscription**, not a one-time import: your
calendar app checks the link periodically and pulls in new/changed seminars
on its own.

- **Outlook (desktop or web):** Calendar → Add calendar → Subscribe from web,
  then paste this link:
  `{{ site.url }}{{ '/calendar.ics' | relative_url }}`
- **Google Calendar:** Settings → Add calendar → From URL → paste the same
  link above.
- **Apple Calendar:** File → New Calendar Subscription → paste the same link.

(The link only works once `url:` is set to your site's real address in
`_config.yml` — see the README.)

Prefer to add just one seminar instead of the whole semester? Each seminar's
own page has "Add to Google Calendar" / "Add to Outlook" links for that
single event.
