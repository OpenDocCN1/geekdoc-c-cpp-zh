```
```
BEGIN
    Initialise variables
    Create a TCP socket
    Get the IP address of the Thingspeak Cloud Service
    Create and load the TCP structure
    Connect to Thingspeak
    Call Read_DHT11 to read the temperature and humidity
    Load the temperature and humidity into msg2 and msg4 respectively
    Send data to Thingspeak
    Return
END
```
```

```
```c
/*--------------------------------------------------------------------
              SENDING TEMPERATURE AND HUMIDITY TO THE CLOUD
              ============================================

This is a Cloud based program using the Thingspeak Cloud Service. The
ambient temperature and humidity are read using a DHT11 sensor. The
data is sent to the Thingspeak cloud and plotted in real time

Author: Dogan Ibrahim
File : Cloud.c
Date : December 2020
-------------------------------------------------------------------------*/

#include <wiringPi.h>
#include <netinet/in.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <netdb.h>
#define Port 80

#define URL_OF_THINGSPEAK "api.thingspeak.com"
#define DHT_PIN 2

int WaitEdge(int);
void Read_DHT11(int*, int*);

unsigned long myChannelNumber=1278451;

//
// This function connects to Thingspeak Cloud Service and then reads
// and sends the aambient temperature and humidity to the Cloud where
// it is plotted in real time
//
```
```