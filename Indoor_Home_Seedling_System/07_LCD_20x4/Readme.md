# 7. LCD Screen

## What's Inside?
### Problem: 
Finally, our system is now under control, but we require real-time insights without having to use the Serial Monitor or PC

### Project Outcome: 
This project aims to show real-time insights of our system using LCD Screen

### Compact microProjects: 
1. ~~Light Intensity meter - BH1750~~
2. ~~Real Time Clock~~
3. ~~MicroSD Card csv data collection~~
4. ~~Temperature and Humidity - DHT22~~
5. ~~Capasitive Soil Moisture sensor~~
6. ~~Relay modules and load wiring~~ (with Insights and Pro Tips)
7. **LCD Screen**

### Tools Needed:
1.   Arduino Mega 2560 Rev3 or any other type ( https://amzn.to/3E3U577 )
2.   USB type A to type B ( https://amzn.to/3xgKFB5 )
3.   Breadboard ( https://amzn.to/3xBzaol )
4.   Power Supply ( https://amzn.to/412eTpo )
5.   Jumper wires ( https://amzn.to/3XqQXc4 )
6.   LCD Screen 20x4 I2C ( https://amzn.to/3XqoR0G )



## Work Inroduction:
In this project, we'll use any Arduino board (I'll use Arduino Mega for further work on the same board) and 20x4 LCD Screen I2C Module. We'll also add all the pervious modules to the final code. 

## Wiring:
LCD I2C module wiring for Arduino Mega will be as the following: 
1.  GND -> GND
2.  VCC -> 5V
3.  SDA -> 20
4.  SCL -> 21

Diagram:

![image](https://user-images.githubusercontent.com/65976495/218754467-45ab5dd4-d861-4ddb-9e22-a65e07f81859.png)



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



