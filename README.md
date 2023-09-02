# arduino-interfaces
Code and wiring for interfaces between small, "Arduino"-like microprocessors


## Controlling a 5V device with a 3.3V processor
e.g. Using an ESP32 to control a WS2812B LED strip

Use <a href="https://www.ti.com/lit/ds/symlink/sn74hct125.pdf">74HCT125</a> (4-channel buffer/line-driver, individually-enabled) or <a href="https://www.ti.com/lit/ds/symlink/sn74hct245.pdf">74HCT245</a> (8-channel transceiver) 

> **IMPORTANT!** Note the "T" in the name - 74HC**T**125 and 74HC**T**245 - this indicates that these chips use TTL-level input. Do not confuse them with their 74HC125 and 74HC245 equivalents which use CMOS-level input.

These chips are 5V CMOS devices but have TTL-compatible inputs. That means that they are supplied with 5V (at the `VCC` pin), and also output 5V (at the the `Y`(74HCT125) / `B`(74HCT245) pins), but they will interpret any input at >2.0V as a logical `HIGH`.
This makes them ideal for receiving an input from a 3.3V MCU such as a Raspberry Pi or ESP8266/ESP32.

- The 74HCT125 allows lines to be individually enabled, whereas all channels on the 74HCT245 are enabled/disabled fromna single OE pin.
- The 74HCT125 is unidirectional - input on A pin always activates output on corresponding Y pin. The 74HCT245 allows transmission either from A to B, or from B to A (selectable via DIR pin))
- Tie unused inputs to `GND`
- As per <a href="https://www.ti.com/lit/ds/symlink/sn74hct245.pdf">10. Power Supply Recommendations</a>, place a 0.1μF and a 1μF capacitors in parallel across `VCC` and `GND` as close to the power pin as possible.
