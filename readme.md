

# SIMHUB Arduino RPM indicator readme

Instructions specific to Arduino Nano Every

![enter image description here](https://i.imgur.com/RLqtLm3.gif)
Project requires:

 - 1x Arduino Nano Every 
 - 1x SSD1306 128x64px OLED screen
 -    2x 8 pixel Neopixel strips   
 - 3d printed case (STL included in repository)  
 - SimHub software

## Neopixel setup

    Place 2 strips together end to end, flip over, solder all 4 pads straight across 
    Wire GND to Arduino GND 
    Wire 4-7VDC to 5v on Arduino 
    Wire DIN to D6 on Arduino 

            

## OLED setup - SSD1306 128x64

    Desolder pins on GND, VCC, SCL, SDA if necessary
    Wire GND to Arduino GND
    Wire VCC to 5v on Arduino
    Wire SCL to A5 on Arduino
    Wire SDA to A4 on Arduino
    SCL and SDA pins for Arduino Nano Every, may change per board

Everything can now be placed in the case.



## SIMHUB setup

	- Note that the file DisplayClientV2 folder contains the final working code for MY SPECIFIC setup.  May not work the same for you.
	- I had to write this for a Nano Every, the SimHub built in editor appears to not want to upload to it.
	- If you use a different model of Arduino, you may be able to use the built in editor instead of Arduino IDE

    Plug in Arduino
    Open Arduino, go to My Hardware
    Set WS2812B leds count to 16
	Set WS2812B data pin to 6
    Set OLED LCD enabled
    Click open in Arduino IDE
    As you can see, the only 2 lines in the includes that aren't commented are WS2812B and OLED
    If you want to modify how the gear selection displays -
        Go to SHGLCD_I2COLED.h file
        setRotation value can be changed to change orientation of text
        setTextSize and setFont can be changed to change the size of text
            Mine looks like this
            	void Init() {
                    glcd1.begin(SSD1306_SWITCHCAPVCC, 0x3C);
                    glcd1.clearDisplay();
                    glcd1.setFont();
                    glcd1.setTextSize(2);
                    glcd1.setTextColor(WHITE);
                    glcd1.setRotation(3);
                    glcd1.setCursor(0, 0);
                    glcd1.print("");
                    glcd1.display();
                    }
    Save the files necessary 
    Import "LED Strip.ledsprofile" in Simhub under Arduino/RGB LEDs
    Modify part1.ini under SimHub\OLEDTemplate\Ingame\0_Default or overwrite with file from this repository
        Mine looks like this   
            [Text]
            X=37
            Y=100
            Color=1
            Text=[DataCorePlugin.GameData.NewData.Gear]
            FontSize=3
            FontType=2
            Align=3
		At some point that stopped working, and I had to change to this
			[Text]
			X=62
			Y=30
			Color=1
			Text=[DataCorePlugin.GameData.NewData.Gear]
			FontSize=10
			FontType=0
			Align=3
		If you want the date and time idle display to work, modify part1.ini under \Idle\TurboChanged
			I didn't edit this on mine so I don't have a file for it
    Upload sketch to Arduino from the Arduino IDE
    After you get it where you want, back up the files in SimHub\_Addons\Arduino\DisplayClientV2
	
## Troubleshooting
	Simhub connects, then disconnects Arduino and never displays data
		Make sure baud rate is set to 19200
	
	Gear position is flipped upside down, or does not display properly
		Try the second block for the display listed in this Readme.
		Change X and Y coords until you get something displayed.
		Change font size and align until you get something displayed.
		Once something displays on the screen, fine tune the settings.


