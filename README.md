# water-pressure-firmware

OTA firmware for the WRA water pressure sensor fleet (FireBeetle 2 ESP32-C5 IO Expansion Kit + DFRobot SEN0257, reporting to Adafruit IO).

Binaries contain no credentials. Device identity, Wi-Fi and Adafruit IO credentials and calibration live in each board's NVS and are provisioned over USB.

## Current firmware

| Version | File | Size | SHA-256 |
|---|---|---|---|
| 2 | WaterPressureAIO-v2.bin | 1,180,512 bytes | bd3b4b8f15f4ac9459e07b97268e9cd1df77f459b334f8059f9b3fc300cdcd07 |

Download URL used by the devices:
https://raw.githubusercontent.com/WRA-Architects/water-pressure-firmware/main/WaterPressureAIO-v2.bin

## How updates work

Devices check the shared Adafruit IO feed `firmware-version` once an hour. The feed holds `VERSION|URL|SHA256[|device-id,...]`. A device downloads the file when VERSION is higher than what it runs, verifies the SHA-256 while streaming into the spare OTA slot, and rolls back automatically if the new image fails to post three times.

## Publishing a new build

Build with `secrets.h` renamed off, confirm `strings WaterPressureAIO-vN.bin | grep -c aio_` prints 0, commit the file to `main`, then update the `firmware-version` feed (canary one device first).
