# WiFi Pineapple MKV

The WiFi Pineapple is a Wireless Pen-Test Drop Box, The current revision sports a 400Mhz Atheros AR9331 SoC, 16MB of ROM, 64MB of RAM and an onboard Realtek RTL8187L Chipset, as well as MicroSD card support and 5 [DIP Switches](dip_switches.md).


## Hardware

The Mark V's firmware is as follows:

- Atheros AR9331 SoC Radio -- Unlocked
- Realtek RTL8187L Radio -- Unlocked
- 16MB of ROM, 64MB of RAM
- Upto 32GB Of MicroSD Storage in EXT/FAT format
- 2x SMA Antenna ports, 1x USB, 1x Ethernet, Expansion Bus, TTL Serial
- Power LED, Ethernet LED, Wireless 1 LED, Wireless 2 LED
- DC in Variable 5-12v, ~1A, 5.5mm*2.1mm (Type M Barrel) connector, International Power Supply

## Software

The WiFi Pineapple firmware is a heavily modified version of OpenWRT, packed with tools to aid your pen testing such as Aircrack-NG, MDK3, SSLStrip, Reaver and many more. The firmware also packs the 'Tile' WebUI with 1.0.0+ that serves as a PHP-Based front end for your pineapple. For more information on the Web UI, please see [WebUI](webui.md).


### Connecting to the Pineapple

The WiFi Pineapple has 4 major interfaces for communicating over, wlan0, wlan1, eth0 and the [Serial UART](serial_uart.md) interface.


### Internet Connection Sharing

You can share internet from your desktop or laptops wireless over ethernet to your pineapple to download various Infusions or share internet to your clients. For in depth way to share the connection see the [Internet Connection Sharing](ics.md) guides

### Recovery

Please see the [Factory Reset page](reset.md).
