# Configuration

Thank you [Schnoog](https://schnoog.eu/hobbies/3dprinting/ender-3-v3-se-klippered) for much of this on this page.

## 0xD34D's Ender 3 V3 SE Configuration files

This project, [jpcurti/ender3-v3-se-klipper-with-display](https://github.com/jpcurti/ender3-v3-se-klipper-with-display), is forked from [0xD34D/klipper_ender3_v3_se](https://github.com/0xD34D/klipper_ender3_v3_se) so we will be using the config files from [0xD34D/ender3-v3-se-klipper-config](https://github.com/0xD34D/ender3-v3-se-klipper-config)

<!-- markdownlint-disable-next-line MD001 -->
#### Download the config files from Github

```sh
curl "https://raw.githubusercontent.com/0xD34D/ender3-v3-se-klipper-config/main/prtouch.cfg" > ~/printer_data/config/prtouch.cfg

curl "https://raw.githubusercontent.com/0xD34D/ender3-v3-se-klipper-config/main/printer-creality-ender3-v3-se-2023.cfg" > ~/printer_data/config/printer.cfg
```

#### Add the reference to `prtouch.cfg` into `printer.cfg`

```sh
echo '[include prtouch.cfg]' >> ~/printer_data/config/printer.cfg
```

## Ender 3 V3 SE Display configuration

<!-- markdownlint-disable-next-line MD001 -->
#### Add the display settings into `printer.cfg`

**NOTE** - Replace `english` with your language of choice and enable logging if desired.

```sh
echo '[e3v3se_display]' >> ~/printer_data/config/printer.cfg
echo 'language: english' >> ~/printer_data/config/printer.cfg
echo 'logging: False' >> ~/printer_data/config/printer.cfg
```

## Initial `macros.cfg`

Macros are a predefined series of gcodes with a friendly name to make common tasks simple.  These can be customized and added to suit your needs.  

To get started, we will use an existing `macros.cfg`. Based on the recommendation from [Artamis` Ultimate Guide for Klipper Installation](https://artamis.me/projects/klipper_guide/#configuration), we will use [shubham0x13's](https://github.com/shubham0x13/ender-3-v3-se-klipper/blob/main/macros.cfg).  It is fully documented to explain what each line is doing.

```sh
curl https://raw.githubusercontent.com/shubham0x13/ender-3-v3-se-klipper/refs/heads/main/macros.cfg > ~/printer_data/config/macros.cfg
```

<!-- markdownlint-disable-next-line MD001 -->
#### Add the reference to `macros.cfg` into `printer.cfg`

```sh
echo '[include macros.cfg]' >> ~/printer_data/config/printer.cfg
```

## Add macros to the E3V3SE display

Macros defined on Klipper can be used on your screen directly, e.g.: Load/Unload filament, calibrate Z offset, calibrate bed mesh, clean nozzle, etc.  The macros defined in `macros.cfg` are not automatically loaded and the menu must be configured in `printer.cfg`.

On your `printer.cfg` you can define the macros using a new config section `[e3v3se_display MACRO%I]` where `%i` is the macro number (This should be unique per macro). The following properties are available:

| Property | Data type | Required | Description                                                      |
|----------|-----------|----------|------------------------------------------------------------------|
| label    | Text      | Yes      | Text to be displayed on the screen                               |
| icon     | Integer   | No       | Internal firmware icon. Defaults to 14 (file icon)               |
| gcode    | Text      | Yes      | GCODE to be run when the item is selected.  i.e `G28` for homing |

Some examples for your inspiration:

```yaml
[e3v3se_display MACRO1]
gcode: LOAD_FILAMENT
label: Load filament
icon: 14

[e3v3se_display MACRO2]
gcode: UNLOAD_FILAMENT
label: Unload filament
icon: 14

[e3v3se_display MACRO3]
gcode: CALIBRATE_Z_OFFSET
label: Calibrate Z offset
icon: 12

[e3v3se_display MACRO4]
gcode: CALIBRATE_BED_MESH
label: Calibrate bed mesh
icon: 29

[e3v3se_display MACRO5]
gcode: CLEAN_NOZZLE
label: Clean nozzle
icon: 9
```

To browse icon library, call the macro `ENDER_SE_DISPLAY_ICON_FINDER` on your Klipper console and use the screen to navigate through the icons.

## Check klippy_uds_address in moonraker.conf

Ensure that your `moonraker.conf` has the correct `klippy_uds_address` set. Run the following

```sh
grep 'klippy_uds_address' ~/printer_data/config/moonraker.conf 
```

This should return `klippy_uds_address: /home/<YOUR SSH USER NAME>/printer_data/comms/klippy.sock`

## Configure your GUI (mainsail, fluidd or octoprint)

Installing the GUI is easily done with kiauh. Just run:

```sh
~/kiauh/kiauh.sh
```

select **1** for install and select your preferred option.

The serial console is located at `~/printer_data/comms/klippy.serial`

### You should now be able to access your printer through your web GUI
