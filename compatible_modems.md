# Compatible Modems

Mobile Broadband (3G/4G) modems are a great way to provide an Internet connection to your mobile WiFi Pineapple. Typically there are two types of modems - traditional USB dongles and newer personal hotspots supporting USB tethering.

## USB Mobile Broadband Modems

Firstly in order for a USB Mobile Broadband Modem to function with the WiFi Pineapple it requires to be supported by the operating system. Thanks to USB ModeSwitch the WiFi Pineapple supports over 300 modems. This is to say that recognized modems will be /modeswitched/, allowing them to transition from being USB Mass Storage devices into being USB Serial devices.

The second part of this equation is the successful carrier configuration. The parameters required include an Interface Name, Protocol, Service, Device, APN, Username, Password, Default Route, PPP Redial, Peer DNS, DNS, Keepalive, and PPPD Options. These can be set from Network > Mobile Broadband from the WiFi Pineapple web UI. Most of these parameters, such as APN and Username, depend on the carrier.

## Personal Hotspots supporting USB Tethering

Much the same as automatic Internet Connection Sharing with tethered Android phones (Froyo and newer), these later type may be easier to configure since the hotspot device manages the connection. This alleviates the operating system from needing to deal with connection interruptions, redial attempts and other networking issues.

Typically a Personal Hotspot with a USB Tether feature (sometimes called Ethernet over USB) will automatically enumerate as a new interface (usb0) much the same way an Ethernet interface would (eth0). The Personal Hotspot usually runs a DHCP server and will assign the new usb0 interface an IP address, which the WiFi Pineapple will accept as its default gateway.

Because of this a personal hotspot supporting USB tethering is an ideal option, requiring little or no configuration, however the hardware may be more expensive than a traditional USB dongle.


## Current Modem Pool

**Table updated Sept, 14, 2014.**

| Carrier | Manufacturer | Adapter | Speed  | Type | Connection Method | Support | Vendor/Product ID | Notes |
|:--:|:--:|--|:--:|:--:|--|:--:|--|--|
|    Many    |     Many     | Android Froyo or better      | Variable |  Phone  | Device configuration, Ethernet over USB | | | [OpenWRT USB Tethering doc](http://wiki.openwrt.org/doc/howto/usb.tethering) |
|   Verizon  |    Novatel   | MiFi 5510L                   |    LTE   | HotSpot | Device configuration, Ethernet over USB | unconfirmed |  | [Verizon 5510 Manual -PDF-](http://www.novatelwireless.com/files/4513/6218/1792/UG_MiFi_5510L_VZW__30Jan2013.pdf) |
|   Verizon  |    Pantech   | MHS291L                      |    LTE   | HotSpot | USB_ModeSwitch, Ethernet over USB       | unconfirmed | 10a9:6080 -> 10a9:6085 | [Forum post on tethering](http://www.draisberghof.de/usb_modeswitch/bb/viewtopic.php?f=3&t=1572) |
|   Verizon  |    Pantech   | UML290                       |    LTE   |   USB   | USB_ModeSwitch, dialup                  | unconfirmed | 106c:3b11 -> 106c:3718 |                                                |
|  T-Mobile  |      ZTE     | MF591                        |   HSPA+  |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 19d2:1523 -> 19d2:1525 |                                                |
|   Virgin   |    Novatel   | MC760                        |   EVDO   |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 1410:5031 -> 1410:6002 |                                                |
|    Ting    |    Novatel   | MC760                        |   EVDO   |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 1410:5030 -> 1410:6000 |                                                |
|  Unlocked  |    Huawei    | E160/169/173/220/230/279/353 |   HSDPA  |   USB   | insmod, dialup                          | unconfirmed | many                   | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/26108-huawei-modems-with-a-pineapple-iv/) |
|  Unlocked  |    Huawei    | E160                         |   HSDPA  |   USB   | insmod, dialup                          |  confirmed  | 12d1:140c              | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/26108-huawei-modems-with-a-pineapple-iv/) |
|  Unlocked  |    Huawei    | E173                         |   HSDPA  |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 12d1:1436              | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/26108-huawei-modems-with-a-pineapple-iv/#entry199704) |
|  Unlocked  |    Huawei    | E160G                        |   HSDPA  |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 12d1:140c -> 12d1:140c | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/26108-huawei-modems-with-a-pineapple-iv/#entry199723) |
|  Unlocked  |    Huawei    | E353                         |   HSDPA  |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 12d1:1f01 -> 12d1:14db | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/26108-huawei-modems-with-a-pineapple-iv/) |
|  Unlocked  |    Huawei    | E169/E1750                   |   HSDPA  |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 12d1:1001              | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/26108-huawei-modems-with-a-pineapple-iv/page-2#entry199996) |
|  Unlocked  |    Huawei    | E173s                        |   HSDPA  |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 12d1:1c05              | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/26108-huawei-modems-with-a-pineapple-iv/page-3#entry205986) |
|   Sprint   |    Novatel   | MiFi 500                     |    LTE   |   USB   | Device configuration, Ethernet over USB | unconfirmed |                        | [Sprint MiFi 500 Manual -PDF-](http://shop.sprint.com/global/pdf/user_guides/novatel_wireless/mifi_500_lte/mifi_500_lte_by_novatel_wireless_ug.pdf) |
|   Sprint   |    Netgear   | Zing                         |    LTE   |   USB   | Device configuration, Ethernet over USB | unconfirmed |                        | [Sprint NETGEAR Zing eGuide](http://eguides.sprint.com/support/eguides/netgearzingmobilehotspot/index.html#netgear_zing_mobile_hotspot_ug/making_a_tethered_connection.html#_Making_a_Tethered) |
| FreedomPop |       ?      | Photon                       |   WiMax  |   USB   | Automatic, Ethernet over USB            |  confirmed  | 19f2:1700              |                                                |
|  T-Mobile  |    Huawei    | E398 (Speedstick Basic)      |   HSPA+  |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 12d1:14fe -> 12d1:1506 | [T-Mobile Speedstick Manual -PDF-](https://www.t-mobile.de/downloads/bedienungsanleitungen-endgeraete/schnellstartanleitung-speedstick-basic.pdf) |
|  Unlocked  |    Huawei    | E5830                        |   HSPA+  |   USB   | USB_ModeSwitch, dialup                  | unconfirmed |                        | [OpenWRT Forum post](https://forum.openwrt.org/viewtopic.php?id=38452) |
|  Unlocked  |    Huawei    | E355                         |   HSPA+  |   USB   | cdc_ncm                                 |  confirmed  |                        | []                                             |
|      ?     |    Novatel   | MiFi 5510                    |    LTE   |   USB   | RNDIS_HOST                              |  confirmed  |                        | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/32785-usb-tether-to-novatel-5510l/) |
|  T-Mobile  |       ?      | HUA-UMG366 Jet 2.0 USB Modem |   HSPA+  |   USB   | tty                                     |  confirmed  |                        | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/33037-settings-for-3g4g-radios/) |
|   Verizon  |    Pantech   | UML295                       |    LTE   |   USB   | cdc_ether                               |  confirmed  |                        | [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/33176-modem-verizon-pantech-uml295/) |
|    Many    |     Nokia    | n900                         | Variable |  Phone  | Serial over USB (cdc_acm)               |  confirmed  |                        | needs kmod-usb-acm, then use /dev/ttyACM0 [Hak5 Forum post](https://forums.hak5.org/index.php?/topic/32993-wifi-pineapple-mark-v-3g-managed-modems/?p=246721) |
|  T-Mobile  |    Huawei    | HUA-UMG366                   |    LTE   |   USB   | USB_ModeSwitch, dialup                  |     none    |                        | network.wan2.pppd_options=noauth[Hak5 Forum post] |
|  Unlocked  |      ZTE     | MF662                        |    LTE   |   USB   | USB_ModeSwitch, dialup                  |  confirmed  | 19d2:0017              | `use /dev/ttyUSB1` |

## Example USB Mobile Broadband Modem Configuration

Below is the configuration for a Novatel MC760 on the Ting network. Usage on other networks should be similar:

  + `Interface Name: ppp0` (almost always ppp0)
  + `Protocol: 3g` (almost always 3g)
  + `Service: cdma` (cdma or evdo for an EVDO-based carrier (Verizon/Sprint in the US) or umts for a GSM carrier (ATT/T-Mobile in the US). Also some Novatel modems support the umts_only and gprs_only value)
  + `Device: /dev/ttyUSB0` (This is the serial device the modem has enumerated as, either on its own or with the aid of USB_ModeSwitch. There are often three - ttyUSB0, ttyUSB1 and ttyUSB3 - for which one is the modem and the others are control channels. ttyUSB0 is usually the modem.)
  + `Username: internet` (The carrier Ting requires a username/password. Your carrier may require a different value or none at all)
  + `Password: internet` (Similar to username)
  + `APN:` (left blank. Typically necessary for GSM carriers and not CDMA)
  + `Default Route: 1` (1 makes the 3g modem your WiFi Pineapple's default Internet gateway for itself and connected clients. 0 does not.)
  + `PPP Redial: persist` (almost always persist)
  + `Peer DNS: 0` (1 accepts the DNS provided by the carrier's DHCP server. 0 allows you to specify your own.)
  + `DNS: 8.8.8.8` (Only necessary if the above peerdns has a value of 0. I typically to use the Google DNS but you can use whatever value you wish.
  + `Keep Alive: 1` (After how many disconnects should the connection be redialed)
  + `PPPD Options: debug` (Some modems require this value and it is not common for this value to make an impact if it is not required)

## Additional Resources

+ International APN Settings for Mobile Broadband Network Operators
+ USB ModeSwitch Device Reference