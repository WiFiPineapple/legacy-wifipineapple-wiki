# Firmware

## Overview

The WiFi Pineapples firmware is a highly modified version of OpenWRT packed with the WiFi Pineapples WebUI, as well as tools to aid your pentesting such as DNSSpoof, URLSnarf, Karma, nmap, mdk3 and much more.

## Downloads

Download can be found here: https://wifipineapple.com/?downloads

## Upgrading the WiFi Pineapple MKV

### Web-Interface updates

With our new Web-Interface, updating individual components is easy. Simply head over to your WiFi Pineapple MKV Infusion Bar. From there, you will not only be able to download, update or remove user created infusions, but also update system infusions - if available. Simply check for updates from either the small tile or the appropriate tab in the large tile. If there is an update available, you can update with just one click!

### Firmware updates

To upgrade or re-flash your firmware, navigate to the "WiFi Pineapple MK5" tile on the pineapple's Web-Interface. Once an upgrade is available, you will be able to select, download and install it all over the air.

## Upgrading manually
In case you want to upgrade manually or are having issues with the webinterface, simply follow these steps.

  1. Download the firmware from this website. Call it something like upgrade.bin.
  2. SCP the downloaded .bin file to your pineapple's `/tmp/` directory.
  3. Run the md5sum command on the uploaded .bin file and make sure it matches the one from the downloads page.
  4. If the MD5 sum matches, execute `sysupgrade -n -v /tmp/upgrade.bin`
  5. Wait for the reboot.

**Once done, you may now proceed with the initial WiFi Pineapple setup.**

## Unbricking a bricked WiFi Pineapple MKV

Bricked your WiFi Pineapple MKV? Unbricking is easy and doesn't require any extra hardware!

  1. Download the [special factory image](https://www.wifipineapple.com/mk5/factory.bin). This image is the WiFi Pineapple MKV's 2.0.4 firmware, packaged differently to allow unbricking. Please verify it's md5 checksum to be **8f684011ad40ca601cf159cd3381f7e0**.
  2. Power off your WiFi Pineapple MKV and set the DIP switches to up, up, up, up, down (from left to right).
  3. Connect to your WiFi Pineapple MKV via ethernet and set your network interface to a static IP of 192.168.1.2
  4. Boot up the WiFi Pineapple MKV. After around five seconds, you can navigate to http://192.168.1.1
  5. Upload the factory-1.2.0.bin file through the interface. Wait for it to complete.
  6. Set all the DIP switches back to the default configuration up, up, up, up, up (from left to right).
  7. Make sure the SD card is inserted and powercycle the WiFi Pineapple MKV. Your device will now boot the 1.2.0 firmware. Please wait patiently and refer to the first boot instructions in your WiFi Pineapple MKV instructions. You may skip any information relating to the stager.

**You are done. Enjoy your freshly flashed WiFi Pineapple MKV!**
