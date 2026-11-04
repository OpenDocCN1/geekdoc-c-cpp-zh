```
```cpp
/*------------------------------------------------
 *          SERIAL INTERFACE TO RASPBERRY PI
 *          =========================
 * This program receives a message from Raspberry Pi and
 * then replies with another message
 *
 * Author: Dogan Ibrahim
 * File : ARDUINOSerial
 * DATE : December 2020
 *------------------------------------------------*/

#include <SoftwareSerial.h>
SoftwareSerial MySerial(6, 7);        // RX, TX

//
// Set Baud rates
//
void setup()
{
    Serial.begin(9600);        // Serial monitor
    MySerial.begin(9600);     // Software serial
}

//
// Receive msg from Raspberry Pi and reply
//
void loop()
{
    char c = 0;

    while(!MySerial.available());         // If no data wait
    while(c != '\n')                    // If not newline
    {
        if(MySerial.available())
        {
            c = MySerial.read();          // Get char
            Serial.write(c);               // Print char
        }
    }

    //
    // Send reply to Raspberry Pi
    //
    MySerial.println("Hello Raspberry Pi, I am OK");
    while(1);
}
```
```

Figure 11.7 ARDUINOSerial.c