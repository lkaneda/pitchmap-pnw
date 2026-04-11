# Weekly Update

Perform a weekly maintenance update on `data.json` for the PitchMap PNW directory.

**Arguments (optional):**
- `--update-only` — only check existing listings for updates, skip adding new entries
- `--add-only` — only add new entries provided below, skip checking existing listings
- `#<number>` — one or more GitHub issue numbers (e.g. `#42 #55`) referencing `listing-request` or `listing-update` issues to process
- `<url>` — one or more URLs (e.g. `https://example.com/pitch`) to WebFetch and build a new entry from
- Default (no args): do both — check existing listings AND add new entries

**Arguments received:** $ARGUMENTS

---

## Instructions

Parse the arguments from `$ARGUMENTS`:
- If `--update-only` is present, set mode to update-only.
- If `--add-only` is present, set mode to add-only.
- Otherwise set mode to both.
- Extract any GitHub issue numbers (patterns like `#42`, `42`, `issue/42`).
- Extract any URLs (strings starting with `http://` or `https://`).

Any content in `$ARGUMENTS` that is not a flag, issue number, or URL is treated as raw new competition data (JSON or descriptive text) to add directly.

Read `data.json` in full before making any changes.

---

### Step 1 — Clear all internal tags (always run this first)

In `data.json`, find every competition object that has an `"internalTags"` field. Remove the entire `"internalTags"` field from each competition. This clears the "new" and "updated" badges set during previous weeks.

---

### Step 2 — Check existing listings for updates (skip if `--add-only`)

For each competition in `data.json`:

1. Fetch the competition's `url` using WebFetch.
2. Compare what you find on the page against the current entry's `events`, `notes`, `status`, `description`, and `eventUrl` fields.
3. If anything has materially changed (new application window opened, status changed, date announced, new event added, event cancelled, etc.):
   - Update the relevant fields in `data.json`.
   - If an event's `status` is being set to `monitor` or `inactive`, also set that event's `eventUrl` to `null`.
   - Add `"internalTags": ["updated"]` to that competition object (at the same level as `"tags"`, not inside events).
   - Record what changed for the summary.
4. If nothing material has changed, leave the entry as-is. Do not add internalTags.

Work through all competitions. Fetch their URLs in parallel where possible to save time.

---

### Step 3 — Add new entries (skip if `--update-only`)

**If GitHub issue numbers were provided in `$ARGUMENTS`:**

For each issue number, fetch it via the GitHub API using WebFetch:
```
https://api.github.com/repos/lkaneda/pitchmap-pnw/issues/<number>
```
Read the issue body to extract the organization name, website URL, type, prize type, and any notes. Check the `labels` array to determine how to handle it:

- Label `listing-request` → add as a new competition entry.
- Label `listing-update` → apply the described update to the matching existing entry instead (and tag it `"updated"`).

WebFetch the URL from the issue body to fill in full event details before writing the entry.

After all changes are written, note in the summary which issues were processed and remind the user to close them manually on GitHub, since issue management requires browser access.

**If URLs were provided in `$ARGUMENTS`:**

For each URL, WebFetch the page and extract everything available: organization name, event name, description, dates, application status, prize type, geography served, and any event-specific URL. Use that to construct a full competition entry. If the page doesn't have enough information to fill a field confidently, use a reasonable default or leave it as `null`.

**If raw competition data was provided (not an issue number or URL):**

Parse the text/JSON directly and construct the entry from it.

**For all new entries:**

1. New entries must follow the existing schema: `id`, `org`, `url`, `serviceArea`, `location`, `tags`, `events[]`.
2. Derive `id` from the org name (lowercase, hyphenated, no special characters).
3. Use WebFetch on the competition URL to fill in description, status, and event details accurately.
4. Add `"internalTags": ["new"]` to each new competition object (at the same level as `"tags"`).
5. Place new competitions at a sensible position in the array (generally at the end, or grouped with similar orgs).
6. Record the org name of each addition for the summary.

If no new entry data was provided at all, note "No new entries provided" in the summary.

---

### Step 4 — Update meta.lastUpdated

Set `meta.lastUpdated` in `data.json` to today's date in `YYYY-MM-DD` format.

---

### Step 5 — Print a summary

After all changes are written, print a summary to the console in this format:

```
=== Weekly Update Summary (YYYY-MM-DD) ===

CLEARED INTERNAL TAGS: <count> competitions had tags removed

UPDATED LISTINGS (<count>):
  - <org name>: <brief description of what changed>
  - <org name>: <brief description of what changed>
  (or "None" if no updates were found)

NEW ENTRIES ADDED (<count>):
  - <org name>
  (or "None" if no new entries were added / skipped due to --update-only)

NO CHANGES DETECTED:
  <count> listings checked, no material changes found.

Mode: <both | update-only | add-only>
```

If there were zero total changes (no updates found and no new entries), make that explicit:
"No changes were made to data.json this week."
