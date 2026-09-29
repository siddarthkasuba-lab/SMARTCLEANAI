# SMARTCLEAN AI — 3D Edition

Global Innovation Hackathon 2026 — Build for a Better Future

Interactive 3D city view of the Sense → Predict → Act waste-collection prototype.

## Run
Open `index.html` in a modern browser (works offline; three.js is bundled as `three.min.js`).

## Use
- Drag to rotate, scroll or pinch to zoom, click a bin (or its tag) to inspect it.
- Bin level and colour show fill and priority; the ring marks the 2-hour forecast; the panel shows a forecast chart per bin.
- Read sensor, Predict, Plan route, and a Live feed (accelerated simulation). The truck runs the route and collects bins.

## Prototype disclosure
All bin readings and metrics are simulated demonstration data, not measured municipal results.

## Future scope
ESP32 + ultrasonic hardware, cloud telemetry, historical-data ML forecasting, GPS/map routing, fleet management.

## Highlights for judges
- **Guided demo** button: a 40-second narrated Sense, Predict, Act walkthrough.
- **Impact estimate** after each route: distance vs a fixed round that visits every bin, plus fuel and CO2 (assumptions stated on screen).
- **Event surge** scenario: a crowd event fills three bins and forecasts update instantly.

## Wet/dry compartments and weight sensing
- Every smart bin has a WET and a DRY compartment, each with an ultrasonic fill sensor and a load cell (ESP32 + HX711 in the proposed hardware).
- Per compartment: physical fill, weight, weight utilization, growth rate, 2-hour prediction, risk, priority and an AI explanation.
- Priority = 0.35 x fill + 0.35 x weight + 0.30 x predicted fill. Flagged when fill or weight >= 85%, or predicted >= 90%.
- Weight alone is not treated as fill level (waste density varies), so ultrasonic fill, weight and growth rate are combined.
- Route ranks bin + waste type (critical bins first, then shortest path). Live simulation, Simulate IoT, history chart and a Hardware architecture view are included.
- All sensor values are simulated in the browser. No hardware is connected.
