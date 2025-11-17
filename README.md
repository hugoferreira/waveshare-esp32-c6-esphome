# ESP32-C6 LCD Demo

This repository contains an esphome configuration for the Waveshare ESP32-C6-LCD-1.47 board. It demonstrates using LVGL with the onboard 1.47" ST7789V display and exposes the board backlight and onboard RGB LED.

Official board page: https://www.waveshare.com/wiki/ESP32-C6-LCD-1.47#Overview

**NOTE: This was last tested with ESPHOME v2025.10.5.** No guarantee it will work with other versions of ESPHome (PRs are welcomed, though). 

## What’s included

- Firmware configuration: [`esphome/test.yaml`](esphome/test.yaml)
- Display configuration: the MIPI-SPI ST7789V display is defined as [`main_display`](esphome/test.yaml).
- LVGL UI: a simple page with a label defined as [`main_page`] and widget in [`esphome/test.yaml`](esphome/test.yaml).
- Backlight output: [`lcd_backlight`](esphome/test.yaml) (controlled via LEDC on GPIO22).
- Status LED: [`status_led`](esphome/test.yaml) (an ESP32 RMT WS2812 strip on GPIO8).

## Homeassistant

Both the backlight and well as the status led are controllable from HomeAssistant.

Referenced symbols in this repo:
- [`esphome` config root](esphome/test.yaml)
- [`lvgl` section](esphome/test.yaml)
- [`main_display`](esphome/test.yaml)
- [`lcd_backlight`](esphome/test.yaml)
- [`status_led`](esphome/test.yaml)

## Quick usage (esphome)

0. Create your own `secrets.yaml`, with three keys: `wifi_ssid`, `wifi_password` and `ota_password`; 
1. Install esphome (pip or Docker), then run from the repository root `esphome compile test.yaml`;
2. Connect the board via USB and follow the prompts from `esphome run test.yaml` to (re-)compile, upload, and monitor logs.

Notes:
- Display pins, buffer size and LVGL settings are tuned for the Waveshare 1.47" (172x320) panel. See the [official board page](https://www.waveshare.com/wiki/ESP32-C6-LCD-1.47#Overview) for hardware details, and check [the official schematics](esphome/ESP32-C6-LCD-1.47_schemetics).

## TODO
- [ ] Add more examples leveraging LVGL
- [ ] If possible add examples unique to C6, like Thread/Zigbee/?
- [ ] Expose the user switch
