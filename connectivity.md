# Internet Connectivity

The WiFi Pineapple may be used to provide WiFi clients with Internet access. While this may not be necessary for all deployment scenarios, it is commonly configured. There are four basic methods for setting up an Internet connection on the WiFi Pineapple.

1. Wired Internet Connection
2. Internet Connection Sharing
3. USB Tethering
4. WiFi Client Mode

These sections serve as guides to setting up a WiFi Pineapple Internet connection. However, please be advised that this guide cannot cover the infinite possible network configurations.

## Wired Internet Connection

The **WiFi Pineapple TETRA** provides two Ethernet ports. A WAN port via a traditional RJ45 port, as well as a LAN port accessible by its USB ETH port. The USB ETH port connects the host device to the LAN via an onboard Realtek USB Ethernet controller.

The WAN port is connected to eth0 on the WiFi Pineapple TETRA and by default will attempt to obtain an IP address from DHCP.

The LAN port is connected to eth1 on the WiFi Pineapple TETRA and hosts the internal DHCP server which will offer an IP address in the 172.16.42.x range by default.

Note: If Windows does not automatically install the Microsoft WHQL USB Ethernet driver from Windows Update, you may [download it from Realtek](http://www.realtek.com.tw/downloads/downloadsView.aspx?Langid=1&PNid=55&PFid=55&Level=5&Conn=4&DownTypeID=3&GetDown=false#RTL8152B%28N%29).

The **WiFi Pineapple NANO** may be enhanced with wired Ethernet functionality by using a supported USB Ethernet adapter. This accessory, when plugged into the USB Host port on the WiFi Pineapple NANO, will enumerate as eth1. Standard network and firewall configuration may apply. See the appropriate /etc/config files for details.

## Internet Connection Sharing

One of the most popular deployment scenarios is to configure the WiFi Pineapple to share an Internet connection from a personal computer, such as a notebook running Windows or Linux. With the WiFi Pineapple providing its WiFi clients Internet access from the host PC, the penetration tester may then extend MITM functions through desktop applications such as packet analyzers and auditing frameworks. 

## Ethernet with Windows

By default the WiFi Pineapple is expecting an Internet connection from 172.16.42.42 on its LAN. Connect the WiFi Pineapple LAN port to the Windows PC host. On the NANO this is the male USB A plug. On the TETRA this is the USB ETH port.

* Open Control Panel > Network and Internet > Network Connections
* Locate the WiFi Pineapple network interface

Note: For convenience the network interface may be renamed by highlighting it and pressing F2

* From the Internet connection source (typically a Wi-Fi or Ethernet), right-click the interface and select Properties.
* From the Sharing tab check the box labeled Allow other network users to connect through this computer's Internet connection and select the WiFi Pineapple network interface from the drop down menu.
* Click OK
* Right-click the WiFi Pineapple network interface and select Properties
* Select Internet Protocol Version 4 (TCP/IPv4) and click Properties
* Replace the default IP address with 172.16.42.42
* Click OK
* Click Close

## Ethernet with Linux

By default the WiFi Pineapple is expecting an Internet connection from 172.16.42.42 on its LAN. Connect the WiFi Pineapple LAN port to the Linux PC host. On the NANO this is the male USB A plug. On the TETRA this is the USB ETH port.

Once connected, the network connection of the host Linux PC may be forwarded to the WiFi Pineapple using iptables. A free script is available to aid in iptables configuration for most Linux hosts. To download the script from the terminal, run:  

> wget www.wifipineapple.com/wp6.sh

Next the script must be made executable, typically by running:  

> chmod +x wp6.sh

Finally execute the script by running: 

> ./wp6.sh

The WiFi Pineapple Connector script for Linux offers either guided or manual setup modes. For most the guided setup is advised. Press G then follow the onscreen prompts to save the connection settings. Once saved, press C to connect.

The WiFi Pineapple Connector script for Linux is provided free of charge for convenience, without warranty, and is not necessary for successful operation of the WiFi Pineapple.

## USB Tethering (Android)

The WiFi Pineapple can be provided an Internet connection from many means, including USB Ethernet adapters. Many Android devices have the capability to emulate a USB Ethernet adapters, sharing their Internet connections with other devices like notebook computers.

Check to see if your Android device supports this Internet Connection Sharing method by selecting Tethering and Portable Hotspot from the Network section of the Settings application. If the option for USB Tethering exists, your Android device may be capable of sharing its Internet connection with the WiFI Pineapple.

Depending on Android ROM and Carrier restrictions, this feature may be unavailable or require a subscription. To test, plug a data-capable USB cable between the host port on the WiFI Pineapple and the Android device. The USB Tethering option should become available.

Note: The USB cable provided with the Pineapple Juice battery is for charging only and does not support data transfer.

If USB Tethering is supported by the Android device, when enabled it will enumerate on the WiFi Pineapple as a new network interface, usb0, and the WiFi Pineapple will automatically adjust its kernel routing table to use this interface for its Internet access, as well as Internet access for any clients connected to the WiFi Pineapple. Via DHCP, the WiFi Pineapple will receive an IP address on the Android devices internal network (typically 192.168.x.x).

Since the WiFi Pineapple will become a client on the Android devices internal network, it is possible to access the WiFi Pineapple web interface from the Android device if the WiFi Pineapple's IP address is known.

For convenience in accessing the USB Tethering setting, as well as discovering the IP address of the WiFi Pineapple on the Android devices network and browsing to the web interface, a [WiFi PIneapple Connector app for Android is provided free of charge from Google Play](
https://play.google.com/store/apps/details?id=org.hak5.pineappleconnector).

When launching the WiFi Pineapple Connector android app, you will be prompted to configure tethering. Tapping Configure will jump to the systems Tethering and Portable Hot Spot settings menu, if available. Tap to enable USB Tethering, then tap back. Once enabled, the WiFi Pineapple Connector app will wait for a network connection from the WiFi Pineapple indicating its IP address on the Android devices internal network. Once discovered, the browser will automatically load the web interface.

Not all Android devices use the standard USB Tethering API or may block the data transfer from the WiFi Pineapple to the Android device. In this case USB Tethering may be enabled, but the WiFi Pineapple Connector app will be unable to determine the IP address of the WiFi Pineapple and launch the browser automatically. In this case determining the IP address of usb0 on the WiFi Pineapple may be initiated by another means, such as from a serial connection or from another device connected to the WiFi Pineapple over WiFi.

The Android API restricts systematically enabling the USB Tethering function, which is why the WiFi Pineapple Connector app can only jump to the systems Tethering and Portable Hotspot settings menu. This functionality may be achieved on rooted devices by other means.

The WiFi Pineapple Connector app for Android is provided free of charge for convenience, without warranty, and is not necessary for successful operation of the WiFi Pineapple.

## WiFi Client Mode

The WiFi Pineapple may obtain an Internet connection from a nearby access point, such as a traditional wireless router as well as personal hotspots and WiFi tethering from smartphones. While achievable throughput may not be as high as with traditional wired, shared or tethered configurations - WiFi Client Mode provides significant convenience for many deployments.

To begin, first note that while the WiFi Pineapple includes two radios (wlan0 and wlan1), they are both required for PineAP operation. If the second radio (wlan1) is used for Client Mode, PineAP functions may not be used. For this reason the auditor is advised to use an external USB WiFi adapter with a compatible chipset.

Compatible chipsets include RaLink RT2800 devices, as well as some Atheros and RealTek devices. Wireless adapters from HakShop.com are certified to work with the WiFi Pineapple.

To enable WiFi Client Mode, navigate to the Networking section of the web interface. From the WiFi Client Mode heading, select the desired interface. When using external USB WiFi adapters, these will be listed as wlan2 and greater. 

With the preferred adapter selected, click Scan to perform a site survey of nearby access points. When the scan completes, a list of Access Points will be available from a drop-down menu. 

Selecting an Access Point will display additional information about the base station, such as BSSID, SSID, channel, signal strength, quality and security.

WPA protected Access Points will require a password. With the Access Point selected, and a WPA key entered if required, click Connect. This will instruct the WiFi Pineapple to attempt to associate with the selected network and obtain an IP address from DHCP. Clicking Refresh will identify the WiFi Pineapple IP address on the target network.

Once configured for WiFi Client Mode, the WiFi Pineapple will attempt to connect to the desired Access Point after each boot. 

To disconnect and prevent subsequent connections at boot, click the Disconnect button from the WiFi Client Mode section of the Networking page in the web interface.

WiFi Client Mode connection information is stored in the **/etc/config/wireless** configuration file.

