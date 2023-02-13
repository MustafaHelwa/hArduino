# 6. Relay modules and load wiring

## What's Inside?
### Problem: 
Although I have collected all the necessary readings, being away from home presents a challenge in providing my plants with the required light and water.

### Project Outcome: 
The project aims to overcome the challenge of providing required light and water to indoor plants, even when one is away from home.

### Compact microProjects: 
1. ~~Light Intensity meter - BH1750~~
2. ~~Real Time Clock~~
3. ~~MicroSD Card csv data collection~~
4. ~~Temperature and Humidity - DHT22~~
5. ~~Capasitive Soil Moisture sensor~~
6. **Relay modules and load wiring** (with Insights and Pro Tips)
7. LCD Screen

### Tools Needed:
1.   Arduino Mega 2560 Rev3 or any other type ( https://amzn.to/3E3U577 )
2.   USB type A to type B ( https://amzn.to/3xgKFB5 )
3.   Breadboard ( https://amzn.to/3xBzaol )
4.   Power Supply ( https://amzn.to/412eTpo )
5.   Jumper wires ( https://amzn.to/3XqQXc4 )
6.   8 Relay Module ( https://amzn.to/40UXPBI )
7.   5VDC Water pump ( https://amzn.to/3RWB38d )
8.   LED lights as needed


## Work Inroduction:
In this project, we'll use any Arduino board (I'll use Arduino Mega for further work on the same board) and Relay Module. Since we're only one step before ending our project, we'll also add all the pervious modules in the final code. 

## Wiring:
Relay Module wiring for Arduino Mega will be as the following (I am using 8 Relay Module since I'll expand my light capacity later): 
1.  GND -> GND
2.  VCC -> 5V
3.  IN1 -> 31
4.  IN2 -> 32
5.  IN3 -> 33
6.  IN4 -> 34
7.  IN5 -> 35
8.  IN6 -> 36
9.  IN7 -> 37
10. IN8 -> 38

Diagram:

## Coding: 
### libraries:
Once we finished wiring, we'll use the following code to define our pin. There is no library needed for Relay Module: 
```
                                // all the below numbers are optional based on your loads
const int ValvePin = 31;        // this pin will be used to control Valve
const int LightPin1 = 32;       // this pin will be used to control light#1
const int LightPin2 = 33;       // this pin will be used to control light#2

int lightstatus, valvestatus;   // this int will be used for defining controlled loads status
```
### void setup():
Since we don't have any library, we'll not initiate any library in ```void setup()``` and but we'll define Relay Module pins as outputs and turn them all off as the following: 
```
void setup()
{
  Serial.begin(9600);

  pinMode (ValvePin, OUTPUT );        digitalWrite (ValvePin, LOW);
  pinMode (LightPin1, OUTPUT );        digitalWrite (LightPin1, LOW); 
  pinMode (LightPin2, OUTPUT );        digitalWrite (LightPin2, LOW); 
  pinMode (34, OUTPUT );        digitalWrite (34, LOW); 
  pinMode (35, OUTPUT );        digitalWrite (35, LOW);
  pinMode (36, OUTPUT );        digitalWrite (36, LOW);
  pinMode (37, OUTPUT );        digitalWrite (37, LOW);
  pinMode (38, OUTPUT );        digitalWrite (38, LOW);
}
```
### void loop():
Finally, in the ```void loop()```, we'll read and write soil moisture and delay for 1 second **(please read each line notes for clarification)**: 
```
void loop() 
{  
  // We'll open water once Soil Moisture is less 60% and leave the loop when soil moisture is 80% or above 
  
  if (SoilMoistureValue <= 60.0)
     {
      digitalWrite (ValvePin, HIGH);
      valvestatus = 1;
      
      for (SoilMoistureValue < 80.0)
      {
      digitalWrite ("SM: ");
      digitalWrite (SoilMoistureValue);
      delay (1000);
      }

     }
      else 
        {
        digitalWrite (ValvePin, LOW);
        valvestatus = 0;
        }
        
    if (valvestatus ==1) Serial.println ("Valve Status: Open");
    else Serial.println ("Valve Status: Closed");
  // Light on/off based on time
  if ( rtc.getTime().hour==6 || rtc.getTime().hour==7 || rtc.getTime().hour==8 || rtc.getTime().hour == 9 || rtc.getTime().hour==10 || rtc.getTime().hour==11 || rtc.getTime().hour==12 ||
       rtc.getTime().hour==13 || rtc.getTime().hour==14 || rtc.getTime().hour==15 || rtc.getTime().hour==16 || rtc.getTime().hour==17 || rtc.getTime().hour==18 )
    {
    digitalWrite (LightPin1, LOW);
    digitalWrite (LightPin2, LOW);
    lightstatus = 1;
    } 
    else
      {
        digitalWrite (LightPin1, HIGH);
        digitalWrite (LightPin2, HIGH);
        lightstatus = 0;
      }
    if (lightstatus = 1) Serial.println ("Lights Status: On");
        else Serial.println ("Lights Status: Off");
}
```

## Serial Monitor: 





## Notes:
- You can adjust the desired soil moisture by adjusting the numbersin line83 and line 88
- Light is based on time only but you can control it with ```lux```  


### Pro Tip!!




See you in the next microProject...

[Next: 7. LCD Screen](https://github.com/MustafaHelwa/hArduino/tree/main/Indoor_Home_Seedling_System/07_LCD_20x4)



