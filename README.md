# sbb-timetable

An [OpenClaw](https://openclaw.com) skill for Swiss public transport timetable lookups.

Uses the free [transport.opendata.ch](https://transport.opendata.ch) API — no API key required. The agent calls endpoints via `web_fetch` with selective `fields[]` filtering to keep token costs low.

## Capabilities

- **Connections** — "How do I get from Bern to Zürich?" (multi-leg journeys, platforms, delays)
- **Stationboard** — "What's leaving from Basel SBB?" (departures/arrivals at a station)
- **Station search** — Disambiguates station names when needed

## Install

Clone into your OpenClaw skills directory:

```bash
git clone https://github.com/cjmlarson/sbb-timetable.git ~/.openclaw/skills/sbb-timetable
```

The skill requires `web_fetch` to be enabled (it is by default).

## License

Public domain.
