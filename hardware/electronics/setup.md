# Electronics Setup Guide

Step-by-step guide for setting up the TerrariumOS electronics (Raspberry Pi, sensors, actuators).

---

## Prerequisites

- Raspberry Pi 4 (4GB) or Raspberry Pi 3B+
- microSD card (32GB+) with Raspberry Pi OS Lite
- BME280 or SHT31 sensor(s)
- Shelly smart plugs OR GPIO relay module
- Jumper wires (for sensor connections)
- Power supply (5V/3A for Pi 4)

See [bom.md](bom.md) for complete parts list.

---

## 1. Prepare Raspberry Pi

### Install Raspberry Pi OS

1. Download [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
2. Flash **Raspberry Pi OS Lite (64-bit)** to microSD card
3. Enable SSH (for headless setup):
   - Create empty file `ssh` in boot partition
4. Configure WiFi (optional):
   - Create `wpa_supplicant.conf` in boot partition
5. Insert microSD and boot Raspberry Pi

### Initial Configuration

```bash
# SSH into Raspberry Pi
ssh pi@raspberrypi.local
# Default password: raspberry

# Change default password
passwd

# Update system
sudo apt update && sudo apt upgrade -y

# Enable I²C interface
sudo raspi-config
# → Interface Options → I²C → Enable → Reboot
```

### Install Dependencies

```bash
# Install Python and tools
sudo apt install -y python3-pip python3-venv git i2c-tools

# Verify I²C is enabled
lsmod | grep i2c
# Should show i2c_bcm2835 or similar

# Test I²C bus (no devices connected yet)
i2cdetect -y 1
```

---

## 2. Connect Sensors

### BME280 / SHT31 (I²C)

**Wiring:**

| Sensor Pin | Raspberry Pi Pin | GPIO | Function |
|------------|------------------|------|----------|
| VCC / VIN  | Pin 1            | -    | 3.3V Power |
| GND        | Pin 6            | -    | Ground |
| SCL        | Pin 5            | GPIO 3 | I²C Clock |
| SDA        | Pin 3            | GPIO 2 | I²C Data |

**Raspberry Pi Pinout Reference:** [pinout.xyz](https://pinout.xyz/)

### Multiple Sensors (Optional)

If using 2 sensors (e.g., bottom + top zone monitoring), ensure **different I²C addresses**:

**BME280:**
- Default: `0x76`
- Alternate: `0x77` (bridge SDO pin to VCC)

**SHT31:**
- Default: `0x44`
- Alternate: `0x45` (connect ADDR pin to VCC)

### Test Sensor Connection

```bash
# Detect I²C devices
i2cdetect -y 1

# Example output with BME280 at 0x76:
#      0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
# 00:          -- -- -- -- -- -- -- -- -- -- -- -- --
# 10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
# 20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
# 30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
# 40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
# 50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
# 60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
# 70: -- -- -- -- -- -- 76 --
```

If sensor is not detected:
- Check wiring (VCC, GND, SCL, SDA)
- Verify I²C is enabled (`sudo raspi-config`)
- Try different I²C address (check sensor datasheet)

---

## 3. Connect Actuators

### Option A: Shelly Smart Plugs (Recommended)

**No GPIO wiring needed!**

1. **Setup Shelly devices:**
   - Plug Shelly into outlet
   - Connect via Shelly app (iOS/Android)
   - Configure WiFi (same network as Raspberry Pi)
   - Note IP addresses (e.g., `192.168.1.100`)

2. **Test Shelly control:**
   ```bash
   # Turn ON (replace IP with your Shelly's IP)
   curl http://192.168.1.100/relay/0?turn=on

   # Turn OFF
   curl http://192.168.1.100/relay/0?turn=off

   # Check status
   curl http://192.168.1.100/status
   ```

3. **Assign Shelly devices to lights:**
   - Dawn/Dusk LED → Shelly #1
   - Daylight Tube → Shelly #2
   - Basking Spot → Shelly #3
   - Moonlight → Shelly #4 (or GPIO)
   - Rain System → Shelly #5

**Recommended:** Set static IP addresses in your router's DHCP settings for Shelly devices.

---

### Option B: GPIO Relay Module (Advanced)

**⚠️ Safety Warning:** Use optocouplers when switching 230V AC loads. Never connect 230V directly to GPIO pins.

**Wiring:**

| Relay Module Pin | Raspberry Pi Pin | GPIO | Function |
|------------------|------------------|------|----------|
| VCC              | Pin 2 / Pin 4    | -    | 5V Power |
| GND              | Pin 6 / Pin 14   | -    | Ground |
| IN1              | Pin 11           | GPIO 17 | Dawn/Dusk LED |
| IN2              | Pin 13           | GPIO 27 | Daylight Tube |
| IN3              | Pin 15           | GPIO 22 | Basking Spot |
| IN4              | Pin 16           | GPIO 23 | Moonlight |

**Relay Module Logic:**
- Most relay modules are **active LOW** (LOW = relay ON, HIGH = relay OFF)
- Check your module datasheet and adjust software accordingly

**Test GPIO control:**

```bash
# Install GPIO tools
sudo apt install -y wiringpi

# Set GPIO 17 to output mode
gpio -g mode 17 out

# Turn relay ON (set LOW for active-low relay)
gpio -g write 17 0

# Turn relay OFF (set HIGH)
gpio -g write 17 1

# Check GPIO status
gpio readall
```

**Lamp Wiring (230V AC):**

```
230V Live ──┬──> Relay COM (Common)
            │
Relay NO ───┴──> Lamp ──> 230V Neutral
(Normally Open)
```

**⚠️ Electrical Safety:**
- Use certified relay module rated for 230V AC
- Use proper wire gauge (minimum 0.75mm² for lamps)
- Keep 230V wiring away from 5V/3.3V logic
- Use cable glands to prevent strain on connections
- Test with multimeter before connecting lamps

---

## 4. Configuration

### Create Hardware Config

```bash
# Create config directory
mkdir -p ~/terrarium_os/config

# Create hardware.yaml
nano ~/terrarium_os/config/hardware.yaml
```

**Example `hardware.yaml`:**

```yaml
sensors:
  - type: bme280
    address: 0x76
    location: bottom

  - type: bme280
    address: 0x77
    location: top

actuators:
  lights:
    dawn:
      type: shelly
      ip: 192.168.1.100

    daylight:
      type: shelly
      ip: 192.168.1.101

    basking:
      type: shelly
      ip: 192.168.1.102

    moonlight:
      type: gpio
      pin: 23

  rain:
    type: shelly
    ip: 192.168.1.103
```

**For GPIO-only setup:**

```yaml
actuators:
  lights:
    dawn:
      type: gpio
      pin: 17

    daylight:
      type: gpio
      pin: 27

    basking:
      type: gpio
      pin: 22

    moonlight:
      type: gpio
      pin: 23
```

---

## 5. Testing Hardware

### Test Sensors

```bash
# Python test script for BME280
python3 << EOF
import smbus2
import bme280

port = 1
address = 0x76
bus = smbus2.SMBus(port)

calibration_params = bme280.load_calibration_params(bus, address)
data = bme280.sample(bus, address, calibration_params)

print(f"Temperature: {data.temperature:.2f} °C")
print(f"Humidity: {data.humidity:.2f} %")
print(f"Pressure: {data.pressure:.2f} hPa")
EOF
```

If script fails, install library:
```bash
pip3 install smbus2 bme280
```

### Test Actuators (CLI Mode)

**Coming in Phase 1:** See [Issue #5](https://github.com/YOUR_USERNAME/TerrariumOS/issues/5)

```bash
# Test individual lights
python -m terrarium_os.cli --test-light dawn --duration 30
python -m terrarium_os.cli --test-light daylight --duration 60

# Test rain system
python -m terrarium_os.cli --test-rain --duration 10
```

---

## 6. Troubleshooting

### Sensors Not Detected

```bash
# Check I²C bus
i2cdetect -y 1

# If sensor not visible:
# - Check wiring (VCC, GND, SCL, SDA)
# - Verify I²C is enabled (sudo raspi-config)
# - Try different I²C address (check sensor datasheet)
# - Check for loose connections
```

### Shelly Not Responding

- Verify Shelly is on same local network as Raspberry Pi
- Check IP address (Shelly app or router DHCP list)
- Ping Shelly device: `ping 192.168.1.100`
- Access Shelly web interface: `http://192.168.1.100`
- Ensure Shelly firmware is up to date

### GPIO Relays Not Switching

- Check relay module power (5V, sufficient current)
- Verify GPIO pin numbers (BCM numbering vs. physical pins)
- Check if relay is active-LOW or active-HIGH
- Test GPIO manually with `gpio` command
- Check for loose jumper wire connections

### Permission Errors

```bash
# Add user to gpio and i2c groups
sudo usermod -a -G gpio,i2c $USER

# Logout and login again
exit
```

---

## 7. Advanced Topics

### PWM Dimming (Phase 2+)

For smooth dawn/dusk transitions, use PWM (Pulse Width Modulation):

**Hardware:**
- PWM-capable GPIO pins (GPIO 12, 13, 18, 19)
- MOSFET driver (e.g., IRLZ44N)
- 12V LED strip

**Software:** Planned for future release.

### Power Management

**UPS (Uninterruptible Power Supply):**
- Recommended for critical setups
- PiJuice HAT or similar
- Allows graceful shutdown on power loss

### Remote Access

**VPN Setup (Phase 5):**
- WireGuard recommended
- Access dashboard remotely
- See [roadmap.md](../../docs/roadmap.md)

---

## Further Reading

- [Raspberry Pi GPIO Pinout](https://pinout.xyz/)
- [I²C Sensor Tutorial (Adafruit)](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c)
- [Shelly API Documentation](https://shelly-api-docs.shelly.cloud/)
- [Safe 230V Switching with Relays](https://www.sainsmart.com/blogs/news/how-to-use-relay-module-with-raspberry-pi)

---

## Support

For setup issues, open an issue on GitHub with the `question` label.

Include:
- Hardware component (e.g., BME280, Shelly Plug)
- Wiring setup (photo if possible)
- Error messages or command output
- Output of `i2cdetect -y 1` (for sensor issues)
