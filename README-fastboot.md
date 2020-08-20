This branch contains a ESP-IDF v3.3 build that has been optimized for boot performance.

**IMPORTANT:** I created this for my own projects and have not done any  testing
beyond that, nor can I provide support. If this causes your project to blow up on you:
bad luck, you are on your own.

# Speedup

I haven't done any accurate measurements, but on my WROVER-B module, bootup time goes
down to <100 milliseconds from almost two seconds.

# Changes

The following changes have been applied:

* Heap poisoning has been disabled in `sdkconfig`
* The bootloader has been modified to skip flash verification
* SPIRAM verification has been hacked away (there is no option for this in ESP-IDF v3.3)

The code changes can be found in `esp-idf-fastboot.diff`.

# Is this safe?

Skipping verification of flash and SPIRAM will cause the ESP to boot even if the flashed
image or the external RAM are faulty. Disabling heap poisoning will disable the detection
of heap corruption at runtime. The Arduino framework is forked and built from the master
branch and not from a stable release.

# Platform.io

You can use this version of the Arduino framework in Platform.io by adding this to your
`platformio.ini`:

```
platform_packages =
    framework-arduinoespressif32 @ https://github.com/DirtyHairy/arduino-esp32#master-fastboot
```

# Credits

Those changes were suggested by the Reddit user LinkeSeitentasche in his excellent
[guide](https://www.reddit.com/r/esp32/comments/fnj51a/a_guide_to_improving_esp32_boot_speed/)
on improving ESP32 bootup speed.
