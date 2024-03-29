# Arduino MEGA 2560 and WaveShare 7.5" e-Paper Display
Connecting and driving a WaveShare 7.5" e-Paper Display using an Arduino MEGA 2560.

| e-Paper Drive Hat | Arduino MEGA    |
| :-------------:   | :-------------: |
| BUSY              | D7              |
| RST               | D8              |
| DC                | D9              |
| CS                | D10             |
| CLK               | D52             |
| DIN               | D51             |
| GND               | POWER GND       |
| VCC               | POWER 5V+       |

![alt text](https://raw.githubusercontent.com/cvasquez-github/arduino-mega-epaper/main/arduino-mega-epaper-hat.png)

## Displaying Full Screen Images using Waveshare samples
Sample code from WaveShare GitHub:
https://github.com/waveshare/e-Paper/tree/master/Arduino/epd7in5_V2

### Generating an Image
- Download Image2LCD Utility from WaveShare wiki page: https://www.waveshare.com/wiki/File:Image2Lcd.7z
- Create a grayscale (or black/white) BMP Image. 400x400 should be fine.
- Open the image in the Image2LCD utility
- Output file type: C array (*.c)
- Scan mode: Horizontal Scan
- BitsPixel: monochrome
- Reverse color
- Save

![Image2LCD Example](https://raw.githubusercontent.com/cvasquez-github/arduino-mega-epaper/main/image2lcd_example.png)

### Displaying the image
- Image2LCD utility will generate a .c file with the resulting array like: 
`const unsigned char gImage[20000] = {}`
- Import/Copy the array into your project.
- You may want to use PROGMEM to store the array data in Flash memory instead of RAM (pgmspace.h library): 
`const unsigned char gImage[20000] PROGMEM = {}`
- Then use the Displaypart(PositionX, PositionY, Width, Height) method to write it to the display. Make sure you set the width and height accordingly.  
`epd.Displaypart(gImage,200, 40,400,400);`
 
![WaveShare Output Example](https://raw.githubusercontent.com/cvasquez-github/arduino-mega-epaper/main/waveshare_example_output.jpg)

Note: the refresh is really slow! So I wouldn't recommend this for displaying something you may want to continously update (maybe only for things you update once a day, like over night...)

## Advanced graphics Using GxEPD2 Library
GxEPD2 GitHub:
https://github.com/ZinggJM/GxEPD2

GxEPD2 Examples:
https://github.com/ZinggJM/GxEPD2/tree/master/examples

First include the display selection headers:
`#include "GxEPD2_display_selection.h"`
`#include "GxEPD2_display_selection_added.h"`

Uncomment the following line from the GxEPD2_display_selection.h file:
`GxEPD2_BW<GxEPD2_750_T7, MAX_HEIGHT(GxEPD2_750_T7)>`

And set the CS, DC, RST and BUSY pins accordingly (DC and RST are inverted):
`GxEPD2_BW<GxEPD2_750_T7, MAX_HEIGHT(GxEPD2_750_T7)> display(GxEPD2_750_T7(/*CS=*/ 10, /*DC=*/ 9, /*RST=*/ 8, /*BUSY=*/ 7)); // GDEW075T7 800x480, EK79655 (GD7965)`

