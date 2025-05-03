![SofleKeyboard default keymap](https://i.imgur.com/MZxVvm9.png)
![SofleKeyboard adjust layer](https://i.imgur.com/f5sKy0I.png)

# Default keymap for Sofle Keyboard

Layout in [Keyboard Layout Editor](http://www.keyboard-layout-editor.com/#/gists/76efb423a46cbbea75465cb468eef7ff) and [adjust layer](http://www.keyboard-layout-editor.com/#/gists/4bcf66f922cfd54da20ba04905d56bd4)

## Requirements

To work with this keyboard configuration, you'll need:

1. **QMK Firmware**
   - QMK CLI tools installed
   - QMK Firmware repository cloned
   - Basic understanding of QMK configuration

2. **Development Tools**
   - AVR toolchain (for compiling and flashing)
   - Git (for version control)
   - Python (for QMK CLI tools)
   - QMK Toolbox (GUI application for flashing keyboards)

3. **Hardware Requirements**
   - Sofle Keyboard (rev1)
   - USB cables
   - AVR programmer (for flashing)

4. **Software Dependencies**
   - avrdude (for flashing)
   - c2json tool (for keymap conversion)
   - keymap parser (for YAML conversion)

## About the Sofle Keyboard

The Sofle Keyboard is a split keyboard with the following specifications:

- **QMK Code**: `sofle/rev1`
- **Type**: Split keyboard
- **Layout**: 6x4+4 keys
- **Display**: Dual OLED displays (one on each half)
- **Encoders**: Two rotary encoders
  - Left: Volume control (up/down/mute)
  - Right: Page navigation (PGUP/PGDOWN)
- **Connectivity**: USB-C
- **Firmware**: QMK compatible

The keyboard features a symmetric design with mirrored modifiers and supports multiple layout modes that can be stored in EEPROM.

## QMK Commands

### Parameters
Before running any command, you'll need to set these parameters:
- `KEYBOARD`: Your keyboard name (e.g., `sofle/rev1`)
- `KEYMAP`: Your keymap name (e.g., `yourProfile`)
- `KEYMAP_PATH`: Path to your keymap directory (e.g., `~/qmk_firmware/keyboards/sofle/keymaps/your_keymap`)

### Compilation and Flashing
```bash
# Compile the firmware
qmk compile -kb KEYBOARD -km KEYMAP

# Flash the entire keyboard
qmk flash -kb KEYBOARD -km KEYMAP

# Flash left half
qmk flash -kb KEYBOARD -km KEYMAP -bl avrdude-split-left

# Flash right half
qmk flash -kb KEYBOARD -km KEYMAP -bl avrdude-split-right
```

### Keymap Management
```bash
# Convert keymap to JSON format
qmk c2json --no-cpp KEYMAP_PATH/keymap.c -o keymap.json

# Parse keymap to YAML format
keymap parse --qmk-keymap-json keymap.json > keymap.yaml
```

### Validation
```bash
# Lint check the keymap
qmk lint -km KEYMAP -kb KEYBOARD --strict
```

### Keymap Location
Your keymap should be located in the QMK firmware directory structure:
```
~/qmk_firmware/keyboards/KEYBOARD/keymaps/KEYMAP/
```