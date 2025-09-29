---
title: Campaign
---

## Campaign Calendar

<div id="calendar"></div>

<script>
document.addEventListener('DOMContentLoaded', function () {
  const el = document.getElementById('calendar');

  const cal = new FullCalendar.Calendar(el, {
    initialView: 'dayGridMonth',
    height: 'auto',
    fixedWeekCount: false,
    expandRows: true,
    timeZone: 'Europe/London',
    firstDay: 1,
    locale: 'en-gb',
    headerToolbar: {
      left: 'prev,next today',
      center: 'title',
      right: 'dayGridMonth,listWeek'
    },

    googleCalendarApiKey: 'AIzaSyC0CRXdZ6_EGtd2R1Uw_gxiBkGcaUiKYz0',
    events: { googleCalendarId: '97084ad1a7c1976fc22d25a18cfebc591f5ea24e12737b6cbbead55805ee5822@group.calendar.google.com' },

    // show 18:00 (24h). For 12h, set hour12: true and add meridiem: 'short'
    eventTimeFormat: { hour: '2-digit', minute: '2-digit', hour12: false },

    eventContent(arg) {
      const titleText = (arg.event.title || '').replace(/-/g, ' ');
      const container = document.createElement('div');
      container.className = 'fc-event-custom';

      const line1 = document.createElement('div');
      line1.className = 'fc-event-line1';

      if (arg.timeText) {
        const time = document.createElement('span');
        time.className = 'fc-time';
        time.textContent = arg.timeText; // e.g., 18:00
        line1.appendChild(time);
      }

      const title = document.createElement('span');
      title.className = 'fc-title';
      title.textContent = (arg.timeText ? ' ' : '') + titleText;
      line1.appendChild(title);

      container.appendChild(line1);

      const loc = arg.event.extendedProps && arg.event.extendedProps.location;
      if (loc) {
        const line2 = document.createElement('div');
        line2.className = 'fc-event-location';
        line2.textContent = '📍 ' + loc;
        container.appendChild(line2);
      }

      return { domNodes: [container] };
    },

    eventDidMount(info) {
      const cal = info.view.calendar;
      const timeText = info.event.start
        ? cal.formatDate(info.event.start, { hour: '2-digit', minute: '2-digit', hour12: false })
        : '';
      const loc = info.event.extendedProps?.location || '';
      let tip = info.event.title.replace(/-/g, ' ');
      if (timeText) tip += ' — ' + timeText;
      if (loc) tip += ' @ ' + loc;
      info.el.title = tip;
    }
  });

  cal.render();
});
</script>

## Campaign Log

> A chronological index of our Terraveil sessions.

<!-- sessions:start -->

- **31-08-2025 — Session 0**  
  _Discussed campaign dates, characters and lore._ → [Read](Session-0.md)
- **11-09-2025 — Session 1**  
  _Our tale has not yet begun, but the pieces are moving…_ → [Read](Session-1.md)
- - **11-09-2025 — Session 2**  
  Battle at the edge of the woods! Wolves, mist, and a crystal spined monstrosity. Lavinia falls but is saved, Onyx defeats the beast and claims a runed skull. → [Read](Session-2.md)

<!-- sessions:end -->