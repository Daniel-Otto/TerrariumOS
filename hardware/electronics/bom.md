# Electronics Bill of Materials (BOM)

Complete list of electronic components needed for TerrariumOS.

---

## Controller

| Part | Description | Quantity | Price (approx.) | Notes |
|------|-------------|----------|-----------------|-------|
| Raspberry Pi 4 (4GB) | Main controller | 1 | 60€ | Pi 3B+ also works |
| microSD Card (32GB) | OS storage | 1 | 10€ | Class 10 or better |
| Power Supply (5V/3A) | Raspberry Pi power | 1 | 10€ | Official recommended |

---

## Sensors

| Part | Description | Quantity | Price (approx.) | Notes |
|------|-------------|----------|-----------------|-------|
| BME280 | Temp/Humidity/Pressure sensor (I²C) | 1-2 | 5€ each | Alternative: SHT31 |
| SHT31 | Temp/Humidity sensor (I²C) | 1-2 | 8€ each | Alternative to BME280 |

**Note:** Use 2 sensors for different terrarium zones (bottom + top).

---

## Actuators & Switching

| Part | Description | Quantity | Price (approx.) | Notes |
|------|-------------|----------|-----------------|-------|
| Shelly Plug S | Smart plug (WiFi) | 4 | 15€ each | For lights & basking spot |
| Shelly Plus 1 | Relay module (WiFi) | 1-2 | 12€ each | Alternative: GPIO relay |
| 4-Channel Relay Module | GPIO-controlled relays | 1 | 8€ | Optional, if not using Shelly |
| Optocoupler Module | Signal isolation | 1 | 5€ | Safety for 230V switching |

**Recommendation:** Use Shelly for easier setup. GPIO relays for advanced users.

---

## Wiring & Connections

| Part | Description | Quantity | Price (approx.) | Notes |
|------|-------------|----------|-----------------|-------|
| Jumper Wires (F-F) | Sensor connections | 10 | 5€ | I²C + power |
| Breadboard | Testing & prototyping | 1 | 5€ | Optional |
| Dupont Connectors | Custom cable length | Set | 8€ | Optional |

---

## Optional Components

| Part | Description | Quantity | Price (approx.) | Notes |
|------|-------------|----------|-----------------|-------|
| Raspberry Pi Camera v3 | Monitoring & timelapse | 1 | 35€ | Wide angle recommended |
| Camera Cable (extension) | Longer camera reach | 1 | 10€ | If needed |
| Case for Raspberry Pi | Protection | 1 | 15€ | With ventilation |

---

## Total Cost Estimate

- **Minimum Setup** (Raspi + 1 sensor + Shelly plugs): **~150€**
- **Standard Setup** (Raspi + 2 sensors + Shelly + case): **~200€**
- **Full Setup** (+ Camera + optocouplers): **~250€**

---

## Where to Buy

- **Germany:** reichelt.de, Conrad, Amazon
- **International:** AliExpress (cheaper, longer shipping), Adafruit, SparkFun
- **Shelly Devices:** shelly.com, Amazon

---

## Notes

- Prices are approximate and may vary by region and vendor
- Check I²C addresses before ordering multiple sensors of the same type
- Always use proper isolation when working with 230V AC power
