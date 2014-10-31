# Legacy

This article is dedicated to the **Mark IV** version of the WiFi Pineapple, and contains guides for various aspects of the Mark IV and how to recover your Mark IV.

## Accessing the UART

The instructions for connecting via the UART are the same as the Mark V's. They are located at [Serial UART](serial_uart.md).

## Enabling WAN

To utilize the WAN port, execute these commands from an SSH Session:

```
iptables -A FORWARD -i eth1 -o wlan0 -s 172.16.42.0 -m state --state NEW -j ACCEPT
iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE
```

## SSLStrip
To use SSLStrip, you must first install it :

```
opkg update
opkg install sslstrip
opkg install --dest usb python
```

Then execute these commands:

```
ln -s /usb/usr/lib/python2.7 /usr/lib/python2.7
touch /usb/usr/lib/python2.7/site-packages/zope/__init__.py
```

Now you need to configure IP Tables:

```
iptables -t nat -A PREROUTING -p tcp –destination-port 80 -j REDIRECT –to-ports 10000
iptables -t nat -A PREROUTING -p tcp –destination-port 443 -j REDIRECT –to-ports 10000
```

All you need to do now is execute SSLStrip.

```
sslstrip -w sslstrip.log &
```