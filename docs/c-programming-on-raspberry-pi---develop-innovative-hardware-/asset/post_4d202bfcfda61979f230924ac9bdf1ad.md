
```c
//
// Connections between Raspberry Pi and LCD
//
#define D4 2
#define D5 3
#define D6 17
#define D7 27
#define RS 22
#define E 10

//
// Start of MAIN program
//
int main(void)
{
    int lcd;
    char CurrentDate[16], CurrentTime[12];
    struct tm* timeinfo;
    time_t timer;

    wiringPiSetupGpio();
    lcd = lcdInit(2, 16, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);
    lcdClear(lcd);

    while(1)
    {
        time(&timer);
        timeinfo = localtime(&timer);

        strftime(CurrentDate, 16, "%d-%b-%Y", timeinfo);
        strftime(CurrentTime, 12, "%H:%M:%S", timeinfo);

        lcdPosition(lcd, 0, 0);
        lcdPuts(lcd, CurrentDate);

        lcdPosition(lcd, 0, 1);
        lcdPuts(lcd, CurrentTime);
        delay(1000);
    }
}
```

Figure 6.9 Program LCDDateTime.c

## 6.8 Project 6 – Displaying the temperature and humidity

### Description:

In this project, a DHT11 temperature and humidity sensor chip is used. Ambient temperature and humidity are displayed on the top and bottom rows of the LCD respectively.

### Aim:

This project aims to show how temperature and humidity data can be displayed on the LCD.

### Block diagram:

Figure 6.10 shows the block diagram of the project.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_194_0.png)

Figure 6.10 Block diagram of the project

### Circuit diagram:

The circuit diagram of the project is shown in Figure 6.11. The LCD is connected to the Raspberry Pi as in the previous project. The DHT11 sensor is connected to GPIO 9.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_194_1.png)

Figure 6.11 Circuit diagram of the project

### Program listing:

### wiringPi

Figure 6.12 shows the program listing (Program: LCDTH.c). In this program, GPIO pin numbering is used. The part of the program that reads the temperature and humidity is as in Figure 5.45. Additionally, the data is displayed on the LCD.

```c
/*-----------------------------------------------------------
                    DISPLAY TEMPERATURE AND HUMIDITY ON LCD
                    ================================

In this program a DHT11 sensor chip and an LCD are connected to the
Raspberry Pi. The program displays the temperature and humidity on
the LCD

Author: Dogan Ibrahim
File  : LCDTH.c
Date  : December 2020
-----------------------------------------------------------*/

#include <wiringPi.h>
#include <stdio.h>
#include <lcd.h>

//
// Connections between Raspberry Pi and LCD
//
#define D4 2
#define D5 3
#define D6 17
#define D7 27
#define RS 22
#define E 10

//
// DHT11 data pin (GPIO 9)
//
#define DHT_PIN 9

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

// This function reads the temperature and humidity from DHT11
// and returns the readings to the calling program
//
void Read_DHT11(int *T, int *H)
{
    char res, i, state, counter, indx = 0;
    int data[5];

    for(i = 0; i < 5; i++)data[i] = 0;
    pinMode(DHT_PIN, OUTPUT);
    digitalWrite(DHT_PIN, LOW);
    delay(18);
    digitalWrite(DHT_PIN, HIGH);
    delayMicroseconds(40);
    pinMode(DHT_PIN, INPUT);

    res = WaitEdge(0);
    res = res * WaitEdge(1);

    i = 0;
    while(i < 80 && res == 0)
    {
        counter = 0;
        if(WaitEdge(0) == 1)break;
        while(digitalRead(DHT_PIN) == HIGH)
        {
            counter++;
            delayMicroseconds(1);
            if(counter == 255)break;
        }

        data[indx/8] <<= 1;
        if(counter > 28)data[indx/8] |= 1;
        indx++;
        i++;
    }
    //
    // Check the Checksum
    //
    if((indx >= 40) && (data[4] ==
       ((data[0] + data[1] + data[2] + data[3]) & 0xFF)))
    {
        *T = data[2];                // T = data[2].data[3]
        *H = data[0];                // H = data[0].data[1]
    }
}

//
// Start of MAIN program
//
int main(void)
{
    int Temp, Hum, lcd;

    wiringPiSetupGpio();
    delay(1000);
    lcd = lcdInit(2, 16, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);

    while(1)
    {
        Read_DHT11(&Temp, &Hum);
        lcdClear(lcd);
        lcdPosition(lcd, 0, 0);          // row 0, col 0
        lcdPrintf(lcd, "T = %d C", Temp);
        lcdPosition(lcd, 0, 1);          // row 1, col 0
        lcdPrintf(lcd, "H = %d %%", Hum);
        delay(5000);                     // 5s delay
    }
}
```

Figure 6.12 Program LCDTH.c

The data is displayed in the following format:

**T = 22 C**

**H = 58 %**

## 6.9 Summary

In this chapter, we learned how to use LCDs with Raspberry Pi while programming using the wiringPi library and C language.

The key topic of the next chapter is the I2C (or I²C) interface and corresponding library.

# Chapter 7 • I2C Bus Interface

## 7.1 Overview

The I2C (or I²C) bus is commonly used in microcontroller based projects. In this chapter, we will look at the use of this bus on Raspberry Pi. The aim is to make the reader familiar with I2C bus library functions and to show how they can be used in a real project. Before looking at the details of the project, it is worthwhile to look at the basic principles of the I2C bus.

## 7.2 The I2C Bus

The I2C bus is one of the most frequently used microcontroller communication protocols for communicating with external devices such as sensors and actuators. The I2C bus is a single master, multiple slave bus, and can operate on standard mode: 100 Kbit/s, full speed: 400 Kbit/s, fast mode: 1 Mbit/s, and high speed: 3.2 Mbit/s. The bus consists of two open-drain wires, pulled-up with resistors:

- **SDA**: data line
- **SCL**: clock line

Figure 7.1 shows the structure of an I2C bus with one master and three slaves.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_199_0.png)

Figure 7.1 I2C bus with one master and three slaves

Because the I2C bus is based on just two wires, there should be a way to address an individual slave device on the same bus. For this reason, the protocol dictates that each slave device provides a unique slave address for the given bus. This address is usually 7-bits wide. When the bus is free, both lines are HIGH. All communication on the bus is initiated and completed by the master which initially sends a START bit, and completes a transaction by sending a STOP bit. This alerts all slaves that data is coming on the bus. After the start bit, 7 bits of unique slave address is sent. Each slave device on the bus has an address and this ensures that only the addressed slave communicates on the bus at any time to avoid any collisions. The last sent bit is the read/write bit. If this bit is 0, the master wishes to write to the bus (e.g. to a register of a slave). If it is 1, the master wishes to read from the bus (e.g. from the register of a slave). The data is sent on the bus with the MSB bit first. An acknowledgment (ACK) bit takes place after every byte and this bit allows the receiver to signal to the transmitter that the byte was received successfully, resulting in another byte being sent. ACK bit is sent at the 9th clock pulse.

Communication over the I2C bus is as follows:

- The master sends on the bus the address of the slave it wants to communicate with.
- The LSB is the R/W bit which establishes the direction of data transmission, i.e. from master to slave (R/W = 0), or from slave to master (R/W = 1).
- Required bytes are sent, each interleaved with an ACK bit until a stop condition occurs.

Depending on the type of slave device used, some transactions may require a separate transaction. For example, the steps to read data from an I2C compatible memory device are:

- Master starts the transaction in write mode (R/W = 0) by sending the slave address on the bus.
- The memory location to be retrieved are then sent as two bytes (assuming 64Kbit memory).
- The master sends a STOP condition to end the transaction
- The master starts a new transaction in read mode (R/W = 1) by sending the slave address on the bus
- The master reads the data from the memory. If reading the memory in sequential format, more than one byte will be read.
- The master sets a stop condition on the bus

Before using any I2C device we have to enable I2C in our Raspberry Pi configuration. The steps are:

- Start the configuration tool
- Move down to **Interface Options** and press **Enter**
- Select **I2C** and press **Enter** to enable it

```bash
pi@raspberrypi:~ $ sudo raspi-config
```

Before using the I2C pins of the Raspberry Pi, we have to make sure the I2C device connected to Raspberry Pi is recognized by the Raspberry Pi I2C bus. Build your circuit and enter the following command on the command line and ensure the I2C address of the connected device is displayed:

```bash
pi@raspberrypi:~ $ sudo i2cdetect -y 1
```
