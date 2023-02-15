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
  
**6.  Relays:**
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

![Diagram](https://user-images.githubusercontent.com/65976495/219017965-fa85c88f-7b51-4d4b-a701-aa686602d66d.png)



## Coding: 
### libraries:
Once we finished wiring, we'll install all below libraries and use the following code to define  variables for our modules: 
```
// Setup for BH1750: 
#include <Wire.h>
#include <BH1750.h>
BH1750 lightMeter;

// Setup for rtc:
#include <DS3231.h>
DS3231  rtc(SDA, SCL);                                    // write the used pins in the following sequence(SDA, SCL) 

// Setup for SD card:
#include <SPI.h>
#include <SD.h>
File dataFile;                                           // to setup read/write variable 

// Setup for DHT22
#include <DHT.h>
#define DHTPin 2                                        // any PWM pin works (2 in my case)
#define DHTType DHT22                                   // DHT22 or DHT11 (DHT22 in my case)
DHT dht = DHT(DHTPin, DHTType);

// Setup for Soil Moisture sensor 
#define SoilMoisturePin A10 

// Setup for LCD I2C 
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd = LiquidCrystal_I2C(0x27, 20, 4);

// Relays; define each relay output by the connected item name for further control
const int ValvePin = 31;
const int LightPin1 = 32; 
const int LightPin2 = 33;
```

Also, well add integers for relay loads status: 
```
int lightstatus, valvestatus;
```

### void setup():
Then, we'll initiate our modules in the ```void setup()``` as the following: 
```
void setup()
{

  Serial.begin(9600);
  Wire.begin();                                           // for BH1750
  lightMeter.begin();                                     // for BH1750
  rtc.begin();                                            // for rtc
  dht.begin();                                            // for DHT22
  
  SD.begin(53);                                           // for Sd Card (CS pin number 53 in my case)
  dataFile = SD.open("data.txt", FILE_WRITE);             // to create new file on SD card

  lcd.init();                                              // for 20x4 LCD initialisation
  lcd.backlight();                                         // turning on backlight
  lcd.setCursor(0,0);                                      // setting cursor place
  lcd.print("Hello... ");                                  // Printing on the screen
  lcd.setCursor(0,1);
  lcd.print("System is on");                            
  delay(1000);
  lcd.clear();                                              // cleaing screen
 
  /*
  // The folHIGHing lines can be uncommented to set the date and time
  rtc.setDOW(SUNDAY);     // Set Day-of-Week to SUNDAY
  rtc.setTime(18, 59, 00);     // Set the time to 12:00:00 (24hr format)
  rtc.setDate(14, 2, 2023);   // Set the date to January 1st, 2014
  */

  // Setup relay output pins (Note that those will be used as relays to take on/off actions where needed and I'll not be using all of them)
    pinMode (31, OUTPUT );        digitalWrite (31, LOW);
    pinMode (32, OUTPUT );        digitalWrite (32, LOW); 
    pinMode (33, OUTPUT );        digitalWrite (33, LOW); 
    pinMode (34, OUTPUT );        digitalWrite (34, LOW); 
    pinMode (35, OUTPUT );        digitalWrite (35, LOW);
    pinMode (36, OUTPUT );        digitalWrite (36, LOW);
    pinMode (37, OUTPUT );        digitalWrite (37, LOW);
    pinMode (38, OUTPUT );        digitalWrite (38, LOW); 

  Serial.println(F("Setup done"));                        // tagging that setup has been done without errors in monitor

}
```


### void loop():
Finally, in the ```void loop()```, we'll do our magic:



```
void loop() 
{
  Serial.println("Loop Start");                           // tagging Void loop start in monitor
  
/*############################################################################*/


  // for rtc time:
   
  Serial.print(rtc.getDOWStr());                            // Send Day-of-Week
  Serial.print(" ");
  Serial.print(rtc.getDateStr());                           // Send date
  Serial.print(" -- ");
  Serial.println(rtc.getTimeStr());                         // Send time

  
/*############################################################################*/

 
  // for BH1750 (lux):
  
  float lux = lightMeter.readLightLevel();                
  
  Serial.print("Light: ");
  Serial.print(lux);
  Serial.println(" lx");

 
/*############################################################################*/

  // for DHT22 (Temp and Humidity):
  
  float h = dht.readHumidity();
  float t = dht.readTemperature();

  Serial.print("Temp: ");
  Serial.print(t);
  Serial.print(" C, Humidity: ");
  Serial.print(h);
  Serial.println("%");

  
/*############################################################################*/

  // for soil moisture sensor 
  
  float SoilMoistureValue = 0;                                // Starting with zero value to make sure the beHIGH is not carried from the last previous reading

  for (int i = 0; i <= 100; i++)                              // the beHIGH for loop used to take 101 readings (form 0 to 100) and accumilate the value of readings 
  { 
    SoilMoistureValue = SoilMoistureValue + analogRead(SoilMoisturePin); 
    delay(1); 
  } 
  SoilMoistureValue = SoilMoistureValue/101.0;                 // this line calculates the average soil moisture readings recorded in the for loop above
  
  Serial.print("Soil moisture: ");
  
  SoilMoistureValue = map ( SoilMoistureValue, 585 ,275 ,0, 100);     // mapping the 0% value as the sensor reading; when it is out of water (575 in my case). Followed by 100% value; when it is fully merged in water cup (276 in my case)
  
  Serial.print(SoilMoistureValue);                              
  Serial.println("%");
  

/*############################################################################*/

  // taking actions (relay outputs)

  if (SoilMoistureValue >= 60.0)
     {
      digitalWrite (ValvePin, LOW);
      valvestatus = 1;
     }
      else 
        {
        digitalWrite (ValvePin, HIGH);
        valvestatus = 0;
        }
        
    if (valvestatus ==1) Serial.println ("Valve Status: Open");
    else Serial.println ("Valve Status: Closed");
  // Light on/off based on time
  if ( rtc.getTime().hour==6 || rtc.getTime().hour==7 || rtc.getTime().hour==8 || rtc.getTime().hour == 9 || rtc.getTime().hour==10 || rtc.getTime().hour==11 || rtc.getTime().hour==12 ||
       rtc.getTime().hour==13 || rtc.getTime().hour==14 || rtc.getTime().hour==15 || rtc.getTime().hour==16 || rtc.getTime().hour==17 || rtc.getTime().hour==18 )
    {
    digitalWrite (LightPin1, HIGH);
    digitalWrite (LightPin2, HIGH);
    lightstatus = 1;
    } 
    else
      {
        digitalWrite (LightPin1, LOW);
        digitalWrite (LightPin2, LOW);
        lightstatus = 0;
      }
    if (lightstatus = 1) Serial.println ("Lights Status: On");
        else Serial.println ("Lights Status: Off");
/*############################################################################*/

  // Setting LCD screen write
 
   lcd.clear();                                              // cleaing screen
   lcd.home();                                               // back cursor to home 
   
   lcd.print("Date:");
   lcd.print(rtc.getDateStr());                              // Send date, check RTC lines
   
   lcd.setCursor(0,1);                                       // setting cursor place
   lcd.print("Time:");
   lcd.print(rtc.getTimeStr());                            // Send time, check RTC lines
   lcd.print("          ");
   
   lcd.setCursor(0,2);                                       
   lcd.print("T:");
   lcd.print(int(t));
   lcd.print("C H:");
   lcd.print(int(h));
   lcd.print("% ");

   lcd.print(" SM:");
   lcd.print(int(SoilMoistureValue));
   lcd.print("%");
   
   lcd.setCursor(0,3);                                       
   lcd.print("Light:");
   lcd.print(int(lux));
   lcd.print(" lx");
   
   lcd.setCursor(17,0);
   lcd.print("L:");
   if (lightstatus == 1) lcd.print("H");
   else lcd.print("L");

   lcd.setCursor(17,1);
   lcd.print ("V:");
   if (valvestatus == 1) lcd.print("H");
   else lcd.print("L");

   lcd.setCursor(15,3);

/*############################################################################*/


  // for SD card writing:
  
  dataFile = SD.open("data.txt", FILE_WRITE);                         // Opening data file on SD card to start writing
   
  if (dataFile ) 
  {
    Serial.print("Recording on SD Card... ");
    
    // Record date every day and time (clock) every 6 hours
      if ( rtc.getTime().hour==0 &&  rtc.getTime().min==0 && rtc.getTime().sec <20 ) 
          {dataFile.print(rtc.getDateStr());}
      
            else if (rtc.getTime().hour==6 &&  rtc.getTime().min==0 && rtc.getTime().sec <20 || rtc.getTime().hour== 12 &&  rtc.getTime().min==0 && rtc.getTime().sec <20 ||
                rtc.getTime().hour==18 &&  rtc.getTime().min==0 && rtc.getTime().sec <20 )
            { dataFile.print(rtc.getTimeStr());   }
            
    dataFile.print (", ");                          // , since I'll use excel csv file later (you can use any separator such as \t for tabs \n for lines or anything you prefer
    dataFile.print (rtc.getTimeStr());              // recording full time (hh:mm:ss)
    dataFile.print(", " );
    dataFile.print(rtc.getTemp());
    dataFile.print(", " );
    dataFile.print(h);                              // recording humidity
    dataFile.print(", ");
    dataFile.print(t);                              // recording temperature
    dataFile.print(", " );                          
    dataFile.print(SoilMoistureValue);              // recording soil moisture 
    dataFile.print(", " );
    dataFile.print(lux);                          // recording lux
    dataFile.print(", " );                          
    dataFile.print(valvestatus);                    // recording valve state
    dataFile.print(", ");
    dataFile.print(lightstatus);                    // recording lights state
    dataFile.println();                             // new line
    dataFile.close(); // close the file

    Serial.println("Recording done :)");
    lcd.print("SDOK)");
  }
  else // if recording on SD card failed
    {
      Serial.println("Error recording data!!!");
      lcd.print("SDERR");
    }
  
  
/*############################################################################*/


  delay (1000);
  Serial.println();

}```

## Serial Monitor: 





## Notes:
- Lines73, 77, 82, 84, and 89 will be used with sensor variables that has been collected (those numbers are only for demonstration)


### Pro Tip!!
- LCD screens are never small. You can display more data if needed, simply write your first insights, delay for 3 seconds, clear your screen, and write the next insights 



See you in the final Project...




Stay safe and Have Fun :)
