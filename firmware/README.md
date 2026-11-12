# AERIX Core firmware

Start with one simple test: blink `LED1` or `LED2`.

This confirms power, SWD, reset, the clock, GPIO, and the firmware toolchain
before adding drivers.

## Bring-up

1. Create an STM32H743IIKx project with STM32CubeMX, STM32CubeIDE, or your
   preferred toolchain.
2. Configure the GPIO connected to `LED1` or `LED2` as a push-pull output.
3. Build and flash over SWD.
4. Toggle the LED once per second.
5. Add logging, storage, sensors, and CAN one at a time.

Use the schematic or CubeMX pinout for the exact LED GPIO. Do not guess it
from the LED reference name.

Hardware references:

* [MCU schematic](../hardware/core/mcu.kicad_sch)
* [Main project](../hardware/core/core.kicad_pro)
* SWD nets: `SWDIO`, `SWCLK`, `RESET`, `VTREF`, `GND`

The firmware build system has not been added yet.
