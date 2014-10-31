# Internet Connection Sharing

## Linux ICS

With an Ethernet cable connected to the WiFi Pineapple, Internet access may be shared from an online computer. This is typically achieved with a cable connected between a notebook computer and the WiFi Pineapple directly. The notebook computer requires some form of Internet access (typically through WiFi or Mobile Broadband).

By default the WiFi Pineapple has an IP address of 172.16.42.1 and will assign WiFi clients with IP addresses in teh 172.16.42.100-150 range via an onboard DHCP server. The default gateway of the WiFi Pineapple is 172.16.42.42. This means the WiFi Pineapple is looking for an Internet connection from a host with this IP address. A simple tethering script is available for Linux host which will automatically setup the IP and forwarding. Download the script from the scripts directory [here](scripts/wp5.sh)

Power the WiFi Pineapple
Connect an Ethernet cable directly between the LAN port on the computer and the LAN port on the WiFi Pineapple
On the computer, download the wp5.sh script from http://www.wifipineapple.com/wp5.sh
Make the script executable with //chmod +x wp5.sh// and run the script as root (e.g. //sudo ./wp5.sh//)
Follow the on screen prompts
EhwTSS7.png

## Windows ICS

## OSX ICS

## Android ICS