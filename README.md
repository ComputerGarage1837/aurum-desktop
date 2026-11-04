# Aurum Desktop - updates

This repository is the **update feed** for Aurum Desktop (a big-button desktop for seniors, provided by Computer Garage).
Every installed copy checks the `update/` folder on the `main` branch a few times a day.

| File | What it does |
|---|---|
| `update/shop.json` | Store details shown on the **Need Help?** screen: phone, website, email, address, store hours, **holiday hours**. Edit this file and every PC shows the change within hours. No new program needed. |
| `update/manifest.json` | Says which program version is newest (`Version`), what is new (`Notes`) and the SHA-256 checksum of the program file. |
| `update/AurumDesktop.exe` | The newest program. Copies download it, check the checksum, and install it when nobody is using the computer (or at the next start). |

Everything here is public on purpose, so customer PCs can read it without a password. **Never put secrets in this repository.**
Keep two-factor authentication on the GitHub account: whoever can push here can change the program on every PC.

## Change the store hours or add holiday hours
Edit `update/shop.json` (the pencil icon on GitHub) and commit. Examples for `HolidayHours` (empty list = nothing shown):

```json
"HolidayHours": [
  { "Name": "Christmas Day",  "Date": "2026-12-25", "Time": "Closed" },
  { "Name": "Christmas break", "From": "2026-12-24", "To": "2026-12-26", "Time": "Closed" },
  { "Name": "New Year's Eve", "Date": "2026-12-31", "Time": "10:00 AM - 2:00 PM", "ShowFrom": "2026-12-15" }
]
```
- `Date` for one day, or `From` + `To` for a range (`yyyy-MM-dd`). `Time` is hours or `Closed`.
- `ShowFrom` (optional) keeps it hidden until that date. Entries hide themselves after their last day.
- On the day itself the "Open now / Closed" badge follows the holiday hours.

## Release a new program version
On the computer with the source code: `.\Make-Release.ps1 -Version 1.2.0 -Notes "What changed"` then `.\Publish-Update.ps1`.
