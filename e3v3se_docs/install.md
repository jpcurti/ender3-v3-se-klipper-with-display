# Installation

Thank you [Schnoog](https://schnoog.eu/hobbies/3dprinting/ender-3-v3-se-klippered) for much of this on this page.

## Requirements

* Your Ender 3 V3 SE
* USB C cable or a USB A to USB C cable
* a microSD card (needed if the display firmware needs to be updated and/or for Raspberry Pi)
* A Raspberry Pi 4 or Raspberry Pi 5 (or comparable device running Linux)*
* Power supply for your Pi or Linux device.

**NOTE** - This guide assumes you are using a Raspberry Pi.  For any other device, it is assumed you will know how to set it up and can get to a shell prompt.

## **Before you begin - Important**

This project is based on the **E3V3SE display firmware 1.0.6**. Any changes in the firmware version, such as a new version from Creality, can change the assets locations within the display memory and a new mapping would be necessary. A list of available firmware can be found [on Creality website](https://www.creality.com/pages/download-ender-3-v3-se) and a detailed instruction on how to update your display is available on [youtube](https://www.youtube.com/watch?v=8oRuCusCyUM&ab_channel=CrealityAfter-sale).

## Step 0 - Preparing your Pi

It is recommended you run Raspberry Pi OS Lite.  

If this is new to you, [follow the official Raspberry Pi organization's instructions](https://www.raspberrypi.com/documentation/computers/getting-started.html) and be sure to **Enable SSH** along with any other relevant OS customizations.

After you have configured and flashed your OS to the microSD card, insert the card into the Pi and wait for it to complete the initial boot process.  Once done, you should be able to SSH into the Pi.

## Step 1 - SSH into your Raspberry Pi/device

## Step 2 - Installation of git

```sh
sudo apt-get update && sudo apt-get install git -y
```

## Step 3 - Installation of KIAUH

The [github user dw-0](https://github.com/dw-0) created a set of scripts to get Klipper installed, called [KIAUH](https://github.com/dw-0/kiauh).

```sh
cd ~ && git clone https://github.com/dw-0/kiauh.git
```

## Step 4 - Adding of jpcurtis' repository to KIAUH

```sh
echo "https://github.com/Klipper3d/klipper" > ~/kiauh/klipper_repos.txt 

echo "https://github.com/jpcurti/ender3-v3-se-klipper-with-display" >> ~/kiauh/klipper_repos.txt
```

## Step 5.1 - Run KIAUH to install all the magic stuff

  *NOTE* - KIAUH expects you to enter the number / letter and confirm it with enter.

```sh
cd ~ && ./kiauh/kiauh.sh
```

## Step 5.2 - Change the repository

> **6** (Settings)  
**1** (Set custom Klipper repository)  
**1** (jpcurti/ender3-v3-se-klipper-with-display)  
**B** (Back)  
**B** (Back)  

## Step 5.3 - Install Klipper *(for the installation process just follow the on screen steps shown by KIAUH)*

> **1** (Install - you may need to enter the password for the current use)  
**1** (Klipper)  
**2** (Moonraker)  
**3** or **4** (Mainsail or Fluidd, whatever you prefer)  
**B** (Back)  
**Q** (Quit)

## Step 6 - Configuring the new printer firmware

```sh
cd ~/klipper
make menuconfig
```

![Demonstration image](images/klipper_make_menuconfig_serial_bridge.png)

With that tool you define what exactly should be compiled. So please do the following configuration:

> Micro-controller Architecture: `STMicroelectronics STM32`
> Processor model: `STM32F103`
> Bootloader offset: `28KiB bootloader`
> Communication interface: `Serial (on USART1 PA10/PA9)`
> Activate the point "`Enable extra low-level configuration options`"
> In the now expanded menu you have to activate "`Enable serial bridge`" and "`USART2`"

And leave `menuconfig` by pressing "Q" and save the just made configuration.

## Step 7. Compiling and installing the new printer firmware

```sh
make
```

The `make` command starts the compiler. It may take a minute or two to complete it.

The compiled firmware is saved as `~/klipper/out/klipper.bin`

**TODO**: Add instructions here to help those unfamiliar with Linux copy the file onto an SD card.  

Copy this bin file to an empty (FAT32, 4096 assoc) SD card, and plug it into the powered off printer. Switch the printer on and wait for two minutes.

**NOTE**: if the old Marlin GUI is shown on the display something went wrong. Try to rename the firmware file to f.e. firmw.bin (or any other max. 8.3 filename which is different to the last flashed firmware file name.

## Step 8. Your printer is now running Klipper but is not configured
