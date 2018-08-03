# PicoPrint

PicoPrint is a 32-bit 3D printer control board, designed to be fast, quiet, and compact.

PicoPrint is still in active development, and some specifications are not yet finalised. Once the design has been finalised, this page will be updated with detailed information.

## Specifications
* 32-bit STM32F446VET6 Microcontroller
  * 180MHz core clock speed
  * 512kB Flash Memory
    * 16kB Bootloader + 32kB EEPROM Emulation = 464kB Available
  * 128kB SRAM
  * Floating Point Unit
* 5 x TMC2130 Stepper Drivers
  * STEP/DIR for motion + SPI bus for configuration
  * StealthChop for quiet printing
  * StallGuard signal wired to endstop inputs for sensorless homing (enabled by jumper)
* 1 x 20A MOSFET for Heated Bed
  * Low RDSon MOSFET for minimum heat dissipation
  * MOSFET driver IC for improved PWM performance
* 2 x 5A MOSFETs for Heater Cartridges
  * Accessible via screw terminal or pin header for pluggable cables
* 3 x 3A MOSFETs for Fans and Lighting
  * Suppresion diodes for flyback protection
  * Accessible via screw terminal (F0 & F1) or pin header (F0, F1 & F2)
* 12-24V Compatibility
  * Maximum 30V on main power rail
  * Maximum 40V on bed power rail
* Internal 5V 2A High-Efficiency Buck Regulator
  * Synchronous regulator for maximum efficiency
  * Up to 2A current draw
    * 200mA required for PicoPrint, 1.8A remaining for peripherals
    * Sufficient for most external LCDs, RC servo motors, or single-board computers (Raspberry Pi and similar)
* 4 x Thermistor Inputs
  * 2 HotEnds, 1 Bed + 1 Chamber/Spare
* 4 x Endstop Inputs
  * Jumper allows selection of either external endstop or TMC2130 StallGuard for sensorless homing for each endstop
* 1 x Z-Probe Connector
  * Includes 1 Interrupt-capable pin and one ADC-capable pin
* Rugged Design for Maximum Reliability
  * Power Rail Protection
    * Main power input is protected against reverse-polarity by P-Ch MOSFET
      * No fuse to replace if wiring is reversed
      * Red LED indicates reversed power polarity
    * 5V from USB is fused (200mA self-resetting PTC) to protect host device
    * 5V Buck Regulator implements overcurrent, overtemperature, and short-circuit protection
    * 3.3V Linear Regulator implements overcurrent and overtemperature protection
    * Power rail to endstops and z-probe is fused (200mA self-resetting PTC)
    * Main power input can be monitored by ADC channel to measure input voltage (firmware dependent)
  * Microcontroller Pin Protection
    * Dedicated ESD-protection IC on USB interface
    * Thermistors + Endstops + Z-Probe protected against accidental connection to ±30V by diode clipping circuit
      * Endstops are safe to use with 5/12/24V signals if desired
  
  
 
  



## Firmware
PicoPrint is designed to run the Marlin 3D printer firmware. A version of Marlin currently running on PicoPrint can be found [here](https://github.com/Aus3D/Marlin/tree/bugfix-2.0.x-F446-PicoPrint).

Compiling and uploading the Marlin firmware will require the Arduino IDE, and a fork of the STM32Generic Hardware Core, [here](https://github.com/chrissbarr/STM32GENERIC/tree/F446VE).
