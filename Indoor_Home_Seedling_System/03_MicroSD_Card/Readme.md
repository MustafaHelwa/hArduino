# 3. MicroSD Card csv data collection

## What's Inside?
### Problem: 
After collecting data, it's crucial to securely store it for future reference.

### Project Outcome: 
The outcome of this project will be a storage system for the collected data in csv form, ensuring its availability for future reference and analysis.

### Compact microProjects: 
1. ~~Light Intensity meter - BH1750~~
2. ~~Real Time Clock~~
3. **MicroSD Card csv data collection**
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
6.   Micro SD Card Module ( https://amzn.to/3xfDSYD )
7.   Micro SD Card with adaptor - Any capacity ( https://amzn.to/3xl3AuS )


## Work Inroduction:
In this project, we'll use any Arduino board (I'll use Arduino Mega for further work on the same board) and Micro SD Card Module. We'll also need jumpers for wiring. 
Before wiring, connect your SD card to your PC and format it in ```fat32``` type then plug it in you Micro SD Card Module and follow the below: 


## Wiring:
Micro SD Card Module wiring for Arduino Mega will be as the following (or check your alternative pins for other boards): 
1. VCC  -> 5.0v
2. GND  -> GND
3. MISO -> 50
4. MOSI -> 51
5. SCK  -> 52
6. CS   -> 53

Diagram:

## Coding: 
### libraries:
Once we finished wiring, we'll install ```<SPI.h>``` and ```<SD.h>``` libraries and use the following code to define our data file: 
```
#include <SPI.h>
#include <SD.h>
File dataFile;
```
### void setup():
Then, we'll initiate **SD** and create our **data.text** file in the ```void setup()``` as the following: 
```
void setup()
{
  SD.begin(53);                                           // CS pin number 53 in my case
  dataFile = SD.open("data.txt", FILE_WRITE);             // to create new file on SD card as text
}
```
### void loop():
Finally, in the ```void loop()```, we'll write our collected data from project 1 and 2 as **csv** format and delay for 1 second: 
```
void loop() 
{  
   lcd.clear();                                              // cleaing screen
   lcd.home();                                               // back cursor to home 
   
   lcd.print("Date:");
   lcd.print(rtc.getDateStr());                              // Send date, check RTC lines
   
   lcd.setCursor(0,1);                                       // setting cursor place
   lcd.print("Time:");
   lcd.print(rtc.getTimeStr());                              // Send time, check RTC lines
   lcd.print("          ");
   
   lcd.setCursor(0,2);                                       
   lcd.print("T:");
   lcd.print(int(t));
   lcd.print("C - H:");
   lcd.print(int(h));
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

   lcd.setCursor(17,2);
   lcd.print("SDC");
   lcd.setCursor(17,3);
}
```

### Final Code: 
This is the code result, you can copy it as it is: 
```
#include <SPI.h>
#include <SD.h>
File dataFile;

void setup()
{
  SD.begin(53);
  dataFile = SD.open("data.txt", FILE_WRITE);            
}

void loop() 
{  
   lcd.clear();
   lcd.home();    
   lcd.print("Date:");
   lcd.print(rtc.getDateStr());
   lcd.setCursor(0,1);
   lcd.print("Time:");
   lcd.print(rtc.getTimeStr());
   lcd.print("          ");
   
   lcd.setCursor(0,2);                                       
   lcd.print("T:");
   lcd.print(int(t));
   lcd.print("C - H:");
   lcd.print(int(h));
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

   lcd.setCursor(17,2);
   lcd.print("SDC");
   lcd.setCursor(17,3);
}
```

## Serial Monitor: 





## Notes:
- This project will not work without adding project 1 and project 2 variables. But, you can remove them and add your own lines for testing
- You can adjust the cursor position using ```lcd.setCursor(x,y)``` where x is the column number and y is the row number starting from 0


### Pro Tip!!
Using I2C bus modules will always minimize your wiring and coding efforts. 



See you in the next microProject...

[Next: 4. Temperature and Humidity - DHT22](https://github.com/MustafaHelwa/hArduino/tree/main/Indoor_Home_Seedling_System/04_TempHumidity)



