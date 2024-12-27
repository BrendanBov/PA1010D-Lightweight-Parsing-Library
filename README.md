# PA1010D Lightweight Parsing Library
This library handles setup function and data parsing for the PA1010D GPS for Arduino IDE. 
All data fields are contained in and setup processes handled by the PA1010D object.
The paramaters are saved in a character buffer with CSV formatting to be printed to a
serial montitor to be handled by another device. 

### Saved Data Fields
- Date
- Time
- Latiude
- Longitude
- Satellites
- Elevation (m)

## Library Features
- Method based polling
- Configurable polling rate at runtime
- All fields stored in single 64-byte buffer
- End message character handled by GPS object