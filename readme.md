![SofleKeyboard default keymap](https://i.imgur.com/MZxVvm9.png)
![SofleKeyboard adjust layer](https://i.imgur.com/f5sKy0I.png)

# Default keymap for Sofle Keyboard

Layout in [Keyboard Layout Editor](http://www.keyboard-layout-editor.com/#/gists/76efb423a46cbbea75465cb468eef7ff) and [adjust layer](http://www.keyboard-layout-editor.com/#/gists/4bcf66f922cfd54da20ba04905d56bd4)

https://github.com/Coko7/sofle
https://github.com/caksoylar/keymap-drawer?tab=readme-ov-file#customization

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
keymap parse --columns 12 --qmk-keymap-json keymap.json > keymap.yaml

# Generate SVG visualization
keymap draw keymap.yaml > keymap.sofle.svg
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

## Orden recomendado de comandos

A continuación se describe el flujo típico para validar, compilar y visualizar tu keymap, junto con la explicación de cada comando y sus parámetros:

1. **Lint del keymap**
   ```bash
   qmk lint -km jhonnycgarcia -kb sofle/rev1 --strict
   ```
   - **Función:** Verifica que tu keymap cumpla con las reglas y convenciones de QMK, detectando errores o advertencias antes de compilar.
   - **Parámetros:**
     - `-km jhonnycgarcia`: Especifica el nombre de tu keymap.
     - `-kb sofle/rev1`: Indica el modelo de teclado.
     - `--strict`: Aplica reglas estrictas de validación.

2. **Compilación del firmware**
   ```bash
   qmk compile -kb sofle/rev1 -km jhonnycgarcia
   ```
   - **Función:** Compila el firmware de QMK para tu teclado y keymap personalizados.
   - **Parámetros:**
     - `-kb sofle/rev1`: Modelo de teclado.
     - `-km jhonnycgarcia`: Nombre del keymap.

3. **Conversión del keymap a JSON**
   ```bash
   qmk c2json --no-cpp keymap.c -o keymap.json
   ```
   - **Función:** Convierte el archivo `keymap.c` a formato JSON, necesario para herramientas de visualización y análisis.
   - **Parámetros:**
     - `--no-cpp`: Omite el preprocesador de C.
     - `keymap.c`: Archivo fuente del keymap.
     - `-o keymap.json`: Archivo de salida en formato JSON.

4. **Parseo del keymap a YAML**
   ```bash
   keymap parse --columns 12 --qmk-keymap-json keymap.json > keymap.yaml
   ```
   - **Función:** Convierte el keymap en JSON a formato YAML, facilitando su edición y visualización.
   - **Parámetros:**
     - `--columns 12`: Define el número de columnas del teclado (ajusta según tu layout).
     - `--qmk-keymap-json keymap.json`: Archivo JSON de entrada.
     - `> keymap.yaml`: Archivo de salida en YAML.

5. **Generación de visualización SVG**
   ```bash
   keymap draw keymap.yaml > keymap.sofle.svg
   ```
   - **Función:** Genera una imagen SVG del layout de tu keymap para documentación o revisión visual.
   - **Parámetros:**
     - `keymap.yaml`: Archivo YAML de entrada.
     - `> keymap.sofle.svg`: Archivo SVG de salida.

> **Nota:** Asegúrate de ejecutar los comandos en este orden para garantizar la validez y correcta visualización de tu keymap.