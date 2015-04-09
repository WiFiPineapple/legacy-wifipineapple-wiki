# Getting Started with the HDK

## Things you will need

1. The HDK
2. A Wifi Pineapple
3. A Soldering iron
4. A programmer (an arduino is fine)
5. (optionally) a USB to serial converter.

![The HDK as it arrives](imgs/hdk1.png)

## Set up of the HDK in the Pineapple

The HDK talks to the Wifi pineapple via a bit-banged SPI interface, using on board gpios. These are not enabled by default. In order to enable the interface, type:

`/sbin/insmod spi-gpio-custom bus0=1,18,20,19,0,125000,21`

Once this command has been run, a new device /dev/spidev1.0 will be created. 

## Soldering the HDK

![](imgs/hdk2.png)

![](imgs/hdk3.png)

![](imgs/hdk4.png)


## Programming the HDK

![](imgs/hdk5.png)

### Example program 

```C

```

## Testing



## Additional Information + Useful Links

https://randomcoderdude.wordpress.com/2013/08/15/spi-over-gpio-in-openwrt/
