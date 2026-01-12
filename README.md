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

## Features

### Lighting System

- **4-phase lighting:** Dawn (4500K), Day (6700K), Basking (2250K), Moon (1W)
- **Seasonal adaptation:** 10-12h light cycles with smooth transitions
- **Smart scheduling:** All events relative to configurable day start time

### Climate Control

- **Humidity-based rain system:** Activates only when needed (not on fixed timers)
- **Temperature monitoring:** BME280/SHT31 sensors
- **Target ranges:** Day 55-70%, Night 70-85%

### Moonlight Simulation

- Daily: 2 hours after dusk
- Full moon: 3 consecutive nights per month until 01:00

---

## Project Structure

```text
TerrariumOS/
├── docs/
│   └── roadmap.md              # Development roadmap
│
├── hardware/                   # Hardware documentation
│   ├── README.md               # Hardware overview
│   ├── electronics/            # Controller, sensors, actuators
│   │   ├── bom.md              # Bill of materials (~150-250€)
│   │   ├── setup.md            # Setup guide
│   │   └── schematics/         # Wiring diagrams
│   └── terrarium/              # Terrarium equipment
│       ├── lighting.md         # Lighting specs (~68€)
│       ├── equipment.md        # Rain system, enclosure (~210-400€)
│       └── plants.md           # Suitable species
│
└── software/                   # Python software
    ├── README.md               # Software documentation
    └── terrarium_os/           # Main Python package
        ├── config/             # Configuration files
        ├── core/               # Scheduler, lights, climate
        ├── sensors/            # Sensor interfaces
        └── actuators/          # Relay & Shelly control
```

---

## Quick Start

### Hardware

See [hardware/README.md](hardware/README.md) for:

- Complete parts list (BOM)
- Setup instructions (Raspberry Pi, sensors, actuators)
- Wiring diagrams
- Safety guidelines

**Estimated cost:** ~360-650€ (electronics + terrarium equipment)

### Software

See [software/README.md](software/README.md) for:

- Installation instructions
- Configuration guide
- Usage examples
- Development setup

---

## Project Status

🚧 **Early Development** – Phase 1 (MVP) in progress

See [docs/roadmap.md](docs/roadmap.md) for planned features and milestones.

**Current Phase:** Core System (MVP)

- Relative time-based scheduler
- Seasonal light cycles
- Lighting control abstraction
- CLI testing mode

---

## Safety Notes

- Never connect 230 V directly to the Raspberry Pi
- Use certified relays or smart plugs
- Do not expose the system directly to the internet
- Use VPN (e.g. WireGuard) for remote access

---

## License

MIT License