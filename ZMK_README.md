# ZMK Configuration for rossw42 3x4 Extended Macropad

This repository contains the ZMK firmware configuration for a custom 3x4 (15-key) macropad using a nice!nano v2 controller.

## Hardware

- **Controller**: nice!nano v2 (nRF52840)
- **Layout**: 3 rows × 5 columns (15 keys total)
- **Connectivity**: Wireless (Bluetooth) + USB-C
- **Power**: Battery powered via nice!nano

## Project Structure

```
├── config/                          # User configuration
│   ├── 3x4macropad.keymap          # Your personal keymap
│   ├── 3x4macropad.conf            # Your configuration settings
│   └── west.yml                    # ZMK dependencies
├── boards/shields/rossw42_3x4/     # Hardware definition
│   ├── rossw42_3x4.overlay         # Pin assignments & matrix
│   ├── rossw42_3x4.keymap          # Default shield keymap
│   ├── rossw42_3x4.conf            # Default shield config
│   ├── Kconfig.shield              # Shield definition
│   └── Kconfig.defconfig           # Default settings
└── build.yaml                      # Build configuration
```

## Pin Assignments (nice!nano v2)

**Rows (3 pins):**

- Row 0: P0.06 (D4)
- Row 1: P0.08 (D5)
- Row 2: P0.17 (D6)

**Columns (5 pins):**

- Col 0: P0.20 (D7)
- Col 1: P0.22 (D8)
- Col 2: P0.24 (D9)
- Col 3: P1.00 (D10)
- Col 4: P0.11 (D16)

**Matrix Configuration:**

- Diode direction: COL2ROW
- Rows are inputs with pull-down resistors
- Columns are outputs driven high

## Default Layout

**Layer 0 (Default):**

```
┌─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │
├─────┼─────┼─────┼─────┼─────┤
│  6  │  7  │  8  │  9  │  0  │
├─────┼─────┼─────┼─────┼─────┤
│ ESC │ SPC │ ENT │ TAB │ FN  │
└─────┴─────┴─────┴─────┴─────┘
```

**Layer 1 (Function):**

```
┌─────┬─────┬─────┬─────┬─────┐
│ F1  │ F2  │ F3  │ F4  │ F5  │
├─────┼─────┼─────┼─────┼─────┤
│ F6  │ F7  │ F8  │ F9  │ F10 │
├─────┼─────┼─────┼─────┼─────┤
│BTCLR│ BT1 │ BT2 │ BT3 │     │
└─────┴─────┴─────┴─────┴─────┘
```

## Features

- **NKRO**: N-Key Rollover enabled
- **Bluetooth**: Multiple device pairing (up to 3 devices)
- **Power Management**: 30-second idle timeout, sleep mode enabled
- **USB-C**: Wired mode when connected
- **Consumer Keys**: Media key support

## Building Firmware

1. **Fork this repository** on GitHub
2. **Enable GitHub Actions** in your fork
3. **Push changes** - firmware builds automatically
4. **Download firmware** from the Actions tab after build completes

The build system will generate a `.uf2` file for flashing to your nice!nano.

## Flashing

1. Connect nice!nano via USB-C
2. Double-tap the reset button to enter bootloader mode
3. Drag the `.uf2` file to the mounted drive
4. The board will automatically reboot with new firmware

## Customization

Edit `config/3x4macropad.keymap` to customize your layout:

**Common ZMK Keycodes:**

- `&kp A` - Letter A
- `&kp N1` - Number 1
- `&kp F1` - Function key F1
- `&mo 1` - Momentary layer 1
- `&lt 1 SPACE` - Layer tap (hold for layer 1, tap for space)
- `&bt BT_CLR` - Clear Bluetooth bonds
- `&bt BT_SEL 0` - Select Bluetooth profile 0

**Power Features in `config/3x4macropad.conf`:**

- Adjust `CONFIG_ZMK_IDLE_TIMEOUT` for different sleep timing
- Enable `CONFIG_ZMK_RGB_UNDERGLOW` if adding RGB LEDs
- Enable `CONFIG_EC11` if adding rotary encoder

## Troubleshooting

- **Keys not working**: Verify pin assignments match your wiring
- **Bluetooth issues**: Use `&bt BT_CLR` to clear paired devices
- **Build failures**: Check GitHub Actions logs for syntax errors
- **Power issues**: Ensure battery is connected and charged

## Resources

- [ZMK Documentation](https://zmk.dev/)
- [nice!nano Pinout](https://nicekeyboards.com/docs/nice-nano/pinout-schematic)
- [ZMK Keycodes](https://zmk.dev/docs/codes)
