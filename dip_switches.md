# DIP Switches

## What do the DIP Switches do?

The new DIP's on the Mark V are available to configure different boot modes/operations. These modes can be easily set from the WebUI, and are labeled 1 through 5 from left to right. Switches 1 and 5 and reserved for system use while 2 through 4 are available to set to whatever you want.

## How do I set the DIP Switches?

You can set the DIP's via clicking on the 'Configuration' tile in the Web UI, then navigating to the Boot Menu tab. You can then place BASH commands in the textboxes next to the combination of switches you would like to have. After saving these, you can boot your pineapple with the same combination set on the DIP's and expect your entered commands to execute on bootup.

![](imgs/dip_switches.png)

## What are some examples of this?

Some examples of what to execute can be found below! Be imaginative, and feel free to add your favourite commands to the list!

|   Boot Mode  |    Command   |
|:------------:|:------------:|
| Auto Capture |   `ifconfig wlan1 up; airmon-ng start wlan1; airodump-ng --write /sd/airodump.csv --output-format pcap mon0;`   |
|  Karmasnarf  | ```hostapd_cli -p /var/run/hostapd-phy0 karma_enable; urlsnarf -i br-lan > /sd/infusions/urlsnarf/includes/log/output_`date +%s`.log &``` |

