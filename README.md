# HydroLogix — Hydration Benchmark Dashboard

HydroLogix is an interactive hydration benchmarking app focused on hot, dry Southwest conditions.

## What it does

- Compares **User Intake** vs **Peer Benchmark** and an **Electrolyte Scenario**
- Calculates baseline hydration from weight and age
- Applies environmental multipliers for:
  - temperature
  - humidity
  - dew point
  - altitude
  - activity level
- Applies a metabolic-window multiplier for hours since last intake
- Triggers a **High Demand** state when heat index crosses threshold
- Renders comparison cards, normalized bars, and actionable insights

## Core logic

- `calculateEvaporativeDemand(...)` isolates environmental burden logic
- `calculateHydrationBenchmark(...)` computes top-level benchmark demand
- `render()` orchestrates card/chart/insight updates

## Data model guidance

Use hydration intake records shaped like:

- `timestamp` (ISO-8601 string)
- `volume_ml` (number)
- `fluid_type_coefficient` (number)

## Run locally

1. Install dependencies: `npm install`
2. Start server: `npm start`
3. Open: `http://localhost:3000`

## Test

- `npm test`

## Notes

This tool provides scenario guidance and is not medical advice.
