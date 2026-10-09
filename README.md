# water-pressure-firmware

OTA firmware for the WRA water pressure sensor fleet (FireBeetle 2 ESP32-C5 IO Expansion Kit + DFRobot SEN0257, reporting to Adafruit IO).

Binaries contain no credentials. Device identity, Wi-Fi and Adafruit IO credentials and calibration live in each board's NVS and are provisioned over USB.

## Current firmware

| Version | File | Size | SHA-256 |
|---|---|---|---|
| 8 | WaterPressureAIO-v8.bin | 1,214,848 bytes | db71df90449b891954830a8f3e5533166a02c6488721c98b6564d3c24986bd95 |
| 7 | WaterPressureAIO-v7.bin | 1,213,536 bytes | 1b31a451ec9149c3511f72b3f974121f017e26a07b7c2ae4212d1ce6fdd46607 |
| 6 | WaterPressureAIO-v6.bin | 1,213,600 bytes | 20fc7a1fd91fb5d66be22deddb9506738ed1de4e6ad7c30a47221136a4f9f600 |
| 5 | WaterPressureAIO-v5.bin | 1,190,240 bytes | 285d362e6c44f46b57bb837d6028b8898c7272d9ea8153bb40c68cf720e1444b |
| 4 | WaterPressureAIO-v4.bin | 1,190,032 bytes | 6bb4c3693c1eccd53bee4b1cd1ff71f25c0e725632e725f0a1020766253faf64 |
| 3 | WaterPressureAIO-v3.bin | 1,181,040 bytes | d0c3b8ceccac0a5e19e107077324820ae86af03c86ea278195ca85e5967ac8ab |
| 2 | WaterPressureAIO-v2.bin | 1,180,512 bytes | bd3b4b8f15f4ac9459e07b97268e9cd1df77f459b334f8059f9b3fc300cdcd07 |

Download URL used by the devices:
https://raw.githubusercontent.com/WRA-Architects/water-pressure-firmware/main/WaterPressureAIO-v8.bin  (older versions are kept beside it for rollback)

## How updates work

Devices check the shared Adafruit IO feed `firmware-version` once an hour. The feed holds `VERSION|URL|SHA256[|device-id,...]`. A device downloads the file when VERSION is higher than what it runs, verifies the SHA-256 while streaming into the spare OTA slot, and rolls back automatically if the new image fails to post three times.

## Publishing a new build

Build with `secrets.h` renamed off, confirm `strings WaterPressureAIO-vN.bin | grep -c aio_` prints 0, commit the file to `main`, then update the `firmware-version` feed (canary one device first).
