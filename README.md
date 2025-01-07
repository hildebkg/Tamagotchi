# ArduinoGotchi - A real Tamagotchi emulator for Arduino UNO

## Synopsis

**ArduinoGotchi** is a real [Tamagotchi P1](https://tamagotchi.fandom.com/wiki/Tamagotchi_(1996_Pet)) emulator running in Arduino UNO hardware. The emulation core is based on [TamaLib](https://github.com/jcrona/tamalib) with intensive optimization to make it fit into UNO's hardware that only comes with 32K Flash 2K RAM.

![Tamagotchi P1 Actual Devices](../main/images/TamaP1_devices.jpg)

## Fork notice

I did the following changes after forking [original repo](https://github.com/GaryZ88/ArduinoGotchi)
- Created a platformio project, so it is easy to target multiple platforms
- Created ports for ESP8266 and ESP32, mainly because speed on 8-bit AVR is just too slow
- Added long click on "back" button - if you press it for 5 seconds, it will reset memory back to egg state
- Added inverted Speaker connection setting. Mainly because the Piezo modules that I have are active on Low. Another reason is mentioned below.

I personally assembled the ESP8266 version with Wemos D1 Mini on perf board, using built-in LED together with speaker, so when it sounds, LED is blinking as well.

### Demo
![Demo #1](/images/VID_20220923_205516.mp4.gif)
![Demo #2](/images/VID_20220923_205528.mp4.gif)
![Demo #3](/images/VID_20220923_205823.mp4.gif)

## How to build and run

Use Platformio. Run `build` task to build for all platforms. Next, run the `Upload` task for a specific platform

### Katy's notes: 
#### Opening the project (Visual Studio Code)
The PlatformIO home page can be accessed by clicking on the house icon in the bottom left toolbar. In the Quick Access window, click Open Project and navigate to the .ini file that corresponds to your desired project. Select this location to open the project. 
#### Building the project
Click on the checkmark icon in the bottom left toolbar to build the project. The first time I did this, I got an error saying I did not have a Java Development Kit installed. I installed JDK 22.01 and tried again with success.
#### Uploading the project
First, make sure you have the right PlatformIO Project Environment selected. Click on the folder icon in the lower left toolbar to switch environments. I have the rev A kit, so I selected "env:tamagotchi-kit-a (esp8266-tamagotchi)". Then, click on the right-pointing arrow icon in the bottom left toolbar to upload the project. 

### Additional notes
- To activate your pet, you have to configure the clock by pressing the middle button. Otherwise, your pet will not be alive.
- The emulator will save the game status every 5 minutes. You can change that by changing the AUTO_SAVE_MINUTES setting
- The speed of the emulator is a bit slower than the actual Tamagotchi device on AVR, still, it is fun. On ESPs it runs smoothly.
- There are a few costs in the `platformio.ini` that you can adjust to fit your needs:
```
  -D DISPLAY_I2C_ADDRESS=0x3C
  -D SCREEN_WIDTH=128
  -D SCREEN_HEIGHT=64
  -D ENABLE_TAMA_SOUND
  -D ENABLE_TAMA_SOUND_ACTIVE_LOW
  -D ENABLE_AUTO_SAVE_STATUS
  -D ENABLE_LOAD_STATE_FROM_EEPROM
```

### Circuit Diagram
![Circuit Diagram](../main/images/circuit_diagram_01.png)

### Wemos D1 Mini

![image](https://user-images.githubusercontent.com/5459747/192046441-1461c20e-b5f6-4a72-a79b-7815a77e1c00.png)
![image](https://user-images.githubusercontent.com/5459747/192046464-36be5fc8-1893-4b04-a4e0-53a563c3ad33.png)
![image](https://user-images.githubusercontent.com/5459747/192046512-4251114a-d74a-42fc-b67a-0f48a1a26ef4.png)
![image](https://user-images.githubusercontent.com/5459747/192046612-6c835d33-e341-4386-8917-5823d573414d.png)

### License
ArduinoGotchi is distributed under the GPLv2 license. See the LICENSE file for more information.

### Where to buy

You may support my work by ordering the kit on [Tindie](https://www.tindie.com/products/sonocotta/esp8266-tamagotchi-diy-kit/) or [Elecrow](https://www.elecrow.com/esp8266-tamagotchi-diy-kit.html)
