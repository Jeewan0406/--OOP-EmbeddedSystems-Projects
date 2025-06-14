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

# Header file
```c
const char* ssid, const char* pass
```
This variable will not hold a direct value, but rather an address to a value of a specific type. 
**ssid**/**pass** is pointer to const char data type. 

![image](https://github.com/user-attachments/assets/0ceab312-0438-473c-9365-156273d66b45)
![image](https://github.com/user-attachments/assets/8648314c-a44d-4cdf-843c-00f3c817ebdc)

Following are the list of contenst decleared/defined in header file:
1.  Include guards (#ifndef / #define or #pragma once)

2.  Core Wi‑Fi header (<WiFi.h> or <ESP8266WiFi.h>)

3. Protocol headers (WiFiClient.h, WiFiServer.h, WiFiUdp.h)

4. Mode-specific headers (WiFiSTA.h, WiFiAP.h, WiFiScan.h, etc.)

5. Definition of WiFiClass and external WiFi object, decleare class name with methods/functions inside the class

6. Declared coonstructore insdie the class.

```c
wificlass(const char* ssid, const char* pass);
```
Declaration of constructor––it tells the compiler “this constructor exists,” but doesn’t give its code (body).

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
# Implementation file
# wificpp.cpp
The compiler needs to know that the definition in the .cpp matches exactly what you declared in the header.

Repeating (const char* ssid, const char* pass) ensures the types, order, and const-correctness match (important even if const can sometimes be optional) 

**ssid & pass** are passed temporarily during object creation. The actual ssid and pass characters are stored permanently in Flash Memory as string literals (sequence of characters enclosed in double quotes (" "), representing a fixed value directly in your source code.) 
The ssid and pass parameters within the constructor (wificlass::wificlass(const char* ssid, const char* pass)) are indeed temporary pointer variables. These temporary pointer variables hold the memory addresses of the string literals in Flash. These temporary pointer variables exist only on the stack (in SRAM) for the brief duration that the constructor function is executing. As soon as the constructor finishes executing, these temporary ssid and pass parameter variables are popped off the stack and their memory in SRAM is reclaimed. Their values (the addresses they held) are effectively "erased" or become meaningless because the memory space is now free for other uses.

when constructor special function is running it will automatically create memory/stack frame (dedicated block of memory for that specific function call)  is allocated in SRAM using the pointer variable. When the constructor is called, a stack frame is allocated in SRAM. Within this stack frame, memory is reserved for the constructor's local variables, including its parameters (ssid and pass). These parameters are indeed pointer variables.The parameters (ssid and pass) hold the values (memory addresses of the string literals in Flash) temporarily while the constructor is active. These values are then copied into the object's permanent member variables (_ssid and _pass).This is the essence of stack memory management. Once the constructor's execution completes, its stack frame is "popped," and the memory it occupied (including the temporary ssid and pass parameter variables) is immediately made available for other functions to use. The data itself might still be there briefly, but the memory is no longer considered in use by your program and can be overwritten.

The call stack efficiently manages memory for local variables and function calls by automatically creating temporary storage when a function starts and clearing it away when the function finishes. This push-and-pop system quickly reuses memory, ensuring your program runs smoothly without needing complex manual memory cleanup for every small task.
```c
#include "wifiheader.h" // Include the custom header file for wificlass declarations.
                        // This makes the wificlass definition (its structure and
                        // function prototypes) available to this source file.

#include <WiFi.h>       // Include the standard Arduino WiFi library.
                        // This provides access to functions like WiFi.begin(),
                        // WiFi.status(), WL_CONNECTED, WiFi.localIP(), etc.,
                        // which are necessary for WiFi operations on ESP32.

// Constructor definition for the wificlass.
// This special member function is automatically called when a wificlass object is created.
// Its purpose is to initialize the object's state (its member variables).
//
// Parameters:
//   ssid: A pointer to a constant character array (C-style string) representing the WiFi SSID.
//         The 'const' keyword ensures that the string pointed to cannot be modified through this pointer.
//   pass: A pointer to a constant character array (C-style string) representing the WiFi password.
//         The 'const' keyword ensures that the string pointed to cannot be modified through this pointer.
wificlass::wificlass(const char* ssid, const char* pass)
{
  // Initialize the private member variable '_ssid' with the value of the 'ssid' parameter.
  // 'this->' explicitly refers to the member variable of the current object.
  // In this case, 'ssid' (parameter) contains a memory address (e.g., 0x1000 in Flash).
  // '_ssid' (member variable) will now store that same memory address, effectively pointing
  // to the same SSID string literal in Flash memory.
  this->_ssid = ssid; // Analogy: self._ssid = ssid in Python (assigns the value)

  // Initialize the private member variable '_pass' with the value of the 'pass' parameter.
  // Similar to _ssid, '_pass' will store the memory address of the password string literal in Flash.
  this->_pass = pass;
}

// Definition of the 'wifi_connect' member function of the wificlass.
// This function handles the process of connecting the ESP32 to the WiFi network.
void wificlass::wifi_connect()
{
  // Initiate the WiFi connection using the stored SSID and password.
  // WiFi.begin() is a non-blocking function; it starts the connection attempt
  // but doesn't wait for it to complete.
  WiFi.begin(this->_ssid, this->_pass); // Use 'this->' to access the object's private members.

  // Enter a loop to continuously check the WiFi connection status.
  // The loop continues as long as the WiFi status is NOT 'WL_CONNECTED'.
  // WL_CONNECTED is an enumeration constant indicating a successful connection.
  while (WiFi.status() != WL_CONNECTED)
  {
    // Pause program execution for 1000 milliseconds (1 second).
    // This delay is important to prevent the loop from running too fast,
    // consuming excessive CPU cycles, and to allow the WiFi module time to connect.
    delay(1000);

    // Print a message to the Serial Monitor indicating that the connection is in progress.
    Serial.println("Connecting to WiFi...");
  }

  // Once the loop is exited, it means WiFi.status() IS WL_CONNECTED.
  // Print a success message to the Serial Monitor.
  Serial.println("Connected to WiFi!");

  // Print the local IP address assigned to the ESP32 by the router.
  // This is useful for accessing the ESP32 over the network.
  Serial.println(WiFi.localIP());
}

```


