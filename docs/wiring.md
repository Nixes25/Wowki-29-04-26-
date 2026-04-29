# Wiring Reference

## Components (from `diagram.json`)

- 1× Raspberry Pi Pico / Pico W
- 1× 4x4 membrane keypad
- 12× LEDs
  - 8× blue LEDs labeled **1–8**
  - 4× red LEDs labeled **A–D**
- 12× 220Ω resistors (one per LED)
- 4× 1kΩ pull-up resistors for keypad rows

## GPIO Mapping

### Keypad Columns

| Keypad column | Pico GPIO |
|---|---|
| C1 | GP19 |
| C2 | GP18 |
| C3 | GP17 |
| C4 | GP16 |

### Keypad Rows

| Keypad row | Pico GPIO |
|---|---|
| R1 | GP26 |
| R2 | GP22 |
| R3 | GP21 |
| R4 | GP20 |

### LED Outputs

| Pico GPIO | LED label |
|---|---|
| GP11 | LED1 |
| GP10 | LED2 |
| GP9  | LED3 |
| GP8  | LED4 |
| GP7  | LED5 |
| GP6  | LED6 |
| GP5  | LED7 |
| GP4  | LED8 |
| GP3  | LEDA |
| GP2  | LEDB |
| GP28 | LEDC |
| GP27 | LEDD |

## Power and Ground Notes

- Use a **common GND** for all LED cathodes.
- Tie keypad pull-up resistors to **3V3**.
- Ensure the Pico ground is shared by keypad and LED circuits.

## Assumptions

If firmware naming differs from physical labels:

- `LED1..LED8` map to the blue LEDs physically labeled **1..8**.
- `LEDA..LEDD` map to the red LEDs physically labeled **A..D**.
- Any alternative naming used in code (e.g., arrays or index-based names) should preserve this one-to-one physical mapping.

## Wokwi vs Real Hardware Notes

- **Timing:** Wokwi often behaves deterministically; on real hardware, scan timing can vary due to clock tolerances and execution jitter.
- **Electrical noise:** Wokwi generally has idealized signals; real keypads and breadboards can introduce contact bounce, noise pickup, and floating behavior if pull-ups are weak/miswired.
- **USB serial behavior:** Wokwi serial is virtual and usually instantly available; on real hardware, USB CDC may enumerate with a delay and can disconnect/reconnect on reset.
