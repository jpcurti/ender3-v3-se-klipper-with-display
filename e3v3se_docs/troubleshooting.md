# Troubleshooting

## The firmware needs to be restarted every time is loses connection with the printer

Based on this [github comment](https://github.com/Klipper3d/klipper/issues/835#issuecomment-725046049)

```sh
sudo echo 'SUBSYSTEM=="usb", ATTRS{idVendor}=="1d50", ATTRS{idProduct}=="614e", ACTION=="add", RUN+="/bin/sh -c \'/usr/bin/systemctl restart klipper.service\'"' > /etc/udev/rules.d/98-klipper.rules
```

The raspberry pi will likely need to be restarted afterwards.

## Printer is not flashing the .bin built from source

Try renaming the file slightly differently.  It may take a few attempts before successful.

<!-- markdownlint-disable-next-line MD026 -->
## After installing this project my display went crazy!

Check if you installed the **E3V3SE display firmware 1.0.6** as mentioned in section [Before you begin - Important](#/install?id=before-you-begin-important)

## I found a bug in the GUI or something doesn't work as expected

Please [open an issue for bugs/feature requests](https://github.com/jpcurti/ender3-v3-se-klipper-with-display/issues) and make a question in the project [discussion](https://github.com/jpcurti/ender3-v3-se-klipper-with-display/discussions)
