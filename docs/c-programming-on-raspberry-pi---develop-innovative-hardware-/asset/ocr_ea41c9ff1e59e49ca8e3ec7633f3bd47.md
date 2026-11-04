```
```c
        {
            Read_DHT11(&Temp, &Hum);
            printf("T=%d C H=%d %%\n", Temp, Hum);
            delay(5000);                              // 5s delay
        }
    }
```
```

Figure 5.47 Program dht11main.c

```
```c
/********************************************************
                DHT11 FUNCTIONS
                ===============

Author: Dogan Ibrahim
File  : dht11func.c
Date  : December 2020
--------------------------------------------------------*/

#include <wiringPi.h>
#include <stdio.h>

#define DHT_PIN 2

//
// This function waits for an edge change. If there is no edge
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
// This function reads the temperature and humidity from DHT11
// and returns the readings to the calling program
//
void Read_DHT11(int *T, int *H)
{
    char res, i, state, counter, index = 0;
    int data[5];
```
```