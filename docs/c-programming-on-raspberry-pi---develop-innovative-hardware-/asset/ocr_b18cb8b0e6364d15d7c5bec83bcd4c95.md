```
```c
#include <wiringPi.h>
#include <stdio.h>

#define ON HIGH
#define OFF LOW

#define DHT_PIN 2                     // DHT11 pin
#define LED 27                        // LED pin
#define Buzzer 3                      // Buzzer pin
#define Relay 22                      // Relay pin

char clr[] = {0x1B,'[','2','J','\0'};          // Clear screen
char home[] = {0x1B,'[','H','\0'};             // Home cursor
char to34[] = {0x1B,'[','3','4',';','4','H','\0'};
char to30[] = {0x1B,'[','3',';','i',';','3','\0','H','\0'};
char to620[] = {0x1B,'[','6',';','2','\0','H','\0'};

//
// This function waits for and edge change. If there is no edge
// change in 255 microseconds then the function returns 1, otherwise
// it returns 0
//
int WaitEdge(int mode)
{
    int counter = 0;
    while(digitalRead(DHT_PIN) == mode)
    {
        counter++;
        delayMicroseconds(1);
        if(counter == 255)return 1;
    }
    return 0;
}

//
// Configure ports as input/output and turn OFF output ports
//
void Configure()
{
    pinMode(LED, OUTPUT);
    pinMode(Relay, OUTPUT);
    pinMode(Buzzer, OUTPUT);
    digitalWrite(LED, OFF);
    digitalWrite(Relay,OFF);
    digitalWrite(Buzzer, OFF);
}
```
```