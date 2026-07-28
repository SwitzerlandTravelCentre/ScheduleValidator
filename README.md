# FIT Package Validator

Standalone browser tool for validating FIT package travel start dates.

The validator helps plan multi-day package trips with several locations. It checks
which start dates are possible and which are blocked because an overnight stay at
a location overlaps with a blocked event date.

## Features

- Configure a package name and validation start date.
- Add any number of locations in travel order.
- Set nights per location; travel days are calculated automatically.
- Add multiple blocked date ranges per location.
- Add buffer days before and after blocked date ranges.
- View results as blocked start dates, calendar, and 60-day matrix.
- Mark actual event days in the calendar, for example `Trucker Festival`.
- Store data locally in the browser with `localStorage`.
- Export and import trip data as JSON.
- Works offline as a single HTML file.

## Quick Start

Open [index.html](./index.html) in a modern browser.

No installation, build step, server, or internet connection is required.

## Import Format

Use the import/export panel in the app to paste JSON data. IDs are optional; the
app creates missing IDs automatically during import.

```json
{
  "packageName": "Alpine Holiday",
  "analysisStart": "2027-05-01",
  "selectedMonth": "2027-06",
  "stops": [
    {
      "location": "Luzern",
      "nights": 3,
      "blocks": []
    },
    {
      "location": "Interlaken",
      "nights": 3,
      "blocks": [
        {
          "from": "2027-06-26",
          "to": "2027-06-28",
          "description": "Trucker Festival",
          "buffer": 0
        }
      ]
    }
  ]
}
```

## Date Logic

Dates are parsed as local calendar dates. The app intentionally avoids UTC date
conversion so that blocked dates stay on the exact day entered by the user.

A start date is blocked when at least one overnight date of the trip overlaps
with a location's effective blocked date range. The effective range is:

```text
blocked from - buffer days  through  blocked to + buffer days
```

## Development

This project is intentionally dependency-free. The product code lives in
[index.html](./index.html).

To check the inline JavaScript syntax locally:

```powershell
node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const m=html.match(/<script>([\s\S]*)<\/script>/); if(!m) throw new Error('No script block found'); new Function(m[1]); console.log('script syntax ok');"
```

## Repository Notes

The repository does not define a public license yet. Treat the contents as
internal unless Switzerland Travel Centre adds a license file.
