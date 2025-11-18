# ESP32-C6 LCD Demo

This repository contains an esphome configuration for the Waveshare ESP32-C6-LCD-1.47 board. It demonstrates using LVGL with the onboard 1.47" ST7789V display and exposes the board backlight and onboard RGB LED.

Official board page: https://www.waveshare.com/wiki/ESP32-C6-LCD-1.47#Overview

**NOTE: This was last tested with ESPHOME v2025.10.5.** No guarantee it will work with other versions of ESPHome (PRs are welcomed, though). 

## What’s included

- Base firmware configuration: [`esphome/test.yaml`](esphome/test.yaml)
- LVGL clock configuration: [`esphome/clock.yaml`](esphome/clock.yaml) – draws a digital clock, polls SNTP every second, and applies the themed colors from `substitutions`.
- Display configuration: the MIPI-SPI ST7789V display is defined as [`main_display`](esphome/test.yaml) / [`esphome/clock.yaml`](esphome/clock.yaml).
- Backlight output: [`lcd_backlight`](esphome/test.yaml) (controlled via LEDC on GPIO22).
- Status LED: [`status_led`](esphome/test.yaml) (an ESP32 RMT WS2812 strip on GPIO8).
- LVGL UI: simple demo widgets in [`esphome/widgets.yaml`](esphome/widgets.yaml) plus the clock face in [`esphome/clock.yaml`](esphome/clock.yaml).

## Homeassistant

Both the backlight and well as the status led are controllable from HomeAssistant.

Referenced symbols in this repo:
- [`esphome` config root](esphome/test.yaml) / [`clock variant`](esphome/clock.yaml)
- [`lvgl` section](esphome/test.yaml) / [`clock variant`](esphome/clock.yaml)
- [`main_display`](esphome/test.yaml)
- [`lcd_backlight`](esphome/test.yaml)
- [`status_led`](esphome/test.yaml)

## Clock example

The LVGL clock config (`esphome/clock.yaml`) shows how to:
- Keep the display backlight at 50 % using an `on_boot` action
- Sync time via SNTP and refresh an LVGL label every second with `lv_label_set_text`
- Theme the UI by swapping substitution-based color palettes

## Quick usage (esphome)

0. Create your own `secrets.yaml`, with three keys: `wifi_ssid`, `wifi_password` and `ota_password`; 
1. Install esphome (pip or Docker), then run from the repository root `esphome compile test.yaml`;
2. Connect the board via USB and follow the prompts from `esphome run test.yaml` to (re-)compile, upload, and monitor logs.

Notes:
- Display pins, buffer size and LVGL settings are tuned for the Waveshare 1.47" (172x320) panel. See the [official board page](https://www.waveshare.com/wiki/ESP32-C6-LCD-1.47#Overview) for hardware details, and check [the official schematics](ESP32-C6-LCD-1.47_schemetics.pdf).

## TODO
- [ ] Add more examples leveraging LVGL
- [ ] If possible add examples unique to C6, like Thread/Zigbee/?
- [ ] Expose the user switch
