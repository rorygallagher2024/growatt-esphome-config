# Growatt ESPHome Configuration

Optimized ESPHome firmware for Growatt MIN 3600TL-X inverter with ShineWifi-X dongle.

## Why This Config?

This is a stripped-down, stable configuration that can be used with the ESP8266 in the ShineWifi-X.

Based on the excellent work by [pvprodk/GrowattESPHome](https://github.com/pvprodk/GrowattESPHome), with the following optimizations:
- **No web server** - Saves ~15KB RAM
- **No API encryption** - Saves additional RAM overhead
- **Single-phase sensors only** - Removes 3-phase support not needed for most residential inverters
- **WiFi power saving disabled** - For connection stability

## Hardware Requirements

- Growatt MIN 3600TL-X (or similar single-phase inverter)
- ShineWifi-X USB dongle
- USB-to-TTL adapter (3.3V only)

## Features

**Monitored values (15-second updates):**
- PV voltage, current, and power
- Grid voltage, current, frequency
- Active power output
- Today's generation
- Total lifetime generation
- Inverter temperature
- Status and fault codes

**Diagnostic info:**
- WiFi signal strength
- IP address
- Uptime
- ESPHome version

## Configuration Details

### Update Intervals
```yaml
modbus_update_interval: 15s        # Main sensor polling
skip_updates_slow: "6"              # Slow sensors update every 90s (15s × 6)
```

Adjust these values based on your needs:
- **Faster updates (10s):** More responsive
- **Slower updates (30s):** Less network traffic, adequate for most automations

### Sensor Customization

The configuration includes sensors for single-phase inverters. If you have a 3-phase system, you'll need to add Phase B and Phase C sensors following the pattern of Phase A sensors (addresses documented in the [pvprodk/GrowattESPHome](https://github.com/pvprodk/GrowattESPHome) repository).

To add/remove sensors, modify the `sensor:` section. Each sensor definition includes:
- Modbus register address
- Data type and scaling factor
- Home Assistant integration metadata

### Modbus Register Map

This configuration uses standard Growatt Modbus registers:
- `0`: Status code
- `3-5`: PV1 voltage/current/power
- `35`: Grid active power
- `37-39`: Grid frequency/voltage/current
- `53`: Today's generation
- `55`: Total energy production
- `93`: Inverter temperature
- `105`: Fault code

## Installation

1. Clone or download `growatt.yaml`
2. Update WiFi credentials (lines 24-25)
3. Flash using ESPHome: `esphome run growatt.yaml`

## Home Assistant Integration

Once flashed and connected, the device will auto-discover in Home Assistant via the ESPHome integration.

**To add manually:**
1. Configuration → Integrations → Add Integration
2. Search for "ESPHome"
3. Enter hostname: `growatt.local`

## Compatibility

Tested on:
- Growatt MIN 3600TL-X (single-phase inverter)
- ShineWifi-X USB dongle (ESP8266-based)

May work on other single-phase Growatt inverters with minor modifications.

## Credits
- [pvprodk/GrowattESPHome](https://github.com/pvprodk/GrowattESPHome)

## Related Resources
- [Detailed blog post about the flashing process](https://medium.com/@rorygallagher2010/flashing-a-growatt-shinewifi-x-replacing-cloud-firmware-with-esphome-for-local-solar-monitoring-99cacaa910f0)
- [Official ESPHome documentation](https://esphome.io/)
- [Alternative Growatt integration methods](https://www.splitbrain.org/blog/2023-11/03-growatt_and_home_assistant)

## License
MIT
