# Messing around with a Cisco WAP150

These access points are pretty cheap nowadays as they are getting EoL'd by Cisco. 802.11ac + PoE make them a good candidate for modern home wifi.

## Teardown instructions

Pull the power button cap. Unscrew the four PH1 screws hidden under the rubber feets. Pry apart the top cover (held in place by plastic clips).

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

Most UART adapters have some sort of pull-up behavior on their RX input, which prevents the device from booting. Soldering a 1k resistor to ground solves the issue.

## Boot log

[Available here](boot.log).

## Bootloader

Unlocked, press any key to get a prompt:

```
CFE> help
Available commands:

button_test         Test button
ledctl              Test LED
nvram               NVRAM utility.
reboot              Reboot.
set console         Change the active console device
loop                Loop a command
flash               Update a flash memory device
memtest             Test memory.
f                   Fill contents of memory.
e                   Modify contents of memory.
d                   Dump memory.
u                   Disassemble instructions.
batch               Load a batch file into memory and execute it
go                  Verify and boot OS image.
boot                Load an executable file into memory and execute it
load                Load an executable file into memory without executing it
save                Save a region of memory to a remote file via TFTP
ping                Ping a remote IP host.
arp                 Display or modify the ARP Table
ifconfig            Configure the Ethernet interface
show clocks         Show current values of the clocks.
show heap           Display information about CFE's heap
show memory         Display the system physical memory map.
show devices        Display information about the installed devices.
unsetenv            Delete an environment variable.
printenv            Display the environment variables
setenv              Set an environment variable.
help                Obtain help for CFE commands

For more information about a command, enter 'help command-name'
*** command status = 0
```

### ledctl

* `ledctl 0`: turns off all LED
* `ledctl 1`: turns on green (main) LED
* `ledctl 2`: turns on blue (main) LED
* `ledctl 3`: turns on red (main) LED

## Open source

* Sep 21: Source request sent to Cisco, following the instructions in https://www.cisco.com/c/dam/en/us/td/docs/wireless/access_point/csbap/wap150_361/OSD/Cisco_WAP150_WAP361_1_1_0.pdf
