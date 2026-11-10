---
name: availability-reply
description: Answer a guest's availability inquiry for a vacation rental with real EasyHost data and draft the reply to send. Use when the owner pastes or describes a guest message like "is the suite free next weekend?", "יש לכם פנוי ב-12.3?", "מה פנוי בחנוכה לזוג?", asks which units are free on dates, or wants a reply to a booking inquiry from WhatsApp, Instagram or email.
---

# Availability reply from EasyHost

The owner gets inquiries all day and has to check the calendar, the price and the unit before answering. This skill checks EasyHost and writes the reply; the owner sends it and takes the booking in EasyHost.

If the EasyHost tools are not available, ask the owner to connect EasyHost (Customize → Connectors in Claude, or `/mcp` in Claude Code) and stop.

## 1. Pin down the dates

Turn the request into a check-in and a check-out date. Check-out is the morning the guest leaves, so "Thursday to Saturday" is two nights. Israeli guests often write d.m or d.m.yy; Jewish holidays and "the weekend" (usually Thursday or Friday to Saturday) need real dates. If the dates are ambiguous, ask the owner once rather than guess. State the dates you used.

## 2. Check

- `check_availability` with `check_in` and `check_out`. Pass `unit_name` when the guest named a unit; it matches part of the name, so "סוויטה" finds "סוויטת הגפן". Without it, every unit is checked.
- A unit that is taken comes back with the clashing stay. Do not share that guest's details in the reply.
- If the requested unit is taken, check every unit for the same dates and offer the free ones. If none is free, try one night earlier or later and say that you did.
- `list_units` gives capacity and the nightly price. Match capacity to the number of guests. The price is the unit's base nightly rate: present it as a starting price, because weekends, holidays and discounts may differ.

## 3. Draft the reply

Write it in the guest's language, usually Hebrew, warm and short, ready to paste into WhatsApp:

- Whether the dates are available, and for which unit.
- The alternatives, if the first choice is taken.
- The price as "starting from" per night, only if the owner wants prices shown.
- One question that moves the booking forward, such as the number of guests or whether to hold the dates.

Show the owner the facts behind the draft in one or two lines (dates, units checked, free units) so they can catch a mistake before sending.

## Limits

Claude can't hold, book or send. The owner sends the reply and creates the booking in the EasyHost app at https://app.easyhost.co.il. Availability can change between the check and the booking, so the draft should not promise the dates are held.
