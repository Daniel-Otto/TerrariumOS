# TerrariumOS Software

Python-based control system for realistic terrarium environments.

---

## Overview

TerrariumOS is the software component that runs on a Raspberry Pi to control lighting, climate, and monitoring systems for tropical terrariums.

**Key Features:**
- Relative time-based scheduler (day starts at configurable time)
- Seasonal light cycle simulation (10-12h, smooth transitions)
- 4-phase lighting (dawn, day, basking, moon)
- Humidity-based climate control
- Modular sensor and actuator support

---

## Project Status

🚧 **Early Development** – Phase 1 (MVP) in progress

See [roadmap.md](../docs/roadmap.md) for planned features and milestones.

---

## Architecture

```
software/
├── terrarium_os/           # Main Python package
│   ├── __init__.py
│   ├── config/             # Configuration files (.yaml)
│   │   ├── base.yaml       # Day start time, overrides
│   │   ├── months.yaml     # Seasonal parameters
│   │   └── hardware.yaml   # GPIO / Shelly mapping
│   │
│   ├── core/               # Core logic
│   │   ├── scheduler.py    # Relative time scheduler
│   │   ├── seasons.py      # Seasonal light calculations
│   │   ├── lights.py       # Lighting control
│   │   ├── climate.py      # Humidity & temperature
│   │   └── moon.py         # Moonlight scheduling
│   │
│   ├── sensors/            # Sensor interfaces
│   │   ├── bme280.py       # BME280 temp/humidity
│   │   └── sht31.py        # SHT31 temp/humidity
│   │
│   └── actuators/          # Actuator interfaces
│       ├── relay.py        # GPIO relay control
│       └── shelly.py       # Shelly HTTP API
│
├── main.py                 # Main entry point
├── requirements.txt        # Python dependencies
└── tests/                  # Unit tests
```

---

## Installation

### Prerequisites

- Python 3.10+
- Raspberry Pi OS (or compatible Linux)
- Hardware setup complete (see [hardware documentation](../hardware/))

### Setup

```bash
# Clone repository
git clone https://github.com/YOUR_USERNAME/TerrariumOS.git
cd TerrariumOS/software

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure hardware
cp terrarium_os/config/hardware.yaml.example terrarium_os/config/hardware.yaml
nano terrarium_os/config/hardware.yaml
```

---

## Configuration

### Base Configuration (`config/base.yaml`)

```yaml
day_start: "08:30"  # When the "day" begins

overrides:
  dawn_duration: 30  # minutes
  dusk_duration: 45  # minutes
```

### Seasonal Configuration (`config/months.yaml`)

```yaml
# Example: Summer vs Winter
months:
  june:
    light_hours: 12.0
    basking_duration: 3.0

  december:
    light_hours: 10.0
    basking_duration: 2.0
```

### Hardware Configuration (`config/hardware.yaml`)

See [hardware setup guide](../hardware/electronics/setup.md) for details.

---

## Usage

### Running the Scheduler

```bash
# Activate virtual environment
source venv/bin/activate

# Run main scheduler
python main.py
```

### CLI Testing Mode (Phase 1)

Test individual components before running the full scheduler:

```bash
# Test lights
python -m terrarium_os.cli --test-light dawn --duration 30
python -m terrarium_os.cli --test-light daylight --duration 60

# Test rain system
python -m terrarium_os.cli --test-rain --duration 10
```

See [Issue #5](https://github.com/YOUR_USERNAME/TerrariumOS/issues/5) for CLI implementation.

---

## Development

### Running Tests

```bash
# Install dev dependencies
pip install -r requirements-dev.txt

# Run tests
pytest tests/
```

### Code Style

This project follows PEP 8 style guidelines.

```bash
# Format code
black terrarium_os/

# Lint code
pylint terrarium_os/
```

---

## Roadmap

See [docs/roadmap.md](../docs/roadmap.md) for detailed development plan.

**Current Phase:** Phase 1 – Core System (MVP)

**Active Issues:**
- [#1: Base scheduler with relative day start](https://github.com/YOUR_USERNAME/TerrariumOS/issues/1)
- [#2: CSV-based seasonal schedule loader](https://github.com/YOUR_USERNAME/TerrariumOS/issues/2)
- [#3: Lighting control abstraction layer](https://github.com/YOUR_USERNAME/TerrariumOS/issues/3)
- [#4: Moonlight scheduling](https://github.com/YOUR_USERNAME/TerrariumOS/issues/4)
- [#5: Manual CLI testing mode](https://github.com/YOUR_USERNAME/TerrariumOS/issues/5)

---

## Contributing

Contributions are welcome! Please:

1. Check existing issues or create a new one
2. Fork the repository
3. Create a feature branch (`git checkout -b feature/your-feature`)
4. Commit your changes
5. Open a pull request

---

## License

MIT License – See [LICENSE](../LICENSE) for details.

---

## Support

For software-related questions:
- Open an issue with the `question` label
- Check [docs/roadmap.md](../docs/roadmap.md) for planned features
- See [hardware documentation](../hardware/) for setup issues
