# 4. Temperature and Humidity - DHT22

## What's Inside?
### Problem: 
Monitoring temperature and humidity is important for data tracking, even when we're indoors

### Project Outcome: 
The outcome of this project will be a system for tracking indoor temperature and humidity, to ensure accurate surrounding climate monitoring.

### Compact microProjects: 
1. ~~Light Intensity meter - BH1750~~
2. ~~Real Time Clock~~
3. ~~MicroSD Card csv data collection~~
4. **Temperature and Humidity - DHT22**
5. Capasitive Soil Moisture sensor
6. Relay modules and load wiring (with Insights and Pro Tips)
7. LCD Screen

### Tools Needed:
1.   Arduino Mega 2560 Rev3 or any other type ( https://amzn.to/3E3U577 )
2.   USB type A to type B ( https://amzn.to/3xgKFB5 )
3.   Breadboard ( https://amzn.to/3xBzaol )
4.   Power Supply ( https://amzn.to/412eTpo )
5.   Jumper wires ( https://amzn.to/3XqQXc4 )
6.   DHT22 sensor ( https://amzn.to/3YrYdWC )


## Work Inroduction:
In this project, we'll use any Arduino board (I'll use Arduino Mega for further work on the same board) and DHT22 module. We'll also need jumpers for wiring. 

## Wiring:
DHT22 wiring for Arduino Mega will be as the following: 
1.  (+) -> 3.3v
2.  (-) -> GND
3.  Out -> 2 (or any other PWM pin)  

**Diagram:**

![image](https://user-images.githubusercontent.com/65976495/218758450-332a9ee3-5eef-4ac4-8b07-fc5a8024eeb4.png)

(Note: DHT22 sensor above uses 4 pins, while our DHT22 module is only 2 pins)







## Coding: 
### libraries:
Once we finished wiring, we'll install ```<DHT.h>``` library and use the following code to define our used pin, sensor type, and dht variable: 
```
#include <DHT.h>
#define DHTPin 2                                        // any PWM pin works (2 in my case)
#define DHTType DHT22                                   // DHT22 or DHT11 (DHT22 in my case)
DHT dht = DHT(DHTPin, DHTType);
```
### void setup():
Then, we'll initiate **dht** and in the ```void setup()``` as the following: 
```
void setup()
{
  Serial.begin(9600);
  dht.begin();
}
```
### void loop():
Finally, in the ```void loop()```, we'll read and write humidity and temperatture and delay for 1 second: 
```
void loop() 
{  
  float h = dht.readHumidity();
  float t = dht.readTemperature();

  Serial.print("Temp: ");
  Serial.print(t);
  Serial.print(" C, Humidity: ");
  Serial.print(h);
  Serial.println("%");
  delay (1000);
}
```


### Final Code: 
This is the code result, you can copy it as it is: 
```
#include <DHT.h>
#define DHTPin 2                                        // any PWM pin works (2 in my case)
#define DHTType DHT22                                   // DHT22 or DHT11 (DHT22 in my case)
DHT dht = DHT(DHTPin, DHTType);



void setup()
{
  Serial.begin(9600);
  dht.begin();
}

void loop() 
{  
  float h = dht.readHumidity();
  float t = dht.readTemperature();

  Serial.print("Temp: ");
  Serial.print(t);
  Serial.print(" C, Humidity: ");
  Serial.print(h);
  Serial.println("%");
  delay (1000);
}
```
## Serial Monitor: 


![image](https://user-images.githubusercontent.com/65976495/218720808-d6c2bf48-7f4a-4003-b4bd-0f7d2f5bd336.png)




## Notes:
- you can use the following code to transfer temperature from °C to °F ```h = ((h*(9/5))+32);```
- If you're using other dht22 sensors, connection will be different (plane sensors come with4 pins and resistor will be needed)


### Pro Tip!!
- Using ready to use modules will minimize your wiring headache 



See you in the next microProject...

[Next: 5. Capasitive Soil Moisture sensor](https://github.com/MustafaHelwa/hArduino/tree/main/Indoor_Home_Seedling_System/05_Soil_Moisture)



