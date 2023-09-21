# Messing around with a Cisco WAP150

These access points are pretty cheap nowadays as they are getting EoL'd by Cisco. 802.11ac + PoE make them a good candidate for modern home wifi.

## Teardown instructions

Pull the power button cap. Unscrew the four PH0x screws hidden under the rubber feets. Pry apart the top cover (held in place by plastic clips).

## Under the hood

* SoC: Broadcom ARM 32-bits (needs confirmation of the part number)
* DRAM: 256MB
* NAND: 128MB (8-bit, TSOP48)
* Wi-Fi: BCM43227, BCM4360

## UART

A UART connector (0.1" header, named "J8") is already populated. Its pinout is the following:

1. GND (the closest pin to the "J8" label on the silkscreen)
2. RX (from router standpoint)
3. TX
4. 3V3

Most UART adapters have a pull-up resistor (internal or external) on their RX input, which causes some issues. A pull-down resistor should be added (I used a 1k5 resistor).

## Boot log

[Available here](boot.log).

## Open source

* Sep 21: Source request sent to Cisco, following the instructions in https://www.cisco.com/c/dam/en/us/td/docs/wireless/access_point/csbap/wap150_361/OSD/Cisco_WAP150_WAP361_1_1_0.pdf
