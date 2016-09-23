# Setup
These setup guides are intended to outline the process of installing the latest software on the WiFi Pineapple. Setup may be completed from any modern operating system with Internet access and a web browser (since you're reading this, it's safe to assume you have both).

The basic setup process is to download the latest firmware, connect the WiFi Pineapple to the host device, browse to the WiFi Pineapple web interface from the host device and follow the on-screen instructions to complete the firmware flashing process. For convenience, instructions and videos are provided for for common operating systems.

## Initial Setup Security

For security purposes, during the setup process you will be prompted to press the reset button. We recommend performing the setup with the WiFi Pineapple radios disabled.

If you are not connected to the WiFi Pineapple over WiFi for initial setup, you are requested to press the reset button momentarily to disable the radios.

If you must proceed with initial setup over WiFi, you will be requested to hold the reset button for 3 or more seconds to continue. 

The Reset button is located on the underside of the WiFi Pineapple NANO and on the back of the WiFi Pineapple TETRA.

## WiFi Pineapple NANO

We advise connecting the WiFi Pineapple NANO to a stable USB power supply capable of providing 9W for initial setup. When connecting to a PC, use the included USB Y cable. This setup process will require 5-10 minutes. Video tutorials for setup can be found from https://www.wifipineapple.com/pages/setup

### Android

1. Download the latest WiFi Pineapple NANO firmware
    https://www.wifipineapple.com/downloads
2. Install the WiFi Pineapple Connector app for Android
    https://play.google.com/store/apps/details?id=org.hak5.pineappleconnector
3. Power on the NANO using the supplied USB Y cable
4. Connect the NANO to the Android with a USB data cable
5. Open the WiFi Pineapple Connector Android app
6. Tap to configure USB Tethering, then tap back to return to the connector
7. When prompted, tap Begin Setup to launch the NANO setup page.
8. Follow the onscreen instructions to complete setup

### Windows / Linux

1. Download the latest WiFi Pineapple NANO firmware
    https://www.wifipineapple.com/downloads
2. Plug the NANO into your computer using the included USB Y cable
3. Browse to http://172.16.42.1:1471
4. Follow the onscreen instructions to complete setup

### MacOS

1. Download the latest WiFi Pineapple NANO firmware  
    [https://www.wifipineapple.com/downloads](https://www.wifipineapple.com/downloads)
2. Plug the NANO into your computer using the included USB Y cable
3. Open System Preferences -> Sharing and enable Internet Sharing
4. Once the blue LED on top of the NANO has stopped flashing, open Network Settings and connect to the new Wifi access point that is created by the NANO.  The naming convention is *Pineapple_NNNN*, where NNNN is from the MAC address printed on the bottom of the device.
5. Browse to [http://172.16.42.1:1471/](http://172.16.42.1:1471/)
6. Follow the onscreen instructions to complete setup
7. Once your initial setup is complete, reconnect to the NANO's access point.
8. Open a new Terminal window and connect to the NANO via SSH  
    `ssh root@172.16.42.1`
9. Configure the IP address  
    `uci set network.lan.ipaddr='192.168.2.10'`
10. Configure the Gateway  
    `uci set network.lan.gateway='192.168.2.1'`
12. Save the configuration and reboot  
    `uci commit && reboot`

You should now be able to access the Wifi Pineapple NANO GUI without connecting to its own access point by navigating to [http://192.168.2.10:1471/](http://192.168.2.10:1471/)

If you receive an error when attemtping to connect to the NANO over SSH (step 8) you may need to remove the existing SSH key from your *known_hosts* file which can be done with this command  
    `ssh-keygen -R 172.16.42.1`

## WiFi Pineapple TETRA

We advise connecting the WiFi Pineapple TETRA to a stable power supply capable of providing 18W for initial setup. When connecting to a PC, use the included USB Y cable. This setup process will require approximately 5 minutes. Video tutorials for setup can be found from https://www.wifipineapple.com/pages/setup

### Android

1. Download the latest WiFi Pineapple TETRA firmware
    https://www.wifipineapple.com/downloads
2. Install the WiFi Pineapple Connector app for Android
    https://play.google.com/store/apps/details?id=org.hak5.pineappleconnector
3. Power on the TETRA using the supplied USB Y cable
4. Connect the TETRA to the Android with a USB data cable
5. Open the WiFi Pineapple Connector Android app
6. Tap to configure USB Tethering, then tap back to return to the connector
7. When prompted, tap Begin Setup to launch the TETRA setup page.
8. Follow the onscreen instructions to complete setup

### Windows / Linux

1. Download the latest WiFi Pineapple TETRA firmware
    https://www.wifipineapple.com/downloads
2. Plug the TETRA into your computer using the included USB Y cable
3. Browse to http://172.16.42.1:1471
4. Follow the onscreen instructions to complete setup

