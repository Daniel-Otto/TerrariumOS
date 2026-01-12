# TerrariumOS Roadmap

## Phase 1 – Core System (MVP)

- Load seasonal schedule from CSV
- Relative time calculation based on configurable start time
- Light control (dawn, daylight, spot, moon)
- Manual CLI testing mode
- Safe GPIO / Shelly abstraction

## Phase 2 – Climate Control

- Temperature & humidity sensor integration
- Humidity target ranges (day/night)
- Rain system logic (time window + threshold)
- Logging of sensor data

## Phase 3 – Web Dashboard

- Flask-based local web UI
- Live sensor stats
- Manual override switches
- Status display (current phase, season, moon)

## Phase 4 – Camera Integration

- Raspberry Pi camera support
- Local MJPEG stream
- Dashboard camera embed

## Phase 5 – Remote Access

- VPN (WireGuard) integration guide
- Secure remote dashboard access
- Optional public snapshot view

## Phase 6 – Educational & Family Features

- Visual day/night indicators
- Simple UI mode for children
- Explanatory texts ("What is the jungle doing now?")
