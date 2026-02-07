---
name: sbb-timetable
description: Swiss public transport timetable lookups via transport.opendata.ch
user-invocable: false
---

# Swiss Public Transport Timetable

Free API at `transport.opendata.ch` — no API key needed. Use `web_fetch` to call these endpoints.

## Connections — "How do I get from A to B?"

```
https://transport.opendata.ch/v1/connections?from=FROM&to=TO&fields[]=connections/duration&fields[]=connections/from/station/name&fields[]=connections/from/departure&fields[]=connections/from/platform&fields[]=connections/from/prognosis/departure&fields[]=connections/to/station/name&fields[]=connections/to/arrival&fields[]=connections/to/prognosis/arrival&fields[]=connections/sections/journey/category&fields[]=connections/sections/journey/number&fields[]=connections/sections/journey/to&fields[]=connections/sections/departure/station/name&fields[]=connections/sections/departure/departure&fields[]=connections/sections/departure/platform&fields[]=connections/sections/arrival/station/name&fields[]=connections/sections/arrival/arrival
```

Required params: `from`, `to` (station names — the API fuzzy-matches them).

Optional params:
- `limit` — number of connections (default 3, max ~6)
- `date` — YYYY-MM-DD
- `time` — HH:MM
- `isArrivalTime=1` — treat `time` as desired arrival instead of departure

Sections with `journey: null` mean a walking transfer between platforms/stations.

## Stationboard — "What's leaving from station X?"

```
https://transport.opendata.ch/v1/stationboard?station=STATION&limit=5&fields[]=stationboard/stop/departure&fields[]=stationboard/stop/delay&fields[]=stationboard/stop/platform&fields[]=stationboard/category&fields[]=stationboard/number&fields[]=stationboard/to
```

Required: `station` (name) or `id` (SBB station ID).

Optional:
- `limit` — default 5
- `type` — `departure` (default) or `arrival`

## Locations — station name disambiguation

Use when a name might be ambiguous (e.g. "Basel" → Basel SBB, Basel Badischer Bahnhof, etc.):

```
https://transport.opendata.ch/v1/locations?query=QUERY&fields[]=stations/name&fields[]=stations/id
```

## Formatting rules

- Show times as HH:MM, never raw ISO timestamps.
- If prognosis differs from scheduled time, mention the delay (e.g. "11:31 (+3 min)").
- Keep responses brief — short sentences, not tables. WhatsApp messages should be concise.
- For multi-leg journeys, summarize the chain: "IC 1 Bern dep 11:31 → Zurich arr 12:28, then S3 → Uster arr 12:52".
- Always mention the train category and number (e.g. IC 1, S3, IR 36).
