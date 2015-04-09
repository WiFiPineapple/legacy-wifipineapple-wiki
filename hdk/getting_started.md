# Getting Started with the HDK

## Things you will need

1. The HDK
2. A Wifi Pineapple
3. A Soldering iron
4. A programmer (an arduino is fine)
5. Wires
6. (optionally) a USB to serial converter.

![The HDK as it arrives](../imgs/hdk1.png)

## Set up of the HDK in the Pineapple

The HDK talks to the Wifi pineapple via a bit-banged SPI interface, using on board gpios. These are not enabled by default. In order to enable the interface, type:

`/sbin/insmod spi-gpio-custom bus0=1,18,20,19,0,125000,21`

Once this command has been run, a new device /dev/spidev1.0 will be created. 

## Soldering the HDK

![Main header to teh MK5](../imgs/hdk2.png)

![ICSP Header](../imgs/hdk3.png)

![Additional Pins](../imgs/hdk4.png)


## Programming the HDK

The easiest way to program the HDK is via an Arduino. This allows you to use the Arduino IDE, (optionally test) and deploy the code via 

![Arduino Gui](../imgs/hdk5.png)

### Example program 

You can obtain the original of this code from here: https://gist.github.com/chrismeyersfsu/3317769

```C
// Written by Nick Gammon
// February 2011
/**
 * Send arbitrary number of bits at whatever clock rate (tested at 500 KHZ and 500 HZ).
 * This script will capture the SPI bytes, when a '\n' is recieved it will then output
 * the captured byte stream via the serial.
 */

#include <SPI.h>

char buf [100];
volatile byte pos;
volatile boolean process_it;

void setup (void)
{
  Serial.begin (115200);   // debugging

  // have to send on master in, *slave out*
  pinMode(MISO, OUTPUT);
  
  // turn on SPI in slave mode
  SPCR |= _BV(SPE);
  
  // get ready for an interrupt 
  pos = 0;   // buffer empty
  process_it = false;

  // now turn on interrupts
  SPI.attachInterrupt();

}  // end of setup


// SPI interrupt routine
ISR (SPI_STC_vect)
{
byte c = SPDR;  // grab byte from SPI Data Register
  
  // add to buffer if room
  if (pos < sizeof buf)
    {
    buf [pos++] = c;
    
    // example: newline means time to process buffer
    if (c == '\n')
      process_it = true;
      
    }  // end of room available
}  // end of interrupt routine SPI_STC_vect

// main loop - wait for flag set in interrupt routine
void loop (void)
{
  if (process_it)
    {
    buf [pos] = 0;  
    Serial.println (buf);
    pos = 0;
    process_it = false;
    }  // end of flag set
    
}  // end of loop
```

### Programming the HDK

![Arduino programmer with the HDK](../imgs/hdk6.png)

### Testing



## Additional Information + Useful Links

https://randomcoderdude.wordpress.com/2013/08/15/spi-over-gpio-in-openwrt/
