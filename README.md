# Raspberry Pi Pico W Keypad-to-LED Controller

Cleaned project structure for a **Raspberry Pi Pico W (RP2040)** + **4x4 membrane keypad** + **12 LEDs** controller using Arduino-style C++.

> Logic is unchanged from the provided source.

## Repository structure

- `sketch.ino` — firmware source
- `diagram.json` — Wokwi diagram
- `wiring.md` — pin-by-pin wiring for simulation and real hardware
- `architecture.md` — behavior and software architecture notes

## Features

- Maps 4x4 keypad keys to 12 LED outputs.
- Controls LEDs in two banks:
  - **Blue bank** (LED1..LED8): keys `1..8`, plus `9`=all ON, `0`=all OFF
  - **Red bank** (LED9..LED12): keys `A..D`, plus `*`=all ON, `#`=all OFF
- 10ms loop delay for simple debounce pacing.

## Quick start (Wokwi)

1. Open [wokwi.com](https://wokwi.com/).
2. Create a new **Raspberry Pi Pico** project.
3. Replace `diagram.json` with this repo's `diagram.json`.
4. Paste `sketch.ino` into the code editor.
5. Add `Keypad` library if prompted.
6. Run simulation and press keypad keys.

## Quick start (real hardware)

1. Wire components exactly as described in `wiring.md`.
2. Open Arduino IDE (or PlatformIO) and select:
   - Board: **Raspberry Pi Pico W**
   - Core: Earle Philhower RP2040 core
3. Install library: **Keypad** by Mark Stanley / Alexander Brevig.
4. Build and upload `sketch.ino`.

## GPIO mapping and detailed architecture

See:
- [`wiring.md`](./wiring.md)
- [`architecture.md`](./architecture.md)
