# Troubleshooting

## LED Status Indicators

**WiFi Pineapple NANO **
The single blue LED indicates bootup and WiFi operation. While starting up, the LED will flash. Once bootup has completed the LED will become solid. The LED will flicker to indicate activity on the first WiFi radio - wlan0. This radio is host to the Access Point.

**WiFi Pineapple TETRA**
The yellow LED indicates activity on the WAN eth0 RJ45 Ethernet port. The blue LED indicates activity on the wlan0 wireless interface, home to the access point. The red LED indicates activity on the wlan1mon wireless interface, used by PineAP and other applications for sniffing and injection.

The boot sequence is: yellow solid followed by a moment of no LED activity, then blue blinking until bootup is complete.

## Factory Reset

Settings may be restored to defaults using the factory reset procedure. This process will restore the device to the initial configuration of the latest installed firmware. Upon performing the factory reset procedure initial setup must be performed, setting the root password and SSID.

To perform a factory reset from a fully booted WiFi Pineapple, hold the RESET button for approximately 7 seconds. The device will then reboot.

Alternatively the factory reset may be performed from the web interface. From the Configuration page, select Factory Reset from the General menu.

Note: data not stored on external media (USB / SD) will be erased during this process.

## Firmware Recovery

The WiFi Pineapple features a firmware recovery option which allows the user to restore the device to a factory firmware image. This procedure is performed via a special web interface.
Begin by downloading the factory firmware image for your device from https://www.wifipineapple.com/pages/faq

Next, follow these steps to access the recovery web interface and update the firmware.

* Unplug the WiFi Pineapple completely from all power sources.
* Begin holding the RESET button on the device.
* With the RESET button held, power on the device.
* Continue holding the RESET button for 10 seconds, then release.

> NANO: The blue LED will remain solid
> TETRA: The yellow LED will remain solid

* Connect the host PC to the WiFi Pineapple via the USB Ethernet Port

> NANO: The male USB A plug
> TETRA: The Micro USB port labeled ETH

* From the host PC, configure a static IP address on the WiFi Pineapple facing Ethernet interface to 192.168.1.2 with netmask 255.255.255.0

> For example, in Linux run ifconfig eth1 192.168.1.1 netmask 255.255.255.0 up (where eth1 is the interface name of the WiFi Pineapple).

* From the host PC, browse to http://192.168.1.1
* Click Choose File and select the factory firmware image downloaded above.
* Click Update Firmware.
* This process will take several minutes. Do not interrupt the power supply while the firmware is updating. Once complete, the WiFi Pineapple will restart.
* Reset the the WiFi Pineapple facing USB Ethernet interface back to DHCP or 172.16.42.42 with netmask 255.255.255.0

## Community Support

The WiFi Pineapple is more than hardware or software -- it's home to a helpful community of creative penetration testers and IT professionals. Welcome!

The forums are a great place to share feedback and ideas. You'll also find community support and discussion as well as modules, tutorials and firmware releases. Be sure to use the search feature to find answers to common questions. https://www.wifipineapple.com/forum

Find a bug? If it hasn't already been reported, you're encouraged to report it along with detailed steps to reproduce the issue at the bug tracker. https://www.wifipineapple.com/bugs

Looking for something a little more informal? The IRC channel is home to a passionate group of WiFi Pineapple enthusiasts. Join us at #pineapple on irc.hak5.org.

Please be aware that views expressed by community members are not those of Hak5 or the WiFi Pineapple team.