---
name: daily-briefing
description: Give a vacation rental owner a short briefing from their EasyHost data - who arrives and leaves today or this week, who has not paid, which units stand empty. Use when the owner asks "what's happening today", "who is arriving", "who hasn't paid", "תן לי סיכום בוקר", "מי מגיע השבוע", "מי לא שילם", or wants a morning or weekly summary of the property.
---

# Daily briefing from EasyHost

EasyHost is a management system for Israeli vacation rentals (zimmers, suites, villas). The briefing turns the owner's bookings into the few things they need to act on today.

If the EasyHost tools are not available, ask the owner to connect EasyHost (Customize → Connectors in Claude, or `/mcp` in Claude Code) and stop.

## Gather

1. `list_bookings`: up to 8 open stays, soonest first, with unit, guests, total and payment status, plus `totalCount`. If it returns `scope="recent"`, nobody has an open stay: say so plainly and do not present past stays as arrivals.
2. `list_units`: every unit, to spot units with no stay in the period.
3. For "which units are free this weekend" or any other date question, call `check_availability` with explicit dates. Do not infer that a unit is free from `list_bookings`, because it returns at most 8 stays.

Work out "today", "tomorrow" and "this week" from the current date, and write the dates you used in the answer. EasyHost returns dates as d.m.yyyy.

## Write

Answer in the owner's language, usually Hebrew. Keep it short enough to read on a phone:

- **Arriving**: unit, guest name, number of guests, nights.
- **Leaving**: unit and guest.
- **Not paid**: guest, unit, amount. Statuses come in Hebrew: שולם paid, שולם חלקית partly paid, שולמה מקדמה deposit paid, ממתין לתשלום awaiting payment, לא שולם unpaid, לא נדרש תשלום no payment needed. Everything except שולם and לא נדרש תשלום still has money due.
- **Empty**: units with no stay in the period, only if the owner asked about the week or about availability.
- One line on anything that needs a decision, such as a pending booking (ממתין) or an unpaid stay arriving today.

If `totalCount` is larger than what came back, say that the list shows only the nearest stays and that the full list is in the EasyHost app.

## Limits

The connection is read-only. Claude cannot confirm, change or cancel a booking, mark a payment or message a guest. When the owner asks for one of these, say it is done in the EasyHost app at https://app.easyhost.co.il, and offer to draft the message for them to send.

Guest phone numbers and emails are personal data. Show them only when the owner asks for them or needs them for the next step.
