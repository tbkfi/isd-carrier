# ISD-CARRIER Prototype PCB

This repository contains a schematic and pcb design for an international sensor development project between Metropolia UAS and Osnabrück Hochschule.

![ISD Carrier Prototype PCB Render](/output/v0.1/render.png)

## Features

![Physical ISD Carrier Prototype PCB](/prototype.png)

The main system power is boosted from the available inputs to 5V, and fed into the MCU module and 5V peripherals. The MCU modules have LDOs that are taken advantage of for the 3V3 peripheral power.
- Sockets for: BlackIoT Polverine, DFR1117
- Unified PWR switch on-pcb
- LiPo protection circuit
- LiPo charging circuit with power path management
- 3V3 output header (extra, just in-case)	
- Multiple power inputs (populate PCB as needed):
	- JST(2.0mm): LiPo battery
	- JST(2.0mm): Photovoltaic panel (8-28V)
	- Header(2.54mm): E.g. Bench-top power supply
    - PCB USB-C (charging, 5V peripherals, main power)
	- MCU module USB-C (no 5V peripherals, no charging!)
- Sensor support (same for Polverine & DFR1117):
	- BME690 via I2C (LGA, integrated)
	- BMV080 via I2C (ZIF-connector, integrated)
	- Seeed E5 LoRa via UART (Grove)
	- SPS30 via I2C (ZHR-5, 5V)
	- I2C (Grove, 3V3)
	- SPI (Header: CS, MISO, MOSI, SCK, GND)

## Documentation

See the repository directory labeled 'output' for the board revision files. The directory contains schematic (pdf), routing (png), and an interactive bill of materials (bom).

![ISD Carrier Prototype PCB Schematic](/output/v0.1/isd-board-dual-socket.pdf)
![ISD Carrier Prototype PCB Routing](/output/v0.1/isd-board-dual-socket.png)

### Issues

The following headings contain discovered issues for revisions, both in schematic and
practical problems when building the board(s).

### version 0.1
- ZIF-connector: Insertion direction is reversed, making it unusable. Neccessitates the use of Polverine for BMV080.
- Power Path: Ordered FET(P) was not the one in BOM, and had differing package. Soldering was still possible at 45deg angle, and bending unneeded pins above the package.
- DW01A: Behaviour is erratic, despite following datasheet application diagram. Can be worked around by powering load from external input, and only connecting the battery afterwards.

