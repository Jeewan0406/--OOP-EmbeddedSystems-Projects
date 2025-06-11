## WiFiSketch 
Include the custom WiFi header file that defines the WifiClass, telling the preprocessor to insert entier contents defined in wifiheader.h file 
such as class declarations, functions prototypes, constant definitions, #define, #if, #endif, etc. instructions, macro definitions etc.the compiler
will know what the class is, what are member variables (_ssid, _pass), methods such as wifi_connect. 
**#include <WiFi.h> & #include "wifiheader.h"** both are **preprocessor directives** that tell the compiler to include a file

NOTE:  Exact header file ***wifiheader.h*** need to be inclused into both *.ino* and *.cpp* file.
- The .cpp file won’t know what to implement → ❌ compiler error
- The .ino file won’t know what class or function you're calling → ❌ “not declared” error
  
Telling the preprocessor to look for the file WiFi.h in the standard library paths provided by the Arduino core or libraries installed via Library Manager or Board Manager.
Standard or third-party libraries like:  

**<WiFi.h>**

**<Wire.h>**

**<Adafruit_Sensor.h>**

Telling the preprocessor, look for the file **wifiheader.h** in the current sketch folder or the folder where my **.ino** or **.cpp** file is located. This is my **user-defined header**

Creating an instance of the class  means making real object in memory ( creates a real object in the computer’s memory) based on class. What the object will contain like data and what it can do like function/methods
Data such as bricks, cement, steels rods, tin sheets, sand etc and instace is the actual house built using those blue print such as functionin/method/feature/action such as 
kitchen for cooking, bathroom for bathing, bedroom for sleeping etc. 

***WiFi.begin()*** → Go to existing WiFi tool, do specific task.

***WiFi(ssid, pass)*** → Create a brand-new WiFi tool and configure it immediately with these details. Create a new WiFi object → immediately run its constructor → configure it with your ssid and password
Specifically for WiFi(ssid, pass):
When we say configure the WiFi with ssid and pass, we are telling the computer:

Here is the WiFi network name (ssid) you should connect to.

Here is the password (pass) needed to join that network.

Use this information to prepare the WiFi tool to start connecting or communicating with that network.
wifi_connect() is a method, not a standalone function.
It belongs to a class or object.
You call it on an object **(WIFI.wifi_connect())** to tell it:
Use this object's stored information and run the connect task.

Imagine you have multiple phones (objects), each with its own contacts and settings. To make a call, you say:
- Phone1.call(number) → calls using Phone1’s contacts and network
- Phone2.call(number) → calls using Phone2’s info
  
Calling just call(number) without specifying which phone to use will make progrem confused and may halisunate 
If you don’t write the object name before the function (e.g., just wifi_connect() instead of WIFI.wifi_connect()), the computer (compiler) will get confused — especially if there are multiple objects of the same class.

Imagine you have two robots:
RobotA knows how to sweep a room
RobotB also knows how to sweep a room
But you say just:
sweep_room()
Now both robots are confused:
Who’s supposed to sweep?
But if you say:
RobotA.sweep_room()
Now it’s clear — only RobotA should do the job, using its own broom and its own memory of which room to clean.

When we create WIFI(ssid, pass), we are building a real, working object inside the computer’s memory. The constructor
is automatically called to make sure everything inside the object is properly set up — just like giving a human legs, hands, 
mouth, and brain — so that the object is ready to be used right away. If something is missing, the constructor makes sure to fix or prepare it immediately.

# wifi_sketch
```C
#include "wifiheader.h"

const char* ssid = "Wokwi-Guest";
const char* pass = "";

wificlass WIFI(ssid, pass);

void setup()
{
  Serial.begin(9600);
  WIFI.wifi_connect();
};

void loop()
{

} 
```
![image](https://github.com/user-attachments/assets/f4533912-fd93-4896-a64b-ba45a4343476)

# wifi_header
```C
// Prevents the header file from being included multiple times
#ifndef WIFIHEADER_H
#define WIFIHEADER_H // This is called an "include guard", if not defined define now.

// Include the WiFi library provided by the ESP32/ESP8266 core.
// This library allows the board to connect to Wi-Fi networks.
#include <WiFi.h>

// Define a custom class named WifiClass that encapsulates Wi-Fi functionality
// This makes the code reusable, organized, and easier to maintain.
class wificlass
{
  public:
  // Constructor: takes Wi-Fi SSID and password as parameters
    // These are passed as 'const char*' because:
    // - SSID and password are strings
    // - const ensures they are not modified inside the class
    wificlass(const char* ssid, const char* pass);
    
    // Public method to initiate Wi-Fi connection
    // This will be called from the main sketch to connect to Wi-Fi
    void wifi_connect();

  private:
    // Private member variables to store SSID and password internally
    // They are 'const char*' because:
    // - Strings are stored as character arrays (C-strings) in low-level C++
    // - const avoids accidental modification
    const char* _ssid;
    const char* _pass;
};

#endif // WIFIHEADER_H  // End of include guard
```


