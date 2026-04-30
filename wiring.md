# Wiring Guide

## 1) GPIO Mapping

### Keypad (4x4)

| Keypad Pin | Pico GPIO |
|---|---|
| C1 | GP19 |
| C2 | GP18 |
| C3 | GP17 |
| C4 | GP16 |
| R1 | GP26 |
| R2 | GP22 |
| R3 | GP21 |
| R4 | GP20 |

> Diagram also shows optional pull-up network on keypad rows to 3V3 using four 1k resistors.

### LEDs (12 outputs)

| Logical LED | Pico GPIO | Key Trigger |
|---|---:|---|
| LED1 | GP11 | `1` |
| LED2 | GP10 | `2` |
| LED3 | GP9  | `3` |
| LED4 | GP8  | `4` |
| LED5 | GP7  | `5` |
| LED6 | GP6  | `6` |
| LED7 | GP5  | `7` |
| LED8 | GP4  | `8` |
| LED9 | GP3  | `A` |
| LED10 | GP2 | `B` |
| LED11 | GP28 | `C` |
| LED12 | GP27 | `D` |

All LED cathodes go to GND. Each anode is driven from GPIO through a **220Ω resistor**.

## 2) Components List (BOM)

- 1x Raspberry Pi Pico W (RP2040)
- 1x 4x4 membrane keypad (8-pin)
- 12x LEDs (8 blue + 4 red in the reference design)
- 12x 220Ω resistors (LED current limiting)
- 4x 1kΩ resistors (row pull-ups shown in Wokwi diagram)
- Breadboard + jumper wires
- 5V USB power/data cable

## 3) Wokwi-specific notes

- Use the included `diagram.json` directly.
- Serial monitor is connected to GP0/GP1 in the diagram, though firmware does not print serial logs.

## 4) Real hardware notes

- RP2040 GPIO is **3.3V only**. Do not apply 5V on GPIO pins.
- If LEDs look dim/bright, you may adjust resistor values (e.g., 330Ω), but this changes electrical behavior only, not code logic.
- Ensure common ground across keypad and LED circuits.
