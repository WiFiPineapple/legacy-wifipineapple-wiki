# Hardware

The WiFi Pineapple hardware is a purpose built wireless auditing platform, combining versatile and convenient components to address the needs of the penetration tester. Please familiarize yourself with the WiFi Pineapple layout and specifications.

## WiFi Pineapple NANO

The ultimate WiFi pentest companion, in your pocket.

### Specifications

* CPU: 400 MHz MIPS Atheros AR9331 SoC
* Memory: 64 MB DDR2 RAM
* Disk: 16 MB ROM + Micro SD (not included. up to 200GB)
* Wireless: Atheros AR9331 (wlan0) + Atheros AR9271 (wlan1), both IEEE 802.11 b/g/n
* Ports: (2) RP-SMA Antenna, Ethernet over USB (ASIX AX88772A)
* USB 2.0 Host, Micro SD card reader
* Power: USB 5V 1.5A. Includes USB Y-Cable
* Configurable Status Indicator LED
* Configurable Reset Button

### Power Considerations

The WiFi Pineapple NANO requires 9W for stable operation under high load. This figure accounts for a 2.5W USB accessory in addition to maximum utilization of the CPU, SD card and radios. Power is provided from the male USB type A plug. A USB Y cable is provided with the WiFi Pineapple NANO.


## WiFi Pineapple TETRA

The amplified, dual-band (2.4/5 GHz) powerhouse.

### Specifications

* CPU: 533 MHz MIPS 74K Atheros AR9344 SoC
* Memory: 64 MB DDR2 RAM
* Disk: 2 GB NAND Flash
* Wireless: Atheros AR9344 + Atheros AR9580, both IEEE 802.11 a/b/g/n with quad integrated skybridge amplifiers and included 5 dBi antenna for a high 29 dBm gain EIRP
* Ports: (4) SMA Antenna, RJ45 Fast Ethernet, Ethernet over USB, Serial over USB, USB 2.0 Host, 12V/2A DC Power
* Power: Requires 18W. Accepts power from any combination of sources; DC Barrel Port, USB ETH port, USB UART port. AC wall adapter for stationary deployment and USB Y cable for mobile deployment included.
* Configurable Status Indicator LED
* Configurable Reset Button


### Power Considerations

The WiFi Pineapple TETRA requires 18W for normal stable operation. While the device may function under minimal load with less power, system instability may occur during peak load.

Power may be provided to the device by any combination of USB UART, USB ETH, or 12V DC ports. The 12V DC port accepts a standard IEC 60130-10:1971 type A connector with 5.5 mm OD, 2.1 mm ID (center positive).

The UART and ETH ports on the WiFi Pineapple TETRA will accept power from combined USB sources, such as from computers, wall adapters or batteries via USB Y cables. There is no risk of providing too much power from standard 5 volt USB sources as the WiFi Pineapple TETRA will only draw as much amperage as needed.

Most modern computers are capable of providing the necessary amperage from their USB ports to power the WiFi Pineapple TETRA using two USB Y cables. Older computers and many netbooks however may not provide enough continuous current for stable operation.

When calculating total power in wattage, multiply the voltage and amperage. USB sources are always 5V and may vary in amperage depending on configuration. Many older USB 2.0 ports are limited to the 500mA specification while newer USB 3.0 ports can deliver 900mA and above. Typically notebook computers with USB charge ports (indicated in yellow, red or by lightning icon) will provide even higher amperage.