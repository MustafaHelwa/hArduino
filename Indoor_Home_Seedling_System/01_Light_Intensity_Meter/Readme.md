# 1. Light Intensity meter - BH1750 

## What's Inside?
### Problem: 
Proper lighting is crucial, and to achieve that, we need to measure it. Our first step towards this goal is to create a light intensity meter.

### Project Outcome: 
The outcome of this project is a functioning light intensity meter to accurately measure and ensure proper lighting.

### Compact microProjects: 
1. **Light Intensity meter - BH1750**
2. Real Time Clock
3. MicroSD Card csv data collection
4. Temperature and Humidity - DHT22
5. Capasitive Soil Moisture sensor
6. Relay modules and load wiring (with Insights and Pro Tips)
7. LCD Screen

### Tools Needed:
1.   Arduino Mega 2560 Rev3 or any other type ( https://amzn.to/3E3U577 )
2.   USB type A to type B ( https://amzn.to/3xgKFB5 )
3.   Breadboard ( https://amzn.to/3xBzaol )
4.   Power Supply ( https://amzn.to/412eTpo )
5.   Jumper wires ( https://amzn.to/3XqQXc4 )
6.   Digital Light sensor - BH1750FVI ( https://amzn.to/3IhshP4 )
7.   ~~Real Time Clock Module - DS3231 ( https://amzn.to/3E2z7Fx )~~
8.   ~~Micro SD Card Module ( https://amzn.to/3xfDSYD )~~
9.   ~~Micro SD Card with adaptor - Any capacity ( https://amzn.to/3xl3AuS )~~
10.  ~~DHT22 sensor ( https://amzn.to/3YrYdWC )~~
11.  ~~Capasitive soil moisture sensor ( https://amzn.to/3Ypcu6d )~~
12.  ~~8 Relay Module ( https://amzn.to/40UXPBI )~~
13.  ~~LCD Screen 20x4 I2C ( https://amzn.to/3XqoR0G )~~
14.  ~~5VDC Water pump ( https://amzn.to/3RWB38d )~~
15.  ~~Box (about 240mm x 130mm x 90mm)~~
16.  LED lights as needed
17.  ~~Water bucket with connections~~


## Work Inroduction:
In this project, we'll use any Arduino board (I'll use Arduino Mega for further work on the same board) and BH1750 light sensor. We'll also, need jumpers for wiring. If you're planning to complete the indoor seedling project set, please use breadboard for the following connections:
- 3.3V
- GND
- SCL
- SDA

Having additional pins for those will make it easier in the coming microProjects (see note below).

## Wiring:
BH1750 wiring will be as the following: 
1. VCC  ->  3.3v
2. GND  ->  GND
3. SCL  ->  SCL1 or 21 for ArduinoMega (SCL1 in my case)  //if you're using other boards just check your SCL pin 
4. SDA  ->  SDA1 or 20 for ArduinoMega (SDA1 in my case)  //if you're using other boards just check your SDA pin

Diagram:

## Coding: 
### libraries:
Once we finished wiring, we'll install <BH1750.h> and <Wire.h> libraries and use the following code to define our light meter: 
```
#include <Wire.h>
#include <BH1750.h>
BH1750 lightMeter;
```
### void setup():
Then, we'll initiate both **Wire** and **lightmeter** in the **void setup()** as the following: 
```
void setup()
{
  Serial.begin(9600);
  Wire.begin();
  lightMeter.begin();
}
```
### void loop():
Finally, in the **void loop()**, we'll record meter reading as *float* then print it and delay for 1 second: 
```
void loop() 
{  
  float lux = lightMeter.readLightLevel();                
  
  Serial.print("Light: ");
  Serial.print(lux);
  Serial.println(" lx");
  delay(1000);
}
```

### Final Code: 
This is the code result, you can copy it as it is: 
```
#include <Wire.h>
#include <BH1750.h>
BH1750 lightMeter;

void setup()
{
  Serial.begin(9600);
  Wire.begin();
  lightMeter.begin();
}

void loop() 
{  
  float lux = lightMeter.readLightLevel();                
  
  Serial.print("Light: ");
  Serial.print(lux);
  Serial.println(" lx");
  delay(1000);
}
```

## Serial Monitor: 





## Notes:
- Keep in mind that SCL and SDA pins will be used for RTC and I2C LCD screen. Arduino Mega got 2 pins for each, but smaller boards usually got one only and there is where breadboard is needed. Also, 5.0v or 3.3v will be used for 7 modules in our project, Arduino Mega got plenty of them, while micro boards got only 1 or 2
- Arduino Mega maximum baud rate is (115200) bps, while Uno is only (9600) bps. Check yours board baud rate and put it in ```Serial.begin(9600);``` line 


### Pro Tip!!
**You can always outsource 5.0v and GND using external DC supply. Always check module voltage range before applying external source current.**


See you in the next microProject...

[2. Real Time Clock](https://github.com/MustafaHelwa/hArduino/tree/main/Indoor_Home_Seedling_System/02_RealTimeClock)


