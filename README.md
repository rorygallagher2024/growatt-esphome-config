# Growatt ESPHome Configuration

Optimized ESPHome firmware for Growatt MIN 3600TL-X inverter with ShineWifi-X dongle.

## Why This Config?

This is a stripped-down, stable configuration that can be used with the ESP8266 in the ShineWifi-X.

Based on the excellent work by [pvprodk/GrowattESPHome](https://github.com/pvprodk/GrowattESPHome), with the following optimizations:
- Removed Web server
- Removed API encryption  
- Uses minimal sensor set for single-phase inverter (Like MIN 3600TL-X)
- Disables wifi power saving for stability

## Hardware Requirements

- Growatt MIN 3600TL-X (or similar single-phase inverter)
- ShineWifi-X USB dongle
- USB-to-TTL adapter (3.3V only)

## Installation

1. Clone or download `growatt.yaml`
2. Update WiFi credentials (lines 24-25)
3. Flash using ESPHome: `esphome run growatt.yaml`

## Compatibility

Tested on:
- Growatt MIN 3600TL-X
- ShineWifi-X

May work on other single-phase Growatt inverters with minor modifications.

## Credits
- [pvprodk/GrowattESPHome](https://github.com/pvprodk/GrowattESPHome)

## License
MIT
