# EasyHost for Claude

EasyHost (אירוח בקליק) is a management system for Israeli vacation rentals: zimmers, suites, cabins and villas. This plugin lets the owner ask Claude about their own property in plain language, in Hebrew or English: who is arriving today, who has not paid yet, which units are free on given dates, and when a guest last stayed. It also drafts replies to guest inquiries based on real availability.

The connection is read-only. Claude can look things up, but it cannot create, change or cancel bookings, record payments or send messages to guests. Those stay in the EasyHost app.

## What's inside

- **MCP server** `https://app.easyhost.co.il/api/mcp`. You sign in with your EasyHost account (OAuth) and approve access on an EasyHost page. Claude sees only your own account. Tools:
  - `search_guests`: find guests by name, email or phone, with their latest stay.
  - `list_bookings`: upcoming and current stays with unit, guests, total and payment status.
  - `list_units`: your units with nightly price, capacity and status.
  - `check_availability`: whether units are free between two dates.
- **Skills**
  - `daily-briefing`: a short morning or weekly summary of arrivals, departures, unpaid stays and empty units.
  - `availability-reply`: checks a guest's dates, finds alternatives and drafts the reply to send.

## Install (Claude Code)

```
/plugin marketplace add dolevhayut/easyhost-plugin
/plugin install easyhost@easyhost
```

Then run `/mcp`, choose **easyhost** and **Authenticate**. Sign in to EasyHost in the browser and approve access.

Requires an EasyHost account: https://app.easyhost.co.il/signup

## Example questions

- Who is arriving this week, and who has not paid yet?
- Is the suite free from 12.3 to 15.3? If not, which units are?
- A guest asked on WhatsApp if we have something for 2 adults next weekend. Draft a reply.
- Find the guest with the phone 050-1234567 and tell me when they last stayed.

## Data

The plugin sends nothing anywhere except the EasyHost server above. Data the tools return, including guests' names, phone numbers and emails, is shown to you in Claude. EasyHost does not store your questions. Details: https://app.easyhost.co.il/docs/claude and the privacy policy at https://app.easyhost.co.il/privacy

## Support

office@bulldog-adv.com · https://easyhost.co.il
