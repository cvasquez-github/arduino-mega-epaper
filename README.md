# Arduio MEGA 2560 and WaveShare 7.5" e-Paper Display
Connecting and driving a WaveShare 7.5" e-Paper Display using an Arduino MEGA 2560.

Sample code from WaveShare GitHub:
https://github.com/waveshare/e-Paper/tree/master/Arduino/epd7in5_V2

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


# Generating an Image
- Create a grayscale (or black/white) BMP Image. 400x400 should be fine.
- Open the image in the Image2LCD utility
- Output file type: C array (*.c)
- Scan mode: Horizontal Scan
- BitsPixel: monochrome
- Reverse color
- Save

![Image2LCD Example](https://raw.githubusercontent.com/cvasquez-github/arduino-mega-epaper/main/image2lcd_example.png)

# Displaying the image
- Image2LCD utility will generate a .c file with the resulting array like: `const unsigned char gImage[20000] = {}`
- You may want to use PROGMEM to store the array data in Flash memory instead of RAM (pgmspace.h library): `const unsigned char gImage[20000] PROGMEM = {}`
