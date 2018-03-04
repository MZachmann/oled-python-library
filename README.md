 This## oled-python-library
A simple library to draw pixels and good quality text to those typical oled displays.
# Simple SSD1306 & SH1106 Python Library
This library enables pixel set/reset/invert for the two primary small OLED controllers. It also includes high quality character display.

This code base only supports **I2C** for the [**Pycom MicroPython**](https://pycom.io) implementation. The communication interface is separated, though, so other pythons/comm languages are easy to support. This is also tested / working as-is on the awesome [**Loboris MicroPython fork.**](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo)
## Simple example

```python
from graphicslib import OledGrafx
x = OledGrafx.OledGrafx(True)
x.PrintStrings("One","Two","3","4")
```
## Installation
Copy the graphicslib folder and contents to your project
## Usage

| Module|Method | Description|
|---| ------------- | ----- |
|OledGrafx||Extremely high level helpers|
||OledGrafx(isFor1306)| Constructor. isFor1306==True for SSD1306, False for SH1103 |
||PrintStrings(first, second, third, fourth)| This prints up to four given strings. They go in the available four lines on a 64 line display.  |
|OledDisplay ||Lower level Oled methods|
||OledDisplay(is1306=True, height=64, external_vcc=False, i2c_devid=0x3c)| Constructor where: is1306 is True for the SSD1306 False for the SH1106; height is the height in scan lines (32 or 64); external_vcc is set True if external power (this may not work on SH1106); i2c_devid is the i2c device id |
||init_display()|This *must be called first*. Initializes hardware.
||clear()| Clear the oled display buffer |
||display()| Move the display buffer to the display  |
||set_pixel(x, y, style)| Draw a pixel in the display buffer. Style = OledDisplay.PIXEL_ON, PIXEL_OFF, or PIXEL_INVERT|
||poweron()|Enable the display|
||poweroff()|Disable the display. All parts go to sleep.|
||set_contrast(amount)|Set the white pixel brightness from 0...255 (one byte). 0=not very black. 255=full brightness.|
|I2cHelper||This is the comm (I2c) interface wrapper. The modules don't pop exceptions but do return failure results.|
||I2cHelper(address)|Constructor. Supply the I2C device ID.|
||SendBuffer(data)|Sends the data bytearray to the device. Returns True if it worked, False on failure. Exceptions are printed to the console.  |
||SendString(text)|Sends the text string to the device. Returns True if it worked, False on failure. Exceptions are printed to the console.  |
||ReadBuffer(size)|Read size bytes from I2C. Returns None on failure else a bytearray.|
||ReadString(size)|Read a string of size bytes from I2C. Returns None on failure else a string (UTF-8)|
|FontDrawer||This module draws characters to the screen|
||FontDrawer(font, oled)|Constructor. Takes a font (see the FontArialxx modules) and an OledDisplay instance|
||DrawChar(theChar, x, y)|Draw a character at x,y (upper left). theChar should be an integer value not a character (string)|
||DrawString(text, x, y)|Draw the text string starting at (x,y) using proportional spacing.|
