# 5. Capasitive Soil Moisture sensor

## What's Inside?
### Problem: 
To effectively water our pots, we need to know when it's required.

### Project Outcome: 
The outcome of this project will be a system for detecting soil moisture, ensuring watering when only it is necessary for our pots.

### Compact microProjects: 
1. ~~Light Intensity meter - BH1750~~
2. ~~Real Time Clock~~
3. ~~MicroSD Card csv data collection~~
4. ~~Temperature and Humidity - DHT22~~
5. **Capasitive Soil Moisture sensor**
6. Relay modules and load wiring (with Insights and Pro Tips)
7. LCD Screen

### Tools Needed:
1.   Arduino Mega 2560 Rev3 or any other type ( https://amzn.to/3E3U577 )
2.   USB type A to type B ( https://amzn.to/3xgKFB5 )
3.   Breadboard ( https://amzn.to/3xBzaol )
4.   Power Supply ( https://amzn.to/412eTpo )
5.   Jumper wires ( https://amzn.to/3XqQXc4 )
6.   Capasitive soil moisture sensor ( https://amzn.to/3Ypcu6d )


## Work Inroduction:
In this project, we'll use any Arduino board (I'll use Arduino Mega for further work on the same board) and Capasitive soil moisture sensor. We'll also need jumpers for wiring. 

## Wiring:
Capasitive soil moisture sensor wiring for Arduino Mega will be as the following: 
1.  GND -> GND
2.  VCC -> 3.3V
3.  AOOT -> A0 (or any analog input pin) 

Diagram:

## Coding: 
### libraries:
Once we finished wiring, we'll use the following code to define our pin. There is no library needed for Soil Moisture sensor (we'll do our own mapping): 
```
#define SoilMoisturePin A0    // or any analog pin used
```
### void setup():
Since we don't have any library, we'll not add any code in ```void setup()``` and it will be as the following: 
```
void setup()
{
  Serial.begin(9600);
}
```
### void loop():
Finally, in the ```void loop()```, we'll read and write soil moisture and delay for 1 second **(please read each line notes for clarification)**: 
```
void loop() 
{  
  float SoilMoistureValue = 0;                           // Starting with zero value to make sure the below is not carried from the last previous reading

  for (int i = 0; i <= 100; i++)                         // the below for loop used to take 101 readings (form 0 to 100) and accumilate the value of readings 
  { 
    SoilMoistureValue = SoilMoistureValue + analogRead(SoilMoisturePin); 
    delay(1); 
  } 
  SoilMoistureValue = SoilMoistureValue/101.0;           // this line calculates the average soil moisture readings recorded in the for loop above
  
  Serial.print("Soil moisture: ");
  SoilMoistureValue = map ( SoilMoistureValue, 575 ,276 ,0, 100);      // mapping the 0% value as the sensor reading; when it is out of water (575 in my case). Followed by 100% value; when it is fully merged in water cup (276 in my case)
    
  Serial.print(SoilMoistureValue);                              
  Serial.println("%");
}
```


### Final Code: 
This is the code result, you can copy it as it is: 

**Test Runs:**
```
#define SoilMoisturePin A0    // or any analog pin used

void setup()
{
  Serial.begin(9600);
}

void loop() 
{  
  float SoilMoistureValue = 0;                           // Starting with zero value to make sure the below is not carried from the last previous reading

  for (int i = 0; i <= 100; i++)                         // the below for loop used to take 101 readings (form 0 to 100) and accumilate the value of readings 
  { 
    SoilMoistureValue = SoilMoistureValue + analogRead(SoilMoisturePin); 
    delay(1); 
  } 
  SoilMoistureValue = SoilMoistureValue/101.0;           // this line calculates the average soil moisture readings recorded in the for loop above
  
  Serial.print("Soil moisture: ");
    
  Serial.print(SoilMoistureValue);                              
  Serial.println("%");
}
```

**Final Run:**
```
#define SoilMoisturePin A0    // or any analog pin used

void setup()
{
  Serial.begin(9600);
}

void loop() 
{  
  float SoilMoistureValue = 0;                           // Starting with zero value to make sure the below is not carried from the last previous reading

  for (int i = 0; i <= 100; i++)                         // the below for loop used to take 101 readings (form 0 to 100) and accumilate the value of readings 
  { 
    SoilMoistureValue = SoilMoistureValue + analogRead(SoilMoisturePin); 
    delay(1); 
  } 
  SoilMoistureValue = SoilMoistureValue/101.0;           // this line calculates the average soil moisture readings recorded in the for loop above
  
  Serial.print("Soil moisture: ");
  SoilMoistureValue = map ( SoilMoistureValue, 575 ,280 ,0, 100);      // mapping the 0% value as the sensor reading; when it is out of water (575 in my case). Followed by 100% value; when it is fully merged in water cup (276 in my case)
    
  Serial.print(SoilMoistureValue);                              
  Serial.println("%");
}
```
## Serial Monitor: 

![image](https://user-images.githubusercontent.com/65976495/218725773-88cd3d17-9e9d-40a1-a11c-b204b4740613.png)




## Notes:
- In ```map(SoilMoistureValue, x, y, 0, 100);``` x will be the value when sensor is in the air and y will be the value when the sensor is in the water
- To get x and y values, comment ```line 68``` and do 2 runs (one in the air and one in the water) and record the values as explained above


### Pro Tip!!
- You can use multiple sensors on different depths and react accordingly



See you in the next microProject...

[Next: 6. Relay modules and load wiring](https://github.com/MustafaHelwa/hArduino/tree/main/Indoor_Home_Seedling_System/06_Relays)



