# TerrariumOS Hardware

Complete hardware documentation for building a TerrariumOS-controlled terrarium.

---

## Overview

TerrariumOS requires two main categories of hardware:

1. **Electronics** – Controller, sensors, actuators, wiring
2. **Terrarium Equipment** – Lighting, rain system, enclosure, plants

---

## Electronics

### Components

- **Controller:** Raspberry Pi 4 (4GB) or Pi 3B+
- **Sensors:** BME280 or SHT31 (I²C temperature/humidity)
- **Actuators:** Shelly smart plugs or GPIO relays
- **Wiring:** Jumper wires, optocouplers, breadboard

### Documentation

- **[Bill of Materials (BOM)](electronics/bom.md)** – Complete parts list with prices (~150-250€)
- **[Setup Guide](electronics/setup.md)** – Raspberry Pi setup, wiring, I²C configuration
- **[Schematics](electronics/schematics/)** – Wiring diagrams (to be added)

**Cost Estimate:** ~150-250€

---

## Terrarium Equipment

### Components

- **Lighting:** 4-phase system (dawn, day, basking, moon)
- **Climate Control:** Rain system (Exo Terra Monsoon)
- **Enclosure:** Glass terrarium with ventilation
- **Substrate & Plants:** Bioactive setup (optional)

### Documentation

- **[Lighting System](terrarium/lighting.md)** – 4-phase lighting setup, lamp specs (~68€)
- **[Equipment List](terrarium/equipment.md)** – Rain system, fogger, enclosure (~210-400€)
- **[Plants & Inhabitants](terrarium/plants.md)** – Suitable species and bioactive setup

**Cost Estimate:** ~210-400€

---

## Total Project Cost

- **Electronics:** ~150-250€
- **Terrarium Equipment:** ~210-400€
- **Total:** ~360-650€

Prices vary by region, vendor, and chosen components.

---

## Quick Links

- [Electronics BOM](electronics/bom.md) – Shopping list for controller and sensors
- [Setup Guide](electronics/setup.md) – Step-by-step Raspberry Pi setup
- [Lighting Guide](terrarium/lighting.md) – Lamp specifications and schedule
- [Equipment Guide](terrarium/equipment.md) – Rain system and climate control

---

## Safety Guidelines

### Electrical Safety

- **Never connect 230V AC directly to Raspberry Pi GPIO pins**
- Use certified relays or smart plugs for switching AC loads
- Use optocouplers for signal isolation
- Keep electronics away from water and spray zones
- Use GFCI outlets near water sources

### Fire Safety

- Ensure proper ventilation around heat-producing lamps
- Do not cover lamp ventilation holes
- Use ceramic lamp sockets for high-wattage bulbs
- Never exceed recommended lamp wattage

### Raspberry Pi Safety

- Use official power supply (5V/3A for Pi 4)
- Ensure adequate cooling (passive heatsinks or active fan)
- Do not expose Pi to direct sunlight or heat sources
- Keep Pi in a ventilated enclosure

---

## Support

For hardware-related questions, open an issue on GitHub with the `question` label.

Include:
- Hardware component (e.g., BME280, Shelly Plug)
- Wiring setup (photo if possible)
- Error messages or unexpected behavior
