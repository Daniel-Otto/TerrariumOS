## TerrariumOS 🦎🌿

![Python](https://img.shields.io/badge/python-3.10+-blue)
![Platform](https://img.shields.io/badge/platform-raspberry%20pi-green)
![License](https://img.shields.io/badge/license-MIT-green)

**TerrariumOS** is an open-source Raspberry Pi–based control system for realistic terrarium environments.

It simulates natural day/night cycles, seasonal changes, humidity dynamics, and lunar phases.

*The jungle lives – but controlled.*

---

## Overview

TerrariumOS is designed for tropical terrariums (e.g. *S. elegans*) and focuses on
biologically plausible environmental simulation rather than simple on/off timers.

The system emphasizes smooth transitions, seasonal perception, and stress-free
conditions for animals and plants alike.

---

## Goals

- Smooth light and temperature transitions
- Seasonal changes without hard switches
- Humidity management based on target ranges
- Modular and extensible (web dashboard, camera, VPN)
- Family- and child-friendly operation

---

## Core Concept

The Raspberry Pi acts as a central **biological clock**.

All events are calculated **relative to a configurable day start time**
(e.g. `08:30` instead of fixed absolute times).

This allows the terrarium schedule to adapt to real family life
(e.g. later mornings when children sleep longer).

---

## Hardware (Recommended)

### Controller

- Raspberry Pi 3B+ or Raspberry Pi 4
- Raspberry Pi OS Lite

### Sensors

- Temperature / humidity: BME280 or SHT31 (I²C)
- Optional second sensor for upper terrarium zones

### Actuators

- Lighting & heat: Shelly Plug / Shelly Plus 1 or relay module (optocoupled)
- Rain system: Exo Terra Monsoon (230 V, ON/OFF)

### Camera (Optional)

- Raspberry Pi Camera Module 3 (Wide recommended)

---

## Lighting Concept

### Lamps

- 4500K LED: dawn & dusk lighting
- 6700K fluorescent tube: main daylight / plant light
- 2250K basking spot: short heat pulse (morning)
- 1W moonlight: night orientation

### Daily Logic (Summer Example)

- Dawn/dusk: 30–45 minutes
- Basking spot: 2–3 hours in the late morning
- No continuous heat spot throughout the day

---

## Seasonal Model

- Summer: 12.0 h light
- Winter: 10.0 h light
- Transitions: ±15 minutes per week
- Basking duration reduced accordingly

No true hibernation – only a controlled activity reduction.

---

## Moonlight

- Daily: 2 hours after dusk
- Full moon: 3 consecutive nights per month until 01:00
- No permanent night lighting

---

## Humidity Control

Target ranges:

- Day: 55–70 %
- Night: 70–85 %

The rain system is **not controlled by fixed timers**, but by:

- Morning / evening time windows
- Activation only when humidity drops below target range

---

## Software Architecture (Python)

```text
terrarium/
├── config/
│   ├── base.yaml        # Day start time, overrides
│   ├── months.yaml     # Seasonal parameters
│   └── hardware.yaml   # GPIO / Shelly mapping
│
├── core/
│   ├── scheduler.py
│   ├── seasons.py
│   ├── lights.py
│   ├── climate.py
│   └── moon.py
│
├── sensors/
│   └── bme280.py
│
├── actuators/
│   ├── relay.py
│   └── shelly.py
│
└── main.py
```

---

## Project Status

TerrariumOS is currently in early development.

See [`docs/roadmap.md`](docs/roadmap.md) for planned features and milestones.

---

## Safety Notes

- Never connect 230 V directly to the Raspberry Pi
- Use certified relays or smart plugs
- Do not expose the system directly to the internet
- Use VPN (e.g. WireGuard) for remote access

---

## License

MIT License