# SMARTCLEAN AI

**Global Innovation Hackathon 2026 — Build for a Better Future**

An interactive, browser-based prototype of an AI-powered predictive waste-collection platform. It combines a 3D city visualization with a full operations dashboard: wet/dry waste monitoring, weight sensing, AI-driven predictions, route optimization, and complete bin CRUD management.

> **SMARTCLEAN AI doesn't just tell you how full a bin is. It predicts which waste compartment needs collection first.**

---

## Run it

No build step, no server, no dependencies to install.

1. Unzip the project.
2. Open `index.html` in a modern desktop or mobile browser.

Three.js is bundled locally as `three.min.js`, so it also works fully offline.

## Deploy it

This is a static site (`index.html` + `three.min.js`), so it deploys as-is to GitHub Pages, Vercel, Netlify, or any static host — no build command needed. A minimal `vercel.json` is included for a clean Vercel deployment.

---

## What it does

### 🏠 Dashboard
A 3D city with six simulated smart bins, each split into wet and dry compartments. Live KPIs: bins monitored, average wet/dry fill, critical compartments, total waste weight, predicted collections, and sensors online — all calculated from the current bin records, never hard-coded.

### 🗑️ Bin Management (full CRUD)
- **Create** — "+ Add new bin" opens a form for ID, name, location (address or lat/lng), ward, install date, status, wet/dry capacity and current readings, and sensor configuration (ultrasonic, weight sensor, ESP32 device ID).
- **Read** — a searchable, filterable table (by ID/name/location/ward, status, risk, waste type) with a detailed bin profile view.
- **Update** — edit any field; changes propagate immediately to the dashboard, priority queue, predictions, and route optimizer.
- **Delete** — requires confirmation, then removes the bin everywhere.
- Validation: no duplicate bin IDs, required fields, latitude −90 to 90, longitude −180 to 180, fill 0–100%, non-negative weights, and a warning (not a block) if weight exceeds configured capacity.
- Data persists in the browser (`localStorage`) across refreshes, structured so it can be swapped for a real backend (Postgres/Firebase/MongoDB/API) later.

### 🧠 AI Predictions
For each compartment: current fill (ultrasonic), weight (load cell), weight utilization, growth rate, 2-hour predicted fill, overflow risk, and a collection priority score — plus a plain-language explanation of why.

**Priority = 0.35 × fill % + 0.35 × weight % + 0.30 × predicted fill %**, flagged when fill or weight ≥ 85% or predicted fill ≥ 90%. Weight alone is never treated as exact fill level (waste density varies), so ultrasonic fill, weight, and growth rate are always blended.

### 🗺️ Routes
The optimizer ranks stops by **bin + waste type** (e.g. "SC-072 — DRY — Priority 87"), visits critical compartments first, then takes the shortest path between stops. Only compartments that actually need collection are included by default; an "include all bins" toggle is available. A 3D truck animates the route and collects bins as it passes.

### 📡 IoT Monitoring
Per-bin device status: ESP32 ID, ultrasonic sensor state, load-cell state, and data mode. If a bin's sensors are offline, the UI shows **"Sensor data unavailable"** rather than faking live readings.

### Guided demo
A one-click, narrated walkthrough of Sense → Predict → Prioritize → Act, including a simulated event surge and a route-efficiency estimate (vs. a fixed round visiting every bin, with fuel/CO₂ savings and stated assumptions).

---

## Prototype hardware (proposed, not connected)

Per compartment: **ultrasonic sensor** (e.g. HC-SR04) for fill level, **load cell + HX711 amplifier** for weight, read by an **ESP32** per bin.
