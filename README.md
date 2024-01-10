# M5-Clock

Simple Clock App for M5Stack's M5Paper

There are very few apps and no documentation for this promising bit of hardware so I wanted to share this. Here's the features that it uses :-
* TTF font loading (from SPIFFS as I couldn't get SD loading working),
* RTC get time and syncing to NTP,
* RTC deep sleep / M5.shutdown(s) (it's more like a shutdown with timed wake-up),
* NVS storage of variables across sleep,
* HTTP API call to fetch weather,
* Loading and displaying a weather image.

Here's what I discovered :-
* You can't use Serial and update the EPD at the same time !!
* Can't get the SD card to work at all
* M5.shutdown(s) doesn't work when the USB cable is connected
* Shutdown restarts the sketch from scratch i.e. all state lost and runs setup()

Have fun !

## Installation

1. Open in Arduino IDE
2. Install Board Plugin as described [here](https://docs.m5stack.com/en/quick_start/m5paper/arduino)
3. Set the correct Board in the IDE (`M5Stack Paper` or `M5Paper`)
4. Install required libraries: I'm not sure which ones are needed since I already had quite a lot of them installed, but during compile the IDE will tell you that some header (`something.h`) is missing. By googling that header, you will find out what Library you need to install.
5. Copy the font file to the SPIFFS using [this](https://github.com/me-no-dev/arduino-esp32fs-plugin) plugin (everything is explained there, note that at least until now you need Arduino IDE 1.x for this)
6. Change Wifi SSID, Password and the Weatherapi.com API key at the beginning of the code to your needs
7. Compile and uploads

## Known issues

### Initially wrong date

I'm not sure why, but initially after the Clock updated, the right time was shown but with an incorrect date (like not something zero, but some random date).
Also a reset (using the reset button on the back) didn't fix this.
Since this resolved automatically after some time (not sure how long, I was away and when I came back after some hours it showed the correct date), I didn't spend any time into debugging this, since for me there was nothing start at.
This just as an information, so don't need to be as confused as I was.

### Dates with 0 show "Saturday" as ordinal

This is probably some OutOfBounds thing caused by the calculation of the ordinals, I have to look into it.
