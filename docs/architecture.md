# Architecture

## System overview

The firmware is a single-loop keypad scanner controlling 12 digital outputs.

- **Input subsystem**: `Keypad` library scans 4 rows x 4 columns.
- **Output subsystem**: 12 GPIO outputs drive 12 LEDs.
- **Control logic**: `switch(key)` maps each key to either single LED control or bank-wide action.

## Software structure

### Constants and pin maps

- `LEDS = 12`, `ROWS = 4`, `COLS = 4`
- `keys[][]` holds the keypad layout.
- `ledPins[]` maps logical LED indices 0..11 to GPIOs.
- `rowPins[]` and `colPins[]` map keypad matrix lines.

### setup()

- Iterates over all LED pins.
- Configures each as `OUTPUT`.
- Initializes all LEDs to `LOW` (OFF).

### loop()

1. Polls keypad with `keypad.getKey()`.
2. If key is valid (`!= NO_KEY`), dispatches action:
   - `1..8`: turn ON one LED in blue bank
   - `9`: turn ON all LEDs in blue bank (indices 0..7)
   - `0`: turn OFF all LEDs in blue bank
   - `A..D`: turn ON one LED in red bank (indices 8..11)
   - `*`: turn ON all LEDs in red bank
   - `#`: turn OFF all LEDs in red bank
3. Sleeps `delay(10)` for loop pacing.

## Behavioral notes

- Actions are **latching**: single-key ON commands do not auto-turn OFF the LED.
- There is no explicit global reset key for all 12 LEDs simultaneously.
- No state machine is required; GPIO state itself is the persistent state.

## Constraints

- Logic intentionally preserved from original source.
- No functional extensions, no remapped keys, and no altered debounce strategy.
