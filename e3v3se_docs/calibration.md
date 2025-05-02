# Calibration

## PRTOUCH_PROBE_ZOFFSET

New commands were added by 0xD34D to aid in calibrating the Ender 3 V3 SE Z-Offset (the difference in height between the nozzle and the PRTouch probe).

`PRTOUCH_PROBE_ZOFFSET` - This command determines the Z-Offset of the nozzle:

`PRTOUCH_ACCURACY SAMPLES=10 PROBE_SPEED=1` This command tests the Z-offset probe for 10 times and returns the statistics of the accuracy of the sensor:

Before you start printing and testing, place an old printbed (or anything else able to protect you current printbed) on the printer.

**Neither any of the developer nor I are responsible if you crash printhead into your bed.**

**NOTE:** - The following commands were added and can be called via the terminal (mainsail, fluidd or octoprint)

First start with determining the z_offset by launching

```txt
PRTOUCH_PROBE_ZOFFSET
```

Run this command several time and look if the values reported are feasible and relatively consistent.

Also run:

```txt
PRTOUCH_ACCURACY SAMPLES=10 PROBE_SPEED=1
```

The output should have a rather low range (remember a standard layer height is 0.2mm).

Once everything looks good, run:

```txt
PRTOUCH_PROBE_ZOFFSET APPLY_Z_ADJUST=1
```

 and save the config afterwards.

```txt
SAVE_CONFIG
```

Then run `PRTOUCH_PROBE_ZOFFSET` again, just to be sure. If everything looks rather stable, happy printing.

## Input shaping

[Follow the offical Klipper docs on 'Measuring Resonances'](https://github.com/Klipper3d/klipper/blob/master/docs/Measuring_Resonances.md)
