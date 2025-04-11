# PA1010D Lightweight Parsing Library
This library handles device setup and data parsing for the PA1010D GPS for Arduino IDE, and was created as an alternative to the Adafruit GPS library.
The Adafruit GPS library stores many of the data fields supplied by the GPS module, while this library has been designed to output these fields to a higher-performance computer or microcontroller. 
For storing information on a PA1010D GPS module or similar unit, please visit the Adafruit GPS library GitHub page [here](https://github.com/adafruit/Adafruit_GPS).

All data fields are contained in (and setup processes handled) by the PA1010D C++ class object defined in this library.
The parameters are saved in a character buffer with CSV formatting to be printed to a serial monitor and handled by another device.
An example program `gpsExample.ino` is provided to show the basic operation of the library and can be compiled with 437 bytes of dynamic memory and 7372 bytes of program memory occupied on the ATmega328P processor (present in the Arduino Uno).

## Library Features
- Method based polling
- Configurable polling rate at runtime
- All fields stored in a single 64-byte buffer
- End message character handled by GPS object
  
### Saved Data Fields
- Date
- Time
- Latitude
- Longitude
- Satellites
- Elevation (m)
