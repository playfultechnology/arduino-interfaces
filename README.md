# arduino-interfaces
Code and wiring for interfaces between small, "Arduino"-like microprocessors


## Controlling a 5V device with a 3.3V processor
e.g. Using an ESP32 to control a WS2812B LED strip

Use <a href="https://www.ti.com/lit/ds/symlink/sn74hct125.pdf">74HCT125</a> (4-channel, individually-enabled) or <a href="https://www.ti.com/lit/ds/symlink/sn74hct245.pdf">74HCT245</a> (8-channel, mass-enabled) 

> **IMPORTANT!** Note the "T" in the name - 74HC**T**125 and 74HC**T**245 - this indicates that these chips use TTL-level input. Do not confuse them with their 74HC125 and 74HC245 equivalents which use CMOS-level input.

These chips are 5V CMOS devices, but with TTL-compatible inputs. That means that they are supplied with 5V (at the ```VCC``` pin), and output 5V (at the the ```Y```(74HCT125) / ```B```(74HCT245) pins)  
- i.e. that is both the input voltage (on the VCC pin), and also the voltage output (on the Bx (74HCT245) or Yx (74HCT125) pins).
However, crucially, these "T" chips have TTL-compatible logic level inputs. 
