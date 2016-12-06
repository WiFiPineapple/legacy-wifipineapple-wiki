# Firmware

## Overview

The WiFi Pineapples firmware is a highly modified version of OpenWRT packed with the WiFi Pineapples WebUI, as well as tools to aid your pentesting such as DNSSpoof, URLSnarf, Karma, nmap, mdk3 and many more.

## Downloads

Current and previous firmware incarnations can be found here: https://wifipineapple.com/?downloads

## Upgrading the WiFi Pineapple MKV

### Web-Interface Updates

With our new WebUI, updating individual components is easy. Simply head over to your WiFi Pineapple MKV Infusion Bar. From here, you can not only download, update and remove Infusions, but also update the core System Infusions. Just check for updates from either the small tile or the appropriate tab in the large tile. If there is an update available, you can download and apply it with just one click!

### Firmware updates

To upgrade or re-flash your firmware, navigate to the "WiFi Pineapple MK5" tile on the pineapple's WebUI. Once an upgrade is available, you will be able to download and install it over the air.

## Upgrading manually
In case you want to upgrade manually or are having issues with the WebUI, simply follow these steps.

  1. Download the firmware from [this](https://wifipineapple.com/?downloads) website. Call it something like upgrade.bin.
  2. SCP the downloaded .bin file to your pineapple's `/tmp/` directory.
  3. Run the md5sum command on the uploaded .bin file and make sure it matches the one from the downloads page. This ensures that there hasn't been any issues in transfering the file.
  4. If the MD5 sum matches, execute `sysupgrade -n -v /tmp/upgrade.bin`
  5. Wait for the reboot

  Note: It may take several minutes for your WiFi Pineapple to apply the update and restart.
  Please be patient and do **NOT** unplug the power until you are sure that your Pineapple has rebooted successfully.

**Once it has completed, you can now proceed with the WiFi Pineapple Initial Setup from the WebUI.**

## Unbricking a bricked WiFi Pineapple MKV

Bricked your WiFi Pineapple MKV? Unbricking is easy and doesn't require any extra hardware!

  1. Download the [special factory image](https://www.wifipineapple.com/mk5/factory.bin). This image is the WiFi Pineapple MKV's 2.4.0 firmware, packaged differently to allow unbricking. Please verify it's md5 checksum to be **96df5ccc388bd86b40a122c546adf687**.
  2. Power off your WiFi Pineapple MKV and set the DIP switches to up, up, up, up, down (from left to right).
  3. Connect to your WiFi Pineapple MKV via ethernet and set your network interface to a static IP of 192.168.1.2
  4. Boot up the WiFi Pineapple MKV. After around five seconds, you can navigate to http://192.168.1.1
  5. Upload the mk5_factory.bin file through the interface. Wait for it to complete.
  6. Set all the DIP switches back to the default configuration up, up, up, up, up (from left to right).
  7. Make sure the SD card is inserted and powercycle the WiFi Pineapple MKV. Your device will now boot the 2.0.4 firmware. Please wait patiently and refer to the first boot instructions in your WiFi Pineapple MKV Instructions. You may skip any information relating to the stager.

**You are now done. Enjoy your freshly flashed WiFi Pineapple MKV!**
