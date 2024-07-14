# Vindriktning-ESP-Home-Prensence
Integrating the Vindriktning air quality sensor with ESP Home and adding temprature, humidity, presure, light level and mm-wave presence sensing.

## Components used
- [Vindriktning air quality sensor](https://www.ikea.com/nl/en/p/vindriktning-air-quality-sensor-70498242/)
- [BH1750 (Ambient Light)](https://esphome.io/components/sensor/bh1750.html)
- [LD2410 (mm-Wave Presence)](https://esphome.io/components/sensor/ld2410.html)
- [AHT20 (Temperature+Humidity)](https://esphome.io/components/sensor/aht10.html) + [BMP280 (Temperature+Pressure)](https://esphome.io/components/sensor/bmp280)
- [Seeed Studio XIAO ESP32C3](https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/)

## Notes
- The XIAO only has 1 UART pair available. Since the air sensor (9600) and the mm-wave sensor (256000) have different baud rates we need to add an aditional UART pair using [software UART](https://esphome.io/components/uart#uart). Since the baud rate of the air sensor is lower we will connect this to the software UART. 

## Pinout and pins used
![esp pinout](https://files.seeedstudio.com/wiki/XIAO_WiFi/pin_map-2.png)
Image from [wiki](https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/)

| Pin | Use | Sensor |
|-----|-----|--------|
| D4  | SDA (I2C)    |    BH1750, AHT20, BMP280    |
| D5  | SCL (I2C)    |    BH1750, AHT20, BMP280    |
| D6  | TX (UART 256000)    |    LD2410    |
| D7  | RX (UART 256000)    |    LD2410    |
| D8  | TX (UART 9600)    |    Vindriktning    |
| D9  | RX (UART 9600)    |    Vindriktning    |

## Voltages
- LD2410 : 5V
- BH1750 : 3-5V
- AHT20+BMP280 : 5V

## Inspiration and sources
- https://esphome.io/components/sensor/pm1006.html
- https://www.espboards.dev/blog/smarter-ikea-vidriktning-esphome/
- https://smarthomescene.com/diy/diy-presence-sensor-with-hi-link-ld2410-and-esp32-for-home-assistant/
