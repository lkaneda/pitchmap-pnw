# PitchMap PNW

**A community-maintained directory of startup pitch competitions across Oregon and Washington.**

🌐 **[pitchmappnw.com](https://pitchmappnw.com)**

---

PitchMap PNW helps entrepreneurs in the Pacific Northwest find pitch competitions, track which ones are actively accepting applications, and discover the organizations that host them. It's searchable by location, filterable by status, and includes a map so you can find opportunities near you.

The directory is updated weekly and covers the Portland metro area, the Columbia River Gorge, and the broader Oregon and Washington startup ecosystem.

---

## What's in the directory

Each listing includes:

- **Host organization** and the events they run
- **Status** — whether applications are open, an event is scheduled, or it's worth monitoring
- **Service area** — Portland Metro, Oregon statewide, Seattle Metro, Washington, PNW-wide, or the Columbia River Gorge
- **Award type** — Cash/Grant, Investment, or Loan
- **Notes** — deadlines, event dates, and other timely details
- **Links** — to the organization's website and event/application page when available

---

## How to suggest a listing

Know of a pitch competition, host organization, or community group that should be on this list? There are two ways to suggest it:

### Option 1 — Google Form (easiest)
Fill out the [Suggest a Listing form](https://forms.gle/DGBsjABtrnDjWZv97). No GitHub account needed.

### Option 2 — GitHub Issue (preferred)
[Open an issue](https://github.com/lkaneda/pitchmap-pnw/issues/new?template=suggest-a-listing.md) using the **Suggest a Listing** template. This keeps everything in one place and lets the community see what's been requested.

All submissions are reviewed before being added. The maintainer typically processes new suggestions within a week.

---

## How the data works

Everything in the directory lives in a single file: [`data.json`](data.json). Each host organization has an entry that looks like this:

```json
{
  "id": "example-org",
  "org": "Example Organization",
  "url": "https://example.org",
  "serviceArea": "portland-metro",
  "location": { "lat": 45.5231, "lng": -122.6765, "city": "Portland, OR" },
  "tags": ["general", "early-stage"],
  "events": [
    {
      "name": "Example Pitch Night",
      "status": "accepting",
      "description": "A brief description of the event.",
      "url": "https://example.org/pitch",
      "eventUrl": "https://example.org/apply",
      "notes": "Applications open through May 1. Event on May 20.",
      "prizeType": "cash",
      "serves": "Greater Portland Metro Area",
      "counties": ["Multnomah County", "Washington County"]
    }
  ]
}
```

### Status values

| Status | Meaning |
|---|---|
| `"accepting"` | 🟢 Actively accepting applications right now |
| `"scheduled"` | 🟡 Event announced, applications closed or opening soon |
| `"monitor"` | 🔵 No active event — worth checking back periodically |
| `"inactive"` | ⚫ Has hosted before but currently appears inactive |

### Service area values

| Value | Meaning |
|---|---|
| `"portland-metro"` | Greater Portland area (~50 mile radius) |
| `"seattle-metro"` | Greater Seattle area (~50 mile radius) |
| `"gorge"` | Columbia River Gorge region (~60 mile radius from The Dalles) |
| `"oregon"` | Oregon state |
| `"washington"` | Washington state |
| `"pnw"` | Oregon + Washington |

### Prize type values

| Value | Meaning |
|---|---|
| `"cash"` | Cash prize or grant |
| `"investment"` | Equity or SAFE investment |
| `"both"` | Cash prize plus investment |
| `"loan"` | Loan financing opportunity |


---

## Project structure

```
pitchmappnw/
├── index.html    ← The website (HTML, CSS, and JS in one file)
├── data.json     ← All directory data — the only file updated regularly
└── README.md     ← This file
```

The site is a single static HTML file with no build step, no framework, and no backend. It loads `data.json` at runtime. Hosting is free via [GitHub Pages](https://pages.github.com/).

---

## Maintained by

[Leila Kaneda](https://github.com/lkaneda), with seed data contributed by **Matthew Spellman**.

Community partner: [RAIN Catalysts](https://raincatalysts.org)

Licensed under [CC0 1.0 Universal](LICENSE) — public domain, no restrictions.
