# 2. Real Time Clock - DS3231 

## What's Inside?
### Problem: 
Accurate timekeeping is also important, and our secondary goal is to create a time and date meter.

### Project Outcome: 
The outcome of this project will be a functioning time and date meter to maintain timekeeping, which is an important secondary goal for further monitoring.

### Compact microProjects: 
1. ~~Light Intensity meter - BH1750~~
2. **Real Time Clock**
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
7.   Real Time Clock Module - DS3231 ( https://amzn.to/3E2z7Fx )


## Work Inroduction:
In this project, we'll use any Arduino board (I'll use Arduino Mega for further work on the same board) and DS3231 Real Time Clock Module. We'll also, need jumpers for wiring. If you're planning to complete the indoor seedling project set, please use breadboard for the following connections:
- 3.3V
- GND
- SCL
- SDA

Again, having additional pins for those will make it easier in the coming microProjects (see note below).

## Wiring:
DS3231 wiring will be as the following: 
1. VCC  ->  3.3v
2. GND  ->  GND
3. SCL  ->  SCL1 or 21 for ArduinoMega (SCL1 in my case)  //if you're using other boards just check your SCL pin 
4. SDA  ->  SDA1 or 20 for ArduinoMega (SDA1 in my case)  //if you're using other boards just check your SDA pin

Diagram:

## Coding: 
### libraries:
Once we finished wiring, we'll install ```<DS3231.h>``` library and use the following code to define our rtc pins: 
```
#include <DS3231.h>
DS3231  rtc(SDA, SCL);                                    // write the used pins in the following sequence(SDA, SCL) 
```
### void setup()
In ```void setup()```, RTC programming is tricky and needs attention, we'll have to initiate **rtc** in the **void setup()** and apply current time and date code that will be deleted (or commented) after the first successful run. It will be as the following:  
```
void setup()
{
  Serial.begin(9600);
  rtc.begin();
   
  // The following lines can be uncommented to set the date and time
  rtc.setDOW(TUESDAY);     // Set Day-of-Week to SUNDAY
  rtc.setTime(13, 52, 00);     // Set the time to 12:00:00 (24hr format)
  rtc.setDate(14, 02, 2023);   // Set the date to January 1st, 2014
}
```

Once the run is successful, the ```void setup()``` code will be adjusted (as will be shown at the end). 

### void loop()
Finally, in the **void loop()**, we'll print current date and time and delay for 1 second: 
```
void loop() 
{    
  Serial.print(rtc.getDOWStr());                            // Send Day-of-Week
  Serial.print(" ");
  Serial.print(rtc.getDateStr());                           // Send date
  Serial.print(" -- ");
  Serial.println(rtc.getTimeStr());                         // Send time
  delay(1000);
}
```

### Final Code:
This is the code result, you can copy it as it is: 

**First Run ONLY:**

```
#include <DS3231.h>
DS3231  rtc(SDA, SCL);

void setup()
{
  Serial.begin(9600);
  rtc.begin();
   
  // The following lines can be uncommented to set the date and time
  rtc.setDOW(TUESDAY);     // Set Day-of-Week to SUNDAY
  rtc.setTime(13, 52, 00);     // Set the time to 12:00:00 (24hr format)
  rtc.setDate(14, 02, 2023);   // Set the date to January 1st, 2014
}

void loop() 
{    
  Serial.print(rtc.getDOWStr());                            // Send Day-of-Week
  Serial.print(" ");
  Serial.print(rtc.getDateStr());                           // Send date
  Serial.print(" -- ");
  Serial.println(rtc.getTimeStr());                         // Send time
  delay(1000);
}
```

**Second and further runs:**

```
#include <DS3231.h>
DS3231  rtc(SDA, SCL);

void setup()
{
  Serial.begin(9600);
  rtc.begin();

  /*
  // The following lines can be uncommented to set the date and time
  rtc.setDOW(TUESDAY);     // Set Day-of-Week to SUNDAY
  rtc.setTime(13, 52, 00);     // Set the time to 12:00:00 (24hr format)
  rtc.setDate(14, 02, 2023);   // Set the date to January 1st, 2014
  */
}

void loop() 
{    
  Serial.print(rtc.getDOWStr());                            // Send Day-of-Week
  Serial.print(" ");
  Serial.print(rtc.getDateStr());                           // Send date
  Serial.print(" -- ");
  Serial.println(rtc.getTimeStr());                         // Send time
  delay(1000);
}
```

## Serial Monitor: 

![image](https://user-images.githubusercontent.com/65976495/218710708-7f7a8a5d-a51f-4aa2-96c9-50c8e35b5893.png)




## Notes:
- RTC first code is for defining date and time. It will keep defining the same information if the 3 line codes has not been removed 
- You can print different forms of date and time, you can refer to library codes 


### Pro Tip!!
You can monitor RTC temperature using   ```Serial.print(rtc.getTemp());```



See you in the next microProject...


[Next: 3. MicroSD Card csv data collection](https://github.com/MustafaHelwa/hArduino/tree/main/Indoor_Home_Seedling_System/03_MicroSD_Card/)


