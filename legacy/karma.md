# What is Karma/Jasager?

Karma is a an attack vector based on exploiting the convenience of wireless devices automatically connecting to open WiFi access points.
Jasager was the name originally given to the implementation of Karma for OpenWRT devices. The two words have since become synonymous.

# How does it Work?

Karma/Jasager works by automatically responding to 802.11 probes. These probes are sent from a client device (such as a phone or tablet). This saves you the inconvenience of having to connect to an access point manually every time you want to connect to it. Essentially, the probes sent out by a client device are done so in order to ascertain whether any previously known WiFi access points are within range. The Pineapple's Karma helpfully responds to these probe requests affirmatively (hence the name 'Jasager') and thus impersonates the access point to the user, and voila, the client device is now connected to your Pineapple whilst believing that it is connected to a familiar access point. This is possible due to the lack of authentication in open WiFi networks. Once the client is connected to the Pineapple, you are the "man-in-the-middle" which means that you are able to take full control of the users web traffic; logging URLs, redirecting HTTP requests, or even injecting images of cats into web pages!

# How do I enable Karma?

The simplest way to activate Karma is from the Web UI, in the Karma tile. If you prefer, it can also be done from a shell via executing :

```
ifconfig wlan0 up
hostapd_cli -p /var/run/hostapd-phy0 karma_enable;
```

## What devices does Karma work against?

Karma works by intercepting probe requests from potential wireless clients. Unfortunately, in recent years many software developers have patched wireless drivers in their Operating Systems to not actively broadcast probe requests whilst connected to an Access Point. This is most prevalent among mobile phone manufacturers such as Apple and Google, whose flagship software products are iOS and Android. NT-Based operating systems such as Windows are mostly unaffected due to their inability to modify wireless drivers through the "Windows Update" feature. As a general rule, almost every device running an embedded or mobile OS developed after 2012 will not work with Karma. 

Currently the main use of Karma is an opportunistic attack vector rather than a specific one. Meaning that it is better to run karma to investigate susceptible devices and proceed from there, as opposed to targeting a specific device or user.