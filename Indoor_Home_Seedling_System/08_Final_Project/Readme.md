# Ardunio Mega Indoor Home Seedling System - Final Project: 

## What's Inside?
### Problem: 
My passion for indoor plants is hindered by my frequent absences from home, leaving my plants without proper hydration and lighting. 
Finally, we prepared all building blocks for our porject. 

### Project Outcome: 
An automated lighting and irrigation system for my indoor plants.

### Compact microProjects: 
1. ~~Light Intensity meter - BH1750~~
2. ~~Real Time Clock~~
3. ~~MicroSD Card csv data collection~~
4. ~~Temperature and Humidity - DHT22~~
5. ~~Capasitive Soil Moisture sensor~~
6. ~~Relay modules and load wiring (with Insights and Pro Tips)~~
7. ~~LCD Screen~~

### Tools Needed:
1.   Arduino Mega 2560 Rev3 or any other type ( https://amzn.to/3E3U577 )
2.   USB type A to type B ( https://amzn.to/3xgKFB5 )
3.   Breadboard ( https://amzn.to/3xBzaol )
4.   Power Supply ( https://amzn.to/412eTpo )
5.   Jumper wires ( https://amzn.to/3XqQXc4 )
6.   Digital Light sensor - BH1750FVI ( https://amzn.to/3IhshP4 )
7.   Real Time Clock Module - DS3231 ( https://amzn.to/3E2z7Fx )
8.   Micro SD Card Module ( https://amzn.to/3xfDSYD )
9.   Micro SD Card with adaptor - Any capacity ( https://amzn.to/3xl3AuS )
10.  DHT22 sensor ( https://amzn.to/3YrYdWC )
11.  Capasitive soil moisture sensor ( https://amzn.to/3Ypcu6d )
12.  8 Relay Module ( https://amzn.to/40UXPBI )
13.  LCD Screen 20x4 I2C ( https://amzn.to/3XqoR0G )
14.  5VDC Water pump ( https://amzn.to/3RWB38d )
14.  Box (~240mm x 130mm x 90mm)
15.  LED lights as needed
16.  Water bucket with connections


## Work Inroduction:
In this project, we'll use any Arduino board (I'll use Arduino Mega for further work on the same board) and all tools that have been used in the previous microProjects

## Wiring:

**1.  BH1750:**
  - VCC -> 3.3V
  - GND -> GND
  - SCL -> SCL1 or 21 (SCL1 in my case)
  - SDA -> SDA1 or 20 (SDA1 in my case)
  
**2.  RTC:**
  - VCC -> 5.0V
  - GND -> GND
  - SCL -> SCL1 or 21 (SCL1 in my case)
  - SDA -> SDA1 or 20 (SDA1 in my case) 
 
**3.  MicroSD Card Adapter Module:**
  - GND -> GND
  - VCC -> 5.0V
  - MISO -> 50
  - MOSI -> 51
  - SCK -> 52
  - CS -> 53
  
**4.  DHT22**
  - (+) -> 3.3v
  - (-) -> GND
  - Out -> 2 (PWM)
  
**5.  Soil Moisture**
  - GND -> GND
  - VCC -> 3.3V
  - AOUT -> A10
  
**6.  Relays: **
  - ~~GND -> GND~~
  - VCC -> 5V
  - IN1 -> 31
  - IN2 -> 32
  - IN3 -> 33
  - IN4 -> 34
  - IN5 -> 35
  - IN6 -> 36
  - IN7 -> 37
  - IN8 -> 38

**7.  LCD 20x4 I2C:**
  - GND -> GND
  - VCC -> VCC
  - SDA -> 20
  - SCL -> 21  
**Diagram:**

![Diagram](https://user-images.githubusercontent.com/65976495/218754467-45ab5dd4-d861-4ddb-9e22-a65e07f81859.png)



## Coding: 
### libraries:
Once we finished wiring, we'll install <LiquidCrystal_I2C.h> library and use the following code to define our lcd: 
```
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd = LiquidCrystal_I2C(0x27, 20, 4);
```
### void setup():
Then, we'll initiate **lcd** in the ```void setup()```, turn on backlight for visibility, and use ```lcd.setCursor(x,y);``` to move our cursor and print welcoming statement, then use ```lcd.clear();``` to clear the screen as the following: 
```
void setup()
{
  Serial.begin(9600);
  lcd.init();                                              // for 20x4 LCD initialisation
  lcd.backlight();                                         // turning on backlight
  lcd.setCursor(0,0);                                      // setting cursor place
  lcd.print("Hello... ");                                  // Printing on the screen
  lcd.setCursor(0,1);
  lcd.print("System is on");                            
  delay(1000);
  lcd.clear();                                              // cleaing screen
}
```
### void loop():
Finally, in the ```void loop()```, we'll write live data that we collected for and delay for 1 second: 
```
void loop() 
{  
   lcd.clear();                                              // cleaing screen
   lcd.home();                                               // back cursor to home 
   
   lcd.print("Date:");
   lcd.print("14-02-2023");                                  // Send date, check RTC lines
   
   lcd.setCursor(0,1);                                       // setting cursor place
   lcd.print("Time:");
   lcd.print(14:07:35);                                      // Send time, check RTC lines
   lcd.print("          ");
   
   lcd.setCursor(0,2);                                       
   lcd.print("T:");
   lcd.print("25");
   lcd.print("C - H:");
   lcd.print("85.2");
   lcd.print("%");
   
   lcd.setCursor(0,3);                                       
   lcd.print("Light:");
   lcd.print("17569");
   lcd.print(" lx");
 }
```

## Serial Monitor: 





## Notes:
- Lines73, 77, 82, 84, and 89 will be used with sensor variables that has been collected (those numbers are only for demonstration)


### Pro Tip!!
- LCD screens are never small. You can display more data if needed, simply write your first insights, delay for 3 seconds, clear your screen, and write the next insights 



See you in the final Project...

[Next: 8. Final Project](https://github.com/MustafaHelwa/hArduino/tree/main/Indoor_Home_Seedling_System/08_Final_Project)






Stay safe and Have Fun :)
