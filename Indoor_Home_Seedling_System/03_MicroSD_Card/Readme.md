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

## SD Card Format: 

![image](https://user-images.githubusercontent.com/65976495/218712307-29a40c96-6f37-45c6-94bf-2118855744dc.png)



![image](https://user-images.githubusercontent.com/65976495/218712379-5f3cc0dd-1eb3-4935-9a7a-dac06ac2ccb1.png)



![image](https://user-images.githubusercontent.com/65976495/218718283-12e8b520-90e2-4335-9fb2-0e3bd9146b7e.png)



## Wiring:
Micro SD Card Module wiring for Arduino Mega will be as the following (or check your alternative pins for other boards): 
1. GND  -> GND
2. VCC  -> 5.0v
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
  Serial.begin(9600);
  SD.begin(53);                                           // CS pin number 53 in my case
  dataFile = SD.open("data.txt", FILE_WRITE);             // to create new file on SD card as text
}
```
### void loop():
Finally, in the ```void loop()```, we'll write our collected data from project 1 and 2 as **csv** format and delay for 1 second: 
```
void loop() 
{  
    dataFile = SD.open("data.txt", FILE_WRITE);                         // Opening data file on SD card to start writing
   
    if (dataFile) 
    {
    
    Serial.print("Recording on SD Card... ");       // to keep tracking that file is available 
    
    dataFile.print("13-2-2023"); 
    dataFile.print (", ");                          // , since I'll use excel csv file later
    dataFile.print ("15:27:31");                    // recording full time (hh:mm:ss)
    dataFile.print(", " );
    dataFile.print("25.17");
    dataFile.print(", " );
    dataFile.print("17695.125");                    // recording lux
    dataFile.println();                             // new line
    dataFile.close();                               // close the file

    Serial.println("Recording done :)");
  }
  else                                              // if recording on SD card failed
    {
      Serial.println("Error recording data!!!");
    }
}
```


### Final Code: 


## Serial Monitor: 





## Notes:
- This project will not work without adding project 1 and project 2 variables. But, you can remove them and add your own lines for testing
- You can track recording failure using serial monitor as shown the end of the loop above 


### Pro Tip!!
Saving data in a *.txt* file separated by *", " (comma followed by space)* will make it convenient for importing into Excel for data plotting and analysis.



See you in the next microProject...

[Next: 4. Temperature and Humidity - DHT22](https://github.com/MustafaHelwa/hArduino/tree/main/Indoor_Home_Seedling_System/04_TempHumidity)



