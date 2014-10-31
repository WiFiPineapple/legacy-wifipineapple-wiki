# What is Karma?

Karma is a an attack vector based on exploiting the convenience of automatically connecting to that free wireless.

# How does it Work?

Karma/Jasager works by automatically responding to 802.11 probes. These probes are sent from your client device (like your phone and tablet), These save the convenience of having to connect to the remembered wireless by doing it for you, asking "Is my open network around?". The Pineapples Karma helpfully responds to these probe requests, and says "Sure, I'm your remembered network, lets get you online!", And voilla, your pineapple is now the remembered wireless. From this, Monitor network traffic, inject code into pages and even spoof pages to have pictures of funny cats, if you'd like.

# How do I enable Karma?

Karma is most easily enabled from the Web UI, in the Karma tile. You can also enable it from a shell by executing :

```
ifconfig wlan0 up
hostapd_cli -p /var/run/hostapd-phy0 karma_enable;
```

## What devices does Karma work against?

Note: NB: Not entirely correct. To be edited.

Karma works by intercepting probe requests from potential wireless clients. Unfortunately, in recent years many software developers have patched wireless drivers in their Operating Systems to not actively broadcast probe requests whilst connected to an Access Point. This is most prevalent amongst mobile operating systems such as iOS and Android. NT-Based operating systems such as Windows are mostly unaffected due to their incapability to modify wireless drivers through the "Windows Update" feature. As a general rule, almost every device running an embedded or mobile OS developed after 2012 will not work with Karma.

Currently the main use of Karma is an opportunistic attack vector rather than a specific one. Meaning that it is better to run karma to investigate susceptible devices and proceed from there, as opposed to targeting a specific device or user.