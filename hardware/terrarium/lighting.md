# Terrarium Lighting Setup

Complete lighting system for realistic day/night cycles and seasonal simulation.

---

## Lighting Philosophy

TerrariumOS uses a **4-phase lighting system** to simulate natural tropical conditions:

1. **Dawn** (4500K) – Warm morning light
2. **Day** (6700K) – Full spectrum daylight
3. **Basking** (2250K) – Short heat pulse
4. **Moon** (cool white 1W) – Night orientation

No lamp runs 24/7. All phases are time-controlled and season-dependent.

---

## Required Lamps

| Lamp Type | Color Temp | Power | Purpose | Daily Runtime | Price (approx.) |
|-----------|------------|-------|---------|---------------|-----------------|
| LED Strip 4500K | 4500K | 12-24W | Dawn & Dusk | 1-1.5h | 20€ |
| T5/T8 Fluorescent | 6700K | 18-24W | Daylight / Plant Growth | 8-10h | 25€ |
| Basking Spot | 2250K | 50W | Morning Heat Pulse | 2-3h | 15€ |
| Moonlight LED | Cool White | 1W | Night Orientation | 2-5h | 8€ |

**Total Lighting Cost:** ~68€

---

## Detailed Specifications

### 1. Dawn/Dusk LED (4500K)

- **Type:** LED Strip or LED Bulb
- **Color Temperature:** 4500K (warm white)
- **Power:** 12-24W
- **Purpose:** Soft morning and evening transitions
- **Control:** Dimmable recommended (PWM via GPIO or smart plug)
- **Mounting:** Top or side panel

**Product Examples:**
- Philips Hue White Ambiance (if budget allows)
- Generic 4500K LED strip (12V, controllable via MOSFET)

---

### 2. Daylight Tube (6700K)

- **Type:** T5 or T8 Fluorescent Tube
- **Color Temperature:** 6700K (daylight)
- **Power:** 18-24W
- **Purpose:** Full-spectrum daylight, supports plant growth
- **Control:** ON/OFF via Shelly or relay
- **Mounting:** Top panel, centered

**Product Examples:**
- Osram Lumilux T5 HO 24W 6700K
- JBL Solar Tropic (terrarium-specific, full spectrum)

---

### 3. Basking Spot (2250K)

- **Type:** Incandescent / Halogen Spot
- **Color Temperature:** 2250K (warm orange)
- **Power:** 50W
- **Purpose:** Short heat pulse in the morning (2-3 hours)
- **Control:** ON/OFF via Shelly or relay
- **Mounting:** Top panel, focused on basking area

**Important:**
- NOT a heat lamp for continuous use
- Provides localized warmth for morning activity
- Automatically reduces duration in winter

**Product Examples:**
- Exo Terra Sun Glo Basking Spot 50W
- Generic halogen spot lamp (E27 socket)

---

### 4. Moonlight (1W LED)

- **Type:** Low-power LED
- **Color Temperature:** Cool white or blue-tinted
- **Power:** 1W
- **Purpose:** Night orientation without disturbing sleep
- **Control:** ON/OFF via GPIO relay
- **Mounting:** Side or back panel

**Schedule:**
- Daily: 2 hours after dusk
- Full moon: 3 consecutive nights until 01:00

**Product Examples:**
- Exo Terra Night Glo Moonlight LED
- Generic 1W LED (blue or cool white)

---

## Seasonal Light Schedule (Example)

### Summer
- Dawn: 08:30 → 09:00 (30 min)
- Daylight: 09:00 → 20:30 (11.5h)
- Basking: 10:00 → 13:00 (3h)
- Dusk: 20:30 → 21:00 (30 min)
- Moonlight: 23:00 → 01:00 (2h)

### Winter
- Dawn: 08:30 → 09:15 (45 min)
- Daylight: 09:15 → 19:15 (10h)
- Basking: 10:00 → 12:00 (2h)
- Dusk: 19:15 → 20:00 (45 min)
- Moonlight: 22:00 → 00:00 (2h)

**Transitions:** ±15 minutes per week

---

## Electrical Setup

### Power Requirements

Total max power consumption:
- 4500K LED: 24W
- 6700K Tube: 24W
- Basking Spot: 50W
- Moonlight: 1W

**Total:** ~100W peak (when all lamps are on, which never happens)

Typical usage: 30-50W during daylight hours.

### Switching

**Option A: Shelly Smart Plugs** (recommended)
- 4x Shelly Plug S (one per lamp type)
- WiFi-controlled via local HTTP API
- Easy setup, no soldering

**Option B: GPIO Relays**
- 4-channel relay module
- Direct GPIO control
- Requires optocoupler for 230V safety

---

## Safety Notes

- Never connect 230V directly to Raspberry Pi GPIO pins
- Use certified relays or smart plugs for switching
- Ensure proper ventilation around heat-producing lamps
- Mount lamps securely to prevent falling into terrarium
- Use waterproof sockets in high-humidity environments

---

## References

- [Exo Terra Lighting Guide](https://www.exo-terra.com/en/support/reptile-lighting/)
- Color temperature and reptile vision: Research pending
