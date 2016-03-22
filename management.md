# The WiFi Pineapple Web Interface

The WiFi Pineapple Web Interface provides convenient access to most WiFi Pineapple functions. It may be accessed by most modern devices (PC, Tablet, Smartphone). Officially supported web browsers include Google Chrome and Mozilla Firefox. 

## Accessing the Web Interface

To access the Web Interface, first connect to the WiFi Pineapple network from the host device. This may be accomplished in a number of ways, including Ethernet and WiFi. See the sections below regarding Internet Connection Sharing and Wired network settings for details.

Once connected to the WiFi Pineapple network, browse to the http://172.16.42.1:1471. 

Note: Be aware of the :1471 part of this URL. The WiFi Pineapple web server hosts pages on both the default port 80, as well as 1471. Port 1471 is reserved for the web interface. 

Once loaded, you will be prompted to login as root with the password configured at time of setup.

## Dashboard

The dashboard provides an at-a-glance view of the WiFi Pineapple status, landing page browser stats, notifications and bulletins.

Landing Page Browser Stats will display hits from popular web browsers when the Landing Page is enabled from Configuration. Notifications will display notifications from modules. The Bulletins feature fetches the latest project information from wifipineapple.com. 

## Recon

Unlike traditional War Driving, whereby the auditor passively listens for beacons being advertised by Access Points to paint a picture of the surrounding WiFi landscape, the WiFi Pineapple Recon goes one giant step further.

By monitoring channels for both beacons and data activity, Recon paints a more complete picture by combining Access Points with their respective clients. With the WiFi landscape displayed in this manner, a tester can quickly identify potential targets from Recon and immediately take action.

Recon allows the auditor to scan for nearby Access Points, or Access Points and their respective Clients. Clients are identified by sniffing for active traffic and are displayed underneath their parent Access Point. If a Client is associated to an Access Point but idle, it may not appear in the list. Increasing scan duration from the drop-down allows the sniffer to see more potential traffic on each channel.

The SSID, MAC, Security, Channel and Signal of Access Points are displayed in the table view. Clients are listed as MAC addresses only.

Clicking the menu button next to a MAC address shows a menu providing buttons to add or remove the MAC from the PineAP Filter or PineAP Tracking feature. Deauth uses the multiplier to send multiple deauthentication frames to the target Client. A multiplier of 2 is twice as many deauthentication frames as a multiplier of 1.

Clicking the menu button next to an SSID shows a menu providing buttons to add or remove the SSID from the PineAP Pool or PineAP Filter. Deauth Client will send deauthentication frames to all associated clients currently recognized by Recon using the multiplier. A multiplier of 2 is twice as many deauthentication frames as a multiplier of 1.

Unassociated Clients show in a unique table listed by MAC Address. These Clients have active radios, however are not associated to an Access Point.

Out Of Range Clients will display in a unique table along with their relationship to their parent Access Point by MAC address only.

Checking the Continuous box will enable an ongoing scan. The tables will update with the latest information from the scan duration interval until the scan is stopped.

## Clients

The WiFi Pineapple will allow clients to connect if Allow Associations is checked in PineAP. Connected clients will list in the Clients view along with their respective MAC Address, IP Address, the SSID to which they have connected (if Log Probes is enabled in PineAP) and Hostname. If the SSID or Hostname is unavailable it will display as such.

The Kick button allows the auditor to remove a client from the WiFi Pineapple network.

Clicking the menu button next to an MAC address shows a menu providing buttons to add or remove the MAC from the PineAP Filter or PineAP Tracking feature.

Clicking the menu button next to an SSID shows a menu providing buttons to add or remove the SSID from the PineAP Pool or PineAP Filter.

The Clients table can be updated by clicking the Refresh button.

## Filters

Filtering may be performed by Client MAC Address or SSID. Both Deny and Allow modes are supported and this option may be toggled using the switch button. 

**Client Filtering**
In Deny Mode, Clients with MAC Addresses listed in the Client Filter will not be able to connect to the WiFi Pineapple. In Allow Mode, only Clients with MAC Addresses listed in the Client Filter will be able to connect. When performing an audit, it is best to use Allow Mode to ensure that only clients within the scope of engagement are targeted.

Client MAC Addresses and SSIDs may be added from menu buttons associated with their respective listings in Recon or Client views. 

**SSID Filtering**
In Deny Mode, clients will not be able to associate with the WiFi Pineapple if they are attempting to connect to an SSID listed in the filter. In Allow Mode, clients will only be able to associate with the WiFi Pineapple if the SSID they are attempting to connect to is listed in the filter.

SSIDs may be added to the filter from the menu buttons associated with their respective listings in Recon.

**Managing Filters**
Filtered Clients and SSIDs will display in the lists. Client MAC addresses and SSIDs may be added to the list manually by using the text input field and Add button. Clicking a Client MAC or SSID will populate the text input field and clicking Remove will remove the entry from the Filter list.

## PineAP

PineAP is an effective, modular rogue access point suite designed to aid the WiFi auditor in collecting clients by thoroughly mimicking Preferred Networks.

**Allow Associations** - when enabled, Client devices will be allowed to associate with the WiFi Pineapple through any requested SSID. E.g. If a Client device sends a Probe Request for SSID "example" the WiFi Pineapple will acknowledge the request, respond and allow the Client device to associate and connect to the WiFi Pineapple network. This feature works in conjunction with Client and SSID filtering. When disabled;clients will not be allowed to associate. Formerly named Karma.

**Log Probes** - when enabled, Client device Probe Requests will be logged. This feature provides information for analysis from the Logging view. 

**Log Associations** - when enabled, Client Associations to the WiFi Pineapple will be logged. This feature provides information for analysis from the Logging view. If disabled, Associations will not be logged and may not appear in the SSID column from the Clients view. 

**PineAP Daemon** - This daemon must be enabled in order to use the Beacon Response, Capture SSIDs to Pool and Broadcast SSID pool features. The PineAP Daemon will coordinate the appropriate actions based on Source and Target MAC settings as well as the Beacon Response and SSID Broadcast intervals. This feature requires access to wlan1 and cannot be used in conjunction with WiFi Client Mode if wlan1 is used. PineAP Daemon must be enabled and PineAP Settings must be saved before the associated features will be available.

**Beacon Response** - when enabled, targeted beacons will be transmitted to Client devices in response to a Probe Request with the appropriate SSID. These beacons will not be transmitted to broadcast, but rather specifically to the device making the probe request. This prevents the beacon from being visible to other devices. If Allow Associations is enabled and the Client device associates with the WiFi Pineapple, then targeted Beacon Responses will continue to transmit to the Client device for a period of time. Beacon Responses will use the Source MAC setting, which is also shared with the Broadcast SSID Pool feature.The Beacon Response Interval will dictate how frequently to transmit.

**Capture SSIDs to Pool** - when enabled, the sniffer will save the SSID data of captured Probe Requests to the SSID Pool. This passive feature benefits the Broadcast SSID Pool feature. The SSID Pool may also be managed manually.

**Broadcast SSID Pool** - when enabled, the SSID Pool will be broadcast as beacons using the Source MAC and Target MAC settings at the interval specified. Formerly named Dogma.

**Source MAC** - by default, this is the MAC address of wlan0 on the WiFi Pineapple. This is the interface for which associations may be allowed and also hosts the Management Access Point. The MAC address of wlan0 may be changed from the Networking view. This MAC address may be set to that of a secondary WiFi Pineapple if desired.

**Target MAC** - by default, this is the broadcast MAC address FF:FF:FF:FF:FF:FF. Frames transmitted to broadcast will be seen by all nearby Client devices. Setting the Client MAC address will target PineAP features at the single device. Similar to Beacon Response, only SSIDs Broadcast from the Pool will be visible to the targeted Client device. When used in conjunction with Filtering, this feature enables precision device targeting.

**Broadcast SSID Pool Interval** - Specifies the Interval in which to Broadcast SSIDs from the Pool. Aggressive requires more CPU usage while Lower requires less.

**Beacon Response Interval** - Specifies the Interval in which to transmit Beacon Responses. Aggressive requires more CPU usage while Lower requires less.

**Save as Default on Boot** - From the Configuration menu, Saving as the Default on Boot will remember the saved PineAP features and settings for use on next boot.

**SSID Pool** - populated automatically when the Capture SSID Pool feature is enabled. May also be added to manually using the text field and Add button. Similarly, clicking a listed SSID will populate the text field allowing for the removal of the entry using the Remove button. From the SSID Pool Menu, Clear SSID Pool will remove all entries.

## Tracking

The tracking feature will continuously scan for specified Clients by MAC address and execute a customizable Tracking Script. This feature requires the Log Probes and/or Log Associations features of PineAP to be enabled. 

Clients may be specified manually using the text field and add button. Clients may also be added to the Client Tracking List by using the PineAP Tracking Add MAC button from an associated MAC address within the Clients view or Recon view. Selecting a MAC address from the Client Tracking List will populate the text field for removal using the Remove button. 

When a client is identified by a logged Probe or Association, the customizable Tracking Script will execute. The Tracking Script defines variables for the Client MAC address, the identification type (Probe or Association) and the SSID with which the Client is Probing or Associating.

## Logging

The Logging view displays the PineAP Log, System Log, Dmesg and Reporting Log.

**PineAP Log** - chronologically displays PineAP events if Log Probes and/or Log Associations are enabled. Each event contains a timestamp, event type (Probe Request or Association), the MAC address of the Client device, and the SSID for which the device is Probing or Associating.

**PineAP Log Filtering**
The Display Probes and Display Associations checkboxes enable the auditor to toggle the display of Probes or Associations. The Remove Duplicates checkbox will remove any duplicate entry, regardless of timestamp. For example, if a Client transmits a Probe Request for SSID "example" 10 times in 1 hour, checking the Remove Duplicates box will show only the first entry.

Filtering by MAC address and SSID is supported by completing the associated text fields. For example, if de:ad:be:ef:c0:fe is input in the MAC text field, only that Client device activity will show in the PineAP Log. Similarly the Log may be filtered by SSID.

Filters do not apply until the Apply Filter button is pressed. Clear Filter will reset to the default and display all captured data. Refresh Log will obtain the latest log data from PineAP and Clear Log will empty the Log File. By default the comma tab delimited PineAP log is located in /tmp and will not be saved after a reboot.

## Reporting

This feature enables the auditor to generate reports at a specified interval. The report may be sent via email and/or saved locally on a suitable SD card (NANO only). See the Format SD Card option from the USB menu on the Advanced view to setup a new card. Email Configuration must be complete in order for the Send Report via email function to operate successfully. 

The Report Contents may contain: the PineAP Log with an option to clear after generating the report, a PineAP Site Survey similar to the Recon View with option to specify AP & Client scan duration, and PineAP Probing and Tracked Clients. 

## Networking

From the Networking view, the auditor may make changes to the Routing, Access Point, MAC Addresses, Hostname and connect to an Access Point using WiFi Client Mode.

**Route** - the Kernel IP routing table is displayed and may be modified for the selected interface. The Route menu enables the auditor to Restart DNS. By default the expected Default Gateway is 172.16.42.42. When using the WiFi Pineapple Connector Android app, IP routing will automatically update to use usb0 as the default gateway.

**Access Point** - The WiFi Pineapple primary open access point and management access point may be configured. Both the open and management access point share the same channel. The open access point may be hidden and the management access point may be disabled.

**WiFi Client Mode** - this feature enables the auditor to connect the WiFi Pineapple to another wireless access point for Internet or local network access. When using WiFi Client Mode, the IP routing will automatically update to use the selected interface. The WiFi Pineapple can be used with a number of supported USB WiFi adapters to add a third (wlan2) interface. wlan0 is reserved for use by the Access Point and wlan1 is required by PineAP and cannot be used if the PineAP Daemon and its subsequent features are being used. 

To connect to a nearby Access Point, select the desired Interface and click Scan. From the Access Point list, choose the desired network, enter the Passphrase (if required) and click Connect. Once connected the WiFi Pineapple IP address will display and the Default Route will update to that of the newly connected network. Click Disconnect to end the connection.

**MAC Address** - The Current MAC address for the selected interface will display. A New MAC address may be specified manually, or set randomly using the New MAC text field and Set New MAC or Set Random MAC buttons. MAC Addresses may be reset to default from the MAC Address menu button. Changing MAC addresses may disconnect connected clients from the WiFi Pineapple.

**Advanced** - The Hostname may be updated using the hostname text field and Update Hostname button. Wireless configuration may be reset using the Reset WiFi Config to Defaults option from the Advanced menu button. The output of ifconfig is displayed.

##Configuration

The Configuration view provides the auditor with means to set general settings and modify the landing page. 

**General** - Timezone settings is displayed and may be manually selected. The system password may be set. The WiFi Pineapple may be rebooted or reset to factory defaults from the General menu button.

**Landing Page** - when enabled, this feature will act as a captive portal. New clients connecting to the WiFi Pineapple will be forwarded to this landing page. Some client devices will automatically launch a browser to this page upon connection. Landing page browser stats will display on the dashboard. PHP and HTML are accepted. The Landing Page may only display if the WiFi Pineapple has an Internet connection.

## Advanced

The Advanced view provides the auditor with information on system resources, USB devices, file system table, CSS and the ability to upgrade the WiFi Pineapple firmware.

**Resources** - displays file system disk usage and memory. From the Resources menu button Page Caches may be dropped.

**USB** - displays connected USB peripherals and allows the auditor to set the file system table (fstab). SD cards may be formatted from the USB menu button (NANO Only).

**CSS** - The WiFi Pineapple Web Interface stylesheet may be modified.

**Firmware Upgrade** - displays current firmware version and allows the auditor to check for updates. This requires an Internet connection and will initiate a connection to WiFiPineapple.com. If an update is available, the changelog will display and the option to Perform Upgrade will be available. Users are advised to carefully read the warnings related to the firmware upgrade feature.

## Firmware Upgrade Warning

Firmware upgrades replace all data (excluding external storage such as SD card or USB). Please ensure any important non-system data has been backed up.

Please stop any unnecessary services and modules before upgrading. Restarting the WiFi Pineapple without starting additional services and modules is recommended to ensure extra processes have been halted properly.

Upgrading firmware should only be done while using a stable power source. An Ethernet connection to the WiFi Pineapple is recommended for this process.

Once the firmware upgrade has completed the WiFi Pineapple will reboot into an initial setup state. This process will take several minutes. Do not interrupt the upgrade process by unplugging power or closing the web interface as this may result in a soft-brick state.

## Modules

The WiFi Pineapple is designed to be as modular as possible. Most sections of the web interface are in fact modules, which may be updated from time to time. In addition to the system modules included with the WiFi Pineapple, such as Recon, Clients and PineAP, the WiFi Pineapple supports community developed modules.

These community developed modules extend functionality by using the WiFi Pineapple API. Anyone can develop for the WiFi Pineapple using this API (learn more at wifipineapple.com) 

System and Community modules come in two varieties - GUI (web interface) and CLI (console). GUI modules will show in the web interface under the Modules menu. CLI modules may be managed using the module command from the console. 

Modules may be managed (Downloaded, updated, deleted) from the **Module Manager** section of the web interface.

Community developed modules are not required for successful operation of the WiFi Pineapple and come as-is with no warranty. Support is community driven and may be found from a modules section on the WiFi Pineapple forums. https://www.wifipineapple.com/forum

Note: Module installation on the WiFi Pineapple NANO is recommended only to an external Micro SD card.

# Console Access

The WiFi Pineapple platform is built on the OpenWRT distribution of the popular GNU/Linux ("Linux") operating system. Accessing the Linux console may provide the penetration tester with a familiar environment as both busybox (/bin/sh) and bash (/bin/bash) are included. Furthermore, packages may be installed from the opkg package management system. 

Note: (NANO) after running opkg update, install packages to the Micro SD card using the --dest parameter. Example: opkg --dest sd install nmap

Two WiFi Pineapple specific commands are provided to interface with PineAP and installed modules which support CLI functions: pineapple and module

## Secure Shell

The most common way to access the WiFi Pineapple console is via Secure Shell (SSH). SSH clients are preinstalled on most Linux and Mac systems. Windows users are advised to download a SSH utility such as the popular PuTTY client. Android users may also find compatible SSH clients from Google Play.

To connect to the WiFi Pineapple console over SSH, first connect to the WiFi Pineapple network from your host device. Once connected, ssh to the WiFi Pineapple IP address (default: 172.16.42.1) with the username root and password configured on setup. This is the same password as used to access the web interface. The SSH service on the WiFi Pineapple operates at the default port 22. 

Example: 
> ssh root@172.16.42.1


## Serial

This section applies only to the WiFi Pineapple TETRA.

Convenient access to the WiFi Pineapple TETRA serial console is provided by its USB UART port. From this console you can access the WiFi Pineapple command line, which is useful for operation from the CLI commands pineapple and module.

### Linux Hosts 
When connected to a Linux host PC via USB cable, the device will enumerate as a usbserial device. After connecting the USB cable, check the output of dmesg | grep tty to determine the device name. It will typically enumerate as ttyUSB0.

From your preferred console, access the serial device using the following settings:

> flowcontrol: none
> baudrate: 115200
> parity: none
> databits: 8
> stopbit: 1

For example, with picocom execute picocom -b 115200 /dev/ttyUSB0 or screen execute 
> screen /dev/ttyUSB0 115200.

Once connected you must press ENTER to activate the console. Login as root with the password configured at setup.

### Windows Hosts 
When connecting to a Windows hosts, open Device Manager and check for the new USB Serial Port (COM#) device under Ports (COM & LPT). Then using PuTTY, select Serial under Connection Type, enter the COM# under Serial Line and 115200 under Speed and click Open.
http://www.putty.org/

Once connected you must press ENTER to activate the console. Login as root with the password configured at setup.

Note: If Windows does not automatically install the Microsoft WHQL serial driver from Windows Update, you may download it from FTDI.
http://www.ftdichip.com/Drivers/D2XX.htm

