# drive-fly — Travel Mode Analysis Dashboard

Repository: https://tinyurl.com/drive-fly

Interactive dashboard for exploring cost, emissions, and time trade-offs across travel modes.

## What it covers

- Driving EV vs driving Hybrid vs driving SUV vs flying
- Occupancy effects (for example SUV with 2 occupants)
- Flight seat class impact (economy, premium economy, business)
- Door-to-door deadhead time and airport process time
- Value-of-time conversion into generalized travel cost
- Break-even distances for Cost, Carbon, and Time across modes

## How to run

1. Open `index.html` in your browser.
2. Adjust controls to model your scenario.
3. Review result cards and break-even insights.

### Live trip estimates (optional server)

Drive-fly includes an optional small Node.js proxy that can provide date-sensitive trip estimates (uses Nominatim geocoding + mocked pricing by default). When you run the server it will also serve the static site and provide `/api/estimate` for the frontend.

Quick start:

PowerShell:

```powershell
cd "c:\Users\089741\OneDrive - City of Phoenix\dev\drive-fly"
npm install
$env:TRIP_API_PROVIDER = ""  # leave empty to use mocked estimates, or set to a provider name
$env:TRIP_API_KEY = "YOUR_API_KEY"  # provider-specific
npm start
```

Open http://localhost:3000 in your browser and use the new "From/To" controls and "Get Live Estimate" button.

Notes:
- If you supply `TRIP_API_PROVIDER` and API credentials, extend `server.js` to call the provider-specific endpoints (Amadeus, Skyscanner/RapidAPI, etc.). The current server will use OpenStreetMap Nominatim to geocode city names and return plausible flight/drive estimates when no provider is configured.
- Be mindful of Nominatim rate limits; for production use get a geocoding API key and cache results.

## Model notes

- Driving costs and emissions are allocated per traveler using occupancy.
- Flight fare and flight emissions scale with seat type multipliers.
- Generalized cost is calculated as:

  `generalized_cost = monetary_cost + value_of_time * travel_hours`

- Break-even distances are solved as linear intersections between two mode equations.

## Good experiments

- EV solo vs flight economy at 300 to 1,200 miles
- Hybrid solo vs flight economy for medium-haul trips
- SUV with 2 vs flight economy under high gas prices
- Business class flight vs EV with high value-of-time
- Cleaner vs dirtier electric grid scenarios

## Next characteristics to explore

- Reliability risk (delay probability and expected delay cost)
- Comfort score (seat quality, noise, personal space)
- Luggage constraints (fees, oversize handling, packing friction)
- First/last-mile burden (transfer count, parking search, curb wait)
- Energy refuel risk (charger/fuel station queues and detours)
- Risk-adjusted outcomes (average day vs worst-case travel day)
