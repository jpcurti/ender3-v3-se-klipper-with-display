<!-- markdownlint-disable-next-line MD041 -->
[![Build Firmware](https://github.com/Atomique13/ender3-v3-se-klipper-with-display/actions/workflows/build-firmware.yaml/badge.svg)](https://github.com/Atomique13/ender3-v3-se-klipper-with-display/actions/workflows/build-firmware.yaml)

# Modified Klipper for the Creality Ender 3 V3 SE with display support

This is a modified [Klipper](https://www.klipper3d.org/) that supports the original **Creality E3V3SE (Ender 3 V3 SE)** display by combining [E4ST2W3ST serial bridge](https://github.com/Klipper3d/klipper/commit/6469418d73be6743a7130b50fdb5a57d311435ca) with the [ender 3 v3 se display interface](https://github.com/jpcurti/E3V3SE_display_klipper) to make it possible to use the printers display cable without any hardware modification. This repository is forked from [0XD34Ds klipper config](https://github.com/0xD34D/klipper_ender3_v3_se), but its commits can be applied separately from any other configuration.

![Demonstration image](images/display_e3v3se_klipper.gif)

## Supported features

The currently supported features are:

| Feature                | Status  |
| ---------------------- | ------- |
| Print file             | &check; |
| Tune print             | &check; |
| Pause/continue print   | &check; |
| Stop print             | &check; |
| Move Axis              | &check; |
| Home Axis              | &check; |
| Set Z offset           | &check; |
| Disable step motors    | &check; |
| Preheat bed            | &check; |
| Cooldown               | &check; |
| Set nozzle temperature | &check; |
| Set bed temperature    | &check; |
| Set max speed          | &cross; |
| Set max acceleration   | &cross; |
| Set steps per-mm       | &cross; |
| Manual probe popup     | &check; |
| Custom macros menu     | &check; |

Features that are not available are shown as a pop-up:

![Demonstration image](https://github.com/jpcurti/E3V3SE_display_klipper/blob/main/docs/img/disabled_features.gif?raw=true)

## Related projects and credits

* This repository is heavily based on the [DWIN_T5UIC1_LCD](https://github.com/odwdinc/DWIN_T5UIC1_LCD) repository for the E3V2 display and makes use of most of the available classes and methods implemented there, with the necessary modifications for the E3V3SE display. All credits goes to the [author of the DWIN_T5UIC1_LCD project](https://github.com/odwdinc) for making the version which this repository is based on.

* This repository includes a proposed change proposed by [E4ST2W3ST](https://github.com/Klipper3d/klipper/commit/6469418d73be6743a7130b50fdb5a57d311435ca) to enable the MCU to act as a serial bridge between USB and the display serial port. Without his work, this project wouldn't exist.

* This repository is forked and makes use of an already configuration for the ender 3 v3 se made by [0XD34D](https://github.com/0xD34D/klipper_ender3_v3_se), where a lot of different improvements were made.

## Other useful links

* [Klipper documentation](https://www.klipper3d.org)
* [Octoprint](https://octoprint.org/)
* [Moonraker - Web API Server for Klipper](https://github.com/arksine/moonraker)
* [DWIN_T5UIC1_LCD - Python class for the Ender 3 V2 LCD](https://github.com/odwdinc/DWIN_T5UIC1_LCD)
* [jpcurti's Python based interface for the Creality Ender 3 V3 SE display running Klipper](https://github.com/jpcurti/E3V3SE_display_klipper)
* [0xD34D's Ender3 V3 SE Klipper config](https://github.com/0xD34D/klipper_ender3_v3_se)
* [Schnoog's documentation](https://schnoog.eu/hobbies/3dprinting/ender-3-v3-se-klippered) - The basis of this guide.
* [Ultimate Guide for Klipper Installation on Ender 3 V3 SE](https://artamis.me/projects/klipper_guide/) - Another general Klipper install guide for the Ender 3 V3 SE.
