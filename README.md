# 320x240 Landscape Keyboard

This is code for a landscape mode keyboard on 320x240 displays using the ILI9341 TFT and an XPT2046 touchscreen.  
You must install and set up your config file for TFT_eSPI library to use this.

## Compatibility
ILI9341 red display  
XPT2046 touch panel on the display  
(not for Adafruit TFT, different touch chip)  

## Wiring
Wire TFT and Touch into your SPI bus pins, make sure TFT_eSPI knows which pins they are. CS and DC pins for TFT went to any GPIO. CS pin for touch went to any GPIO.

## Notes
Arduino IDE  
This was tested with a cheap red-color touch TFT connected to an ESP32-S3 using SPI.  
The Adafruit TFT uses a different touch chip and likely won't work with this.  

## Requirements
Requires TFT_eSPI library in Arduino IDE  
New users: learn about User_setup and User_setups directory to make it work  

_ means Enter 
< means Backspace
