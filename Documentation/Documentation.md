# PA1010D Lightweight Parsing Library Documentation
Created By: Brendan Bovenschen, December 27, 2024\
Last Modified By: Brendan Bovenschen, December 27, 2024

## PA1010D (Class)
This object type handles serial communication with a GPS module at the pin values and polling rate set at object instantiation.

### Properties

#### gpsBuf *char\**
```cpp
char* gpsBuf[64] = {0}
```
64-byte buffer for GPS data fields stored in CSV (Comma Separated Value) format.\
**Example Value**
```cpp
// Date,Time,Latiude,Longitude,Satellites,Elevation (m)<',' or '\n'> based on endLine parameter
26/11/2024,21:04:07.000,36°10'01.69"N,097°04'09.96"W,5,316.7,
```


#### gpsComplete *bool*
```cpp
bool gpsComplete = false
```
Flag for completion state of GPS data stored in `gpsBuf`. When true, all data values should be filled in `gpsBuf`.

#### readingGPS *bool*
```cpp
bool readingGPS = true
```
Flag for the read status of GPS object. If true, no other processes should take place in the `loop()` of the arduino so that no characters are missed from the serial connection to the GPS module. Below is a sample loop structure that follows this paradigm.\
**Example**
```cpp
if(!gps.readingGPS && gps.gpsComplete)
  {
    Serial.print(gps.gpsBuf);
  }
```
Data is printed to the Arduino serial port when the GPS data buffer is filled and data is not being read from the GPS module.


### Public Methods

#### PA1010D *PA1010D*
```cpp
PA1010D PA1010D(uint8_t tx, uint8_t rx, uint16_t pollPeriodMS = 1000, bool endLine = false)
```
Constructor for the `PA1010D` object class. `tx` and `rx` refer to the transmit and recieve serial pins on the GPS module and should be matched. reciprocals should NOT be used. `pollPeriodMS` determines polling period of the GPS in milliseconds. The minimum supported polling rate for similar modules is 10Hz (100 ms). `endLine` determines end character of `gpsBuf` in CSV formatting. If true, the character will be the ASCII newline character '\n'. If false, another CSV value is expected and the character printed will be a comma ','. 

#### SetupGPS *void*
```cpp
void SetupGPS()
```
Setup method must be called before the data will be logged to the GPS buffer `gpsBuf`. This method opens the serial connection and enters commands to the GPS module.
**Example**
```cpp
PA1010D gps(9, 8, 200, false);

void setup() 
{
  gps.SetupGPS();
}
```

#### PollGPS *void*
```cpp
void PollGPS()
```
Reads a character from the GPS serial connection, writes data to `gpsBuf` on completion, and handles state variables. This method must be called on each iteration of the `loop()` function so no characters are lost. Below is an example system for reading data from the GPS module.
**Example**
```cpp
void loop() 
{
  gps.PollGPS();	// reads a character and handles fields

  // Ensure the GPS is not being read and the buffer is complete
  if(!gps.readingGPS && gps.gpsComplete)
  {
    Serial.print(gps.gpsBuf);
  }
}
```
