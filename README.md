# Pico W Wokwi Template Project

## Project Overview
This repository is a starter template for running a **Raspberry Pi Pico W + MicroPython** project in both:

- **Wokwi simulation** (fast iteration), and
- **real hardware deployment** (physical Pico W board).

It documents the expected workflow for flashing firmware, deploying project files, validating serial output, and keeping Wi-Fi credentials out of source code.

## Features
- MicroPython-first workflow for Raspberry Pi Pico W.
- Compatible simulation flow for Wokwi.
- Clear deployment steps for real boards.
- Wi-Fi configuration pattern using a local config file or env-style values.
- Wiring and GPIO reference with dedicated documentation links.

## Repository Structure
Current and expected key paths:

- `README.md` — setup and usage guide.
- `diagram.json` — Wokwi diagram and pin definition source.
- `docs/wiring.md` — wiring notes and expanded GPIO details.
- `src/main.py` — application entrypoint to deploy to the Pico W.
- `lib/` — additional MicroPython modules used by `src/main.py`.

> If your local clone does not yet include some paths, add them following this structure.

## Hardware Components
Typical bill of materials:

- Raspberry Pi Pico W
- USB data cable (USB cable with data lines, not charge-only)
- Breadboard and jumper wires
- Optional peripherals/sensors/actuators used by your app
- 5V USB power source (or powered USB hub)

## GPIO Mapping Summary
GPIO usage is **authoritatively defined** in:

- `diagram.json`, and
- `docs/wiring.md`.

Always treat those files as the source of truth before connecting or reassigning pins.

## Running in Wokwi
1. Open/import this project in Wokwi.
2. Confirm `diagram.json` matches your intended hardware wiring.
3. Start the simulation.
4. Watch console logs for successful startup and runtime behavior.

## Running on Real Pico W (MicroPython UF2 + file deployment)
1. Download the latest stable **MicroPython UF2 for Raspberry Pi Pico W**.
2. Hold **BOOTSEL** while connecting the Pico W over USB.
3. Copy the UF2 file to the mounted `RPI-RP2` drive.
4. After reboot, connect with a MicroPython tool (e.g., Thonny, mpremote, rshell, ampy).
5. Copy project files:
   - `src/main.py` -> board as `main.py`
   - `lib/` modules -> board `lib/` directory
6. Reset the board and verify serial logs.

## Wi-Fi Configuration (no hardcoded secrets)
Never hardcode SSID/password in committed source files.

Recommended pattern:

- Keep credentials in a local, untracked config file (for example `wifi.local.env`), or
- Inject values using an env-style key/value workflow during deployment.

Example env-style format:

```env
WIFI_SSID=your_network_name
WIFI_PASSWORD=your_secret_password
```

Then load these values in your deployment process or generate a local config module that is excluded from version control.

## Quick Start
1. Flash MicroPython UF2 to Pico W.
2. Copy `src/main.py` and required `lib/` modules to the board.
3. Open serial console and verify startup logs.

## Troubleshooting
- **No serial output**: Confirm baud rate expected by your app/tooling (common values are 115200 or tool defaults).
- **Board not detected**: Use a USB **data** cable; many charge-only cables cannot transfer data.
- **Unexpected behavior**: Check for pin conflicts against `diagram.json` and `docs/wiring.md`.
- **Random resets / unstable peripherals**: Verify shared ground, wiring quality, and adequate power.
- **Wi-Fi not connecting**: Validate local credentials file format and ensure secrets are loaded at runtime.
