# PitchMap PNW

**The community-maintained pitch competition directory for Oregon & Washington entrepreneurs.**

→ Live site: [pitchmappnw.com](https://pitchmappnw.com)  
→ Maintained by: [Leila Kaneda](https://github.com/lkaneda)  
→ Community partner: [RAIN Catalysts](https://raincatalysts.org)

---

## What this is

PitchMap PNW is a simple, free website that helps PNW entrepreneurs find startup pitch competitions in their area. It tracks host organizations, their current status (accepting applications, event scheduled, monitor, inactive), service area, and links out to their websites.

It is **not** auto-scraped or automatically updated. It is updated manually once a week (or as news comes in) by the maintainer, with the help of a Claude AI project that does the research legwork.

---

## How to update the directory

**You only ever edit one file: `data.json`**

Open `data.json` in any text editor (even Notepad works). Everything is plain text. Here's what each competition entry looks like:

```json
{
  "id": "demolicious",
  "name": "Demolicious",
  "org": "Demolicious",
  "url": "https://www.pitchatdemolicious.com",
  "status": "monitor",
  "description": "Portland-based pitch and demo event for early-stage startups.",
  "serviceArea": "portland-metro",
  "location": { "lat": 45.5231, "lng": -122.6765, "city": "Portland, OR" },
  "tags": ["general", "early-stage"],
  "notes": ""
}
```

### Status options (copy/paste exactly):
| Status | Meaning |
|---|---|
| `"accepting"` | 🟢 Currently accepting applications |
| `"scheduled"` | 🟡 Event date announced, registration open or coming soon |
| `"monitor"` | 🔵 No active event — check their site periodically |
| `"inactive"` | ⚫ Has hosted in the past but appears to have gone quiet |

### Service area options:
| Value | Meaning |
|---|---|
| `"portland-metro"` | Greater Portland area |
| `"oregon"` | All of Oregon |
| `"washington"` | Washington state |
| `"pnw"` | Oregon + Washington / broader PNW |

### To change a status:
Find the entry in `data.json`, change the `"status"` value, and save. Example:

```json
"status": "accepting"
```

### To add notes (like a deadline or event date):
Fill in the `"notes"` field:
```json
"notes": "Applications open through April 30, 2025. Event May 15."
```

### To add a new organization:
Copy an existing entry block, paste it at the end of the `"competitions"` array (before the final `]`), and fill in the details. Make sure to add a comma after the previous entry.

### To update the "Last Updated" date:
Change this line near the top of `data.json`:
```json
"lastUpdated": "2025-03-31"
```

---

## How to publish updates (GitHub → Netlify)

1. Go to the GitHub repo: [github.com/lkaneda/pitchmap-pnw](https://github.com/lkaneda/pitchmap-pnw)
2. Click on `data.json`
3. Click the **pencil icon** (Edit this file)
4. Make your changes directly in the browser
5. Scroll down and click **"Commit changes"**
6. Netlify automatically detects the change and rebuilds the site in about 60 seconds

That's it. No code, no terminal, no deployment steps.

---

## How to suggest or accept a community addition

**Via email form:** Anyone can submit via the "Suggest a Listing" form on the site. Submissions go to the maintainer's email.

**Via GitHub issue:** Anyone with a GitHub account can [open an issue](https://github.com/lkaneda/pitchmap-pnw/issues/new) using the listing request template. The maintainer reviews and adds it.

---

## Weekly update process (with Claude)

The maintainer uses a Claude Project called **PitchMap PNW Monthly Sweep** to make updates fast. Here's the workflow:

1. Open the Claude project
2. Type: `Run the monthly sweep`
3. Claude searches each org's website and the aggregator calendars for pitch competition activity
4. Claude returns a summary: what changed, what looks active, what to update
5. Maintainer makes the edits to `data.json` and commits

Estimated time: **20–30 minutes once a month.**

---

## Hosting setup (one-time, already done)

- **GitHub:** Source files live at `github.com/lkaneda/pitchmap-pnw`
- **Netlify:** Connected to the GitHub repo, auto-deploys on every commit. Free tier.
- **Domain:** `pitchmappnw.com` — configured in Netlify DNS settings. Costs ~$12/year.
- **Forms:** The "Suggest a Listing" form is handled by Netlify Forms (free tier, up to 100 submissions/month).

---

## File structure

```
pitchmappnw/
├── index.html       ← The website (don't edit unless you know HTML)
├── data.json        ← THE FILE YOU EDIT for all updates
└── README.md        ← This guide
```

---

## Credits

- Seed data contributed by **Matthew Spellman**
- Built for the PNW startup ecosystem
- Community partner: **RAIN Catalysts**
