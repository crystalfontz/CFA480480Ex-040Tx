# CFA480480Ex-040Tx
Example code for 4" Square EVE modules
# CFA480480E0-040Tx EVE Demo Code

This example Seeeduino (Arduino clone) code is for the Crystalfontz line of 4" square displays powered by a Bridgetek EVE chip. These displays are driven by the powerful BT817 chip and are available in capacitive touch and non-touch. Please refer to the datasheets for more information.

For more information on our full list of EVE displays, please click [here](https://www.crystalfontz.com/products/eve-accelerated-tft-displays.php)

## Display information
4" EVE Displays\
[CFA480480E0-040TW](https://www.crystalfontz.com/product/cfa480480e0040tw) - Capacitive Touch With Overhanging Glass\
[CFA480480E0-040TN](https://www.crystalfontz.com/product/cfa480480e0040tn) - Non-Touch


 
Full Functional Seeeduino Demo Kits for these products can be found here:  
[CFA480480E0-040TW-KIT](https://www.crystalfontz.com/product/cfa480480e0040twkit) - Capacitive Touch With Overhanging Glass Dev Kit\
[CFA480480E0-040TN-KIT](https://www.crystalfontz.com/product/cfa480480e0040tnkit) - Non-Touch Dev Kit

## Navigating the Code

To toggle on or off different demonstrations, some defines in "CFA10118_defines.h" can be changed.

```c++
#define BMP_DEMO             (0)  
#define   BMP_SCROLL         (0)  
#define SOUND_DEMO           (0)  
#define   SOUND_VOICE        (0)  
#define   SOUND_PLAY_TIMES   (10)
#define LOGO_DEMO            (1)  
#define   LOGO_PNG_0_ARGB2_1 (1)  
#define BOUNCE_DEMO          (1)  
#define MARBLE_DEMO          (0)  
#define TOUCH_DEMO           (0)
#define VIDEO_DEMO           (0) 
```

`BMP_DEMO`    - Toggled to 1 will display "SPLASH.a8z" from flash \
`BMP_SCROLL`  - Toggled to 1 will display "CLOUD.a8z" from flash and scroll it accross the screen. Requires BMP_DEMO is also set to 1\
`SOUND_DEMO`  - Toggled to 1 will look to the uSD card to pull a file and play it. File is chosen by SOUND_VOICE \
`SOUND_VOICE` - Toggled to 1 will look to the uSD card to pull the "VOI_8K.RAW" file. Toggled to 0, will pull "MUS_8K.RAW"\
`LOGO_DEMO`   - Toggled to 1 will display the Crystalfontz Logo from flash\
`BOUNCE_DEMO` - Toggled to 1 will show a ball bouncing around the screen\
`MARBLE_DEMO` - Toggled to 1 will display a rotating earth from flash.\
`TOUCH_DEMO`  - Toggled to 1 will enable the touch screen (only compatible on touch versions of the module)\
`VIDEO_DEMO`  - Toggled to 1 will enable the video playback of Ice_400.avi from flash.

If the above indicates "from flash" the file must already be programmed into flash by using PROGRAM_FLASH_FROM_USD

## Flash Usage
Creating the files:
1. Open [EVE Asset Builder](https://brtchip.com/eab/)
2. In the Image Converter tool, use the "ADD" button to load the image
3. Set the output format to "ASTC_8x8" and ASTC Preset to "thorough" and click compressed
4. Click Convert and rename the extension of the *.bin file to *.a8z
5. The file names are hard coded in the firmware. These names can be found starting on line 104 of demos.cpp

Configuring the demo code:
1. Load the files on an SD card and connect to the Seeeduino (see pinout)
2. Set PROGRAM_FLASH_FROM_USD to 1
3. Compile and upload the firmware
4. Watch the serial monitor, the code will export the memory locations that are needed for the demo code to work
5. Take the macros that are exported from the code and insert them on line 92 of CFA10118_defines.h
6. Set PROGRAM_FLASH_FROM_USD to 0
7. Set VIDEO_DEMO to 1 
8. Compile and upload the code

Here is an example of the macros that will exported from the code:
```c++
#define FLASH_SECTOR_MARBLE (1UL)
#define FLASH_LENGTH_MARBLE (14400UL) // sectors: 3
#define FLASH_SECTOR_SPLASH (5UL)
#define FLASH_LENGTH_SPLASH (57600UL) // sectors: 14
#define FLASH_SECTOR_CLOUDS (20UL)
#define FLASH_LENGTH_CLOUDS (57600UL) // sectors: 14
#define FLASH_SECTOR_ICE_FPV_512x300 (35UL)
#define FLASH_LENGTH_ICE_FPV_512x300 (12882892UL) // sectors: 3145
//Total sectors = 4096, free sectors = 915
//Total flash = 16777216, free flash = 3747840
```

For an in-depth guide to loading custom images on our EVE lineup of displays without an SD card (using the Seeeduino's flash memory), please refer to our blog post [available here](https://www.crystalfontz.com/blog/custom-images-on-eve-displays/).

## Connection Details
#### To [CFA10098 Adapter Board](https://www.crystalfontz.com/product/cfa10098) (See kits above)
| 10098 Pin         | Seeeduino Pin| Connection Description |
|-------------------|--------------|------------------------|
| 1  (3v3)          | 3v3          | +3.3V Power            |
| 2  (GND)          | GND          | Ground                 |
| 3  (SCK)          | D13          | Serial Clock           |
| 4  (MOSI/D0)      | D11          | MOSI/D0                |
| 5  (MISO/D1)      | D12          | MISO/D1                |
| 6  (GPIO0/D2)     | DNC          | GPIO0/D2               |
| 7  (GPIO1/D3)     | DNC          | GPIO1/D2               |
| 8  (GND)          | GND or DNC   | Ground                 |
| 9  (CS)           | D9           | Chip Select            |
| 10 (INT)          | D7           | Interupt               |
| 11 (PD)           | D8           | Chip Power Down        |
| 12 (MODE/GPIO2)   | DNC          | MODE/GPIO2             |
| 13 (AUDIO)        | DNC          | Audio PWM              |
| 14 (GND)          | GND or DNC   | Ground                 |


#### To Optional [uSD Adapter Board](https://www.crystalfontz.com/product/cfa10112) 
| microSD Pin | Seeeduino Pin| Connection Description |
|-------------|--------------|------------------------|
| 1 (CS)      | D10          | SD CS                  |
| 2 (DI)      | D11          | SD MOSI                |
| 3 (DO)      | D12          | SD MISO                |
| 4 (VDD)     | 3v3          | +3.3V Power            |
| 5 (SCLK)    | D13          | SD SCLK                |
| 6 (VSS)     | GND          | Ground                 |

## Additional Accessories
Additional accessories for the products can be found at the bottom of each of the product pages. This includes 30 position FFC cables, wires, and any accessory boards that are available.
