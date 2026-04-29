# Architecture Overview

## High-Level Data Flow

1. **Keypad scan/read**
   - Firmware drives/reads keypad matrix GPIO lines.
2. **Decode key**
   - Row/column state is converted into a logical key (e.g., numeric or symbolic key ID).
3. **LED control logic**
   - Decoded key is processed by application logic, which updates LED output pins.

In short: **scan matrix → decode key event → update LED outputs**.

## File / Module Responsibilities

> Current repository contents are minimal. The responsibilities below describe the intended layout referenced by the request.

### `src/main.py`

- Hardware initialization for keypad and LED GPIO pins.
- Main loop for keypad scanning and event handling.
- Invocation of LED update logic based on decoded key input.

### `lib/*` helpers (if present)

- `lib/keypad*` (typical): matrix scanning utilities and key decode helpers.
- `lib/led*` (typical): LED state mapping and GPIO write helpers.
- `lib/utils*` (typical): shared timing/state helpers.

If no `lib/*` modules currently exist, these are planned logical separations for maintainability.

## Runtime Behavior Summary

Without changing business logic semantics:

- Firmware repeatedly scans keypad rows/columns.
- When a valid key state is detected, it is decoded to an internal key representation.
- Existing LED behavior (as implemented in firmware) is applied by writing HIGH/LOW states to the mapped GPIO pins.
- The loop continues continuously for interactive input/output behavior.

## Extension Points (Future Work)

Clearly marked areas to extend later:

1. **Debounce layer** (future)
   - Insert between scan/read and decode.
   - Purpose: suppress chatter from mechanical key bounce.

2. **Wi-Fi telemetry** (future)
   - Add after key decode or LED state update.
   - Purpose: publish key events/LED states to a remote endpoint.

3. **Explicit state machine** (future)
   - Wrap current control logic in states (e.g., idle/input/alert/test mode).
   - Purpose: improve scalability as behavior grows.

## Wokwi vs Real Hardware Differences

- **Timing behavior:** simulator timing is stable; real boards may show jitter and occasional latency spikes.
- **Electrical characteristics:** simulator omits many analog artifacts (bounce/noise/ground issues) that affect matrix scanning and LED drive reliability.
- **USB serial:** Wokwi console is persistent/virtual; real USB serial depends on host enumeration and may miss early boot logs unless connection timing is handled.
