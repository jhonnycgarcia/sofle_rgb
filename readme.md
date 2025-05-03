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

## Features:

- Symmetric modifiers (CMD/Super, Alt/Opt, Ctrl, Shift)
- Various modes, can be switched (using Adjust layer and the selected one is stored in EEPROM.
- Modes for Qwerty and Colemak support
- Modes for Mac vs Linux/Win support -> different order of modifiers and different action shortcuts on the "UPPER" layer (the red one in the image). Designed to simplify transtions when switching between operating systems often.
- The OLED on master half shows selected mode and caps lock state and is rotated.
- Left encoder controls volume up/down/mute. Right encoder PGUP/PGDOWN.
- sofle/rev1
- /Users/jhonnychristiangarciacordova/qmk_firmware/keyboards/sofle/keymaps/jhonnycgarcia
- qmk c2json --no-cpp keymap.c -o keymap.json
- keymap parse --qmk-keymap-json keymap.json > keymap.yaml
- qmk lint -km jhonnycgarcia -kb sofle/rev1 --strict
- qmk compile -kb sofle/rev1 -km jhonnycgarcia
- https://github.com/samhocevar-forks/qmk-firmware/blob/master/docs/keycodes.md
- qmk flash -kb sofle/rev1 -km jhonnycgarcia
- qmk flash -kb sofle/rev1 -km jhonnycgarcia -bl avrdude-split-left
- qmk flash -kb sofle/rev1 -km jhonnycgarcia -bl avrdude-split-right