# Firmware
This directory contains firmware source and binaries for the board. As of now, it only contains changes to RomWBW.

## RomWBW changes
These changes apply to RomWBW 3.1.1 (the current `dev` branch at time of writing). They were compared against RomWBW 3.1.1-pre.71 on 2021/04/19. The **.diff** files apply to files in `Source/HBIOS`, and the config **.asm** should be placed in `Source/HBIOS/Config`. A prebuilt ROM image is provided. To build this image under Windows, run `BuildShared`, then `BuildROM RCZ80 pd256 128` (both from `Source`).
