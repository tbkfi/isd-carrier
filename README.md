# Prototype PCB for International Sensor Development Project

This repository contains a schematic and pcb design for an international sensor development project between Metropolia UAS and Osnabrück Hochschule, which concluded on 2026.02.27.

![ISD Carrier Prototype PCB Render](/output/v0.1/render.png)

## Board Features

The PCB provides 5V power to the MCU modules, which have built-in LDOs to provide 3V3 power
for external and integrated peripherals.

- Interleaved dual socket (BlackIoT Polverine and DFR1117)
- Built-in power switch (external reset/power button)
- LiPo protection circuit (2.4-4.2V)
- LiPo charging circuit (configurable output)
- Power Path management using P-FET, actuated by external power voltage to disconnect battery from load during charging.
- Auxiliary 3V3 output pin header.
- Multiple power input options (all selectively populatable):
	- JST(2.0mm): LiPo battery
	- JST(2.0mm): Photovoltaic panel (8-28V)
	- Header(2.54mm): E.g. Bench-top power supply
    - PCB USB-C (charging, 5V peripherals, main power)
	- (MCU module USB-C (no 5V peripherals, no charging!))
- Sensor support (for both Polverine & DFR1117):
	- BME690 via I2C (integrated, LGA, 3V3)
	- BMV080 via I2C (integrated, ZIF-connector, 3V3)*
	- Seeed E5 LoRa via UART (external, Grove, 3V3)
	- SPS30 via I2C (external, ZHR-5, 5V)
	- I2C (external, Grove, 3V3)
	- SPI (Header: CS, MISO, MOSI, SCK, GND)

## Documentation

See the repository directory labeled 'output' for the board revision files. The directory contains schematic (pdf), routing (png), and an interactive bill of materials (bom).

![ISD Carrier Prototype PCB Schematic](/output/v0.1/isd-board-dual-socket.pdf)

![ISD Carrier Prototype PCB Routing](/output/v0.1/isd-board-dual-socket.png)

### Issues

![Physical ISD Carrier Prototype PCB](/prototype.png)

This section contains issues encountered up to and during the final integration testing when using
this board with all the external peripherals. Some issues are PCB related, others are practical inefficiencies or overlooked details.

### version 0.1
1. ZIF-connector: Insertion direction is reversed. Causing the pin-direction to be flipped, making the connector unusable. Neccessitates the use of Polverine for BMV080 functionality.
2. Power Path: P-FET which was ordered had differing package type from original. Soldering was still possible at 45deg angle, and bending unneeded pins above the package to avoid shorts.
3. DW01A: Behaviour was unexpected during testing despite following datasheet application diagram in design. Couple workarounds were found, but ultimately the IC should be replaced in the design
with something more robust from TI or Microchip (E.g.) to increase reliability and control over the protection circuit.
4. Peripheral cabling: Operation was susceptible to jumpers, badly crimped or soldered cables, which caused unnecessary debugging and inconsistent results.
5. Prototype PCB count: Not enough prototypes were made to provide such large teams with an efficient number of PCBs while continuing to validate power management behaviour.
As LoRa and Sensor teams received one prototype, and found them to be in working condition, it became virtually impossible to get either of them back for more power-related validation. 
6. It's a good idea to validate the MCU modules and cabling that is in use by other teams, specially if they were made or modified by them, as on more than one ocassion incorrectly (or not at all)
soldered pin headers caused certain functionality to not work, as nothing was plugged in...
7. I2C Pull-ups: Existing 10k pulls caused issues with DFR1117, while the configuration worked with Polverine. The pull-ups on PCB were removed to fix the issue. Though it's possible
this issue was due to bad cabling or bad sensor, as the pull-ups shouldn't technically cause this kind of issue in this configuration.
