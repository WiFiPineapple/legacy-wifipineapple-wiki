# Legacy

This article is dedicated to the **Mark IV** version of the WiFi Pineapple, and contains guides for various aspects of the Mark IV and how to recover your Mark IV.

## Accessing the UART

The instructions for connecting via the UART are the same as the Mark V's. They are located at [Serial UART](serial_uart.md).

## Enabling WAN

In order to utilize the WAN port, execute these commands from an SSH Session:

```
iptables -A FORWARD -i eth1 -o wlan0 -s 172.16.42.0 -m state --state NEW -j ACCEPT
iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE
```

## SSLStrip
To use SSLStrip, we first need to install it as well as Python. Ensure that your Pineapple is connected to the internet and then from an SSH session, issue the following commands:

```
opkg update
opkg install sslstrip
opkg install --dest usb python
```

Then we need to create a symlink from the USB Mass Storage to the Pineapple's root directory (/) to ensure that Python will work properly:

```
ln -s /usb/usr/lib/python2.7 /usr/lib/python2.7
touch /usb/usr/lib/python2.7/site-packages/zope/__init__.py
```

Finally, IPTables need to be configured correctly so as to allow the web traffic to be redirected to SSLStrip:

```
iptables -t nat -A PREROUTING -p tcp –destination-port 80 -j REDIRECT –to-ports 10000
iptables -t nat -A PREROUTING -p tcp –destination-port 443 -j REDIRECT –to-ports 10000
```

Now you can execute SSLStrip as normal:

```
sslstrip -w sslstrip.log &
```