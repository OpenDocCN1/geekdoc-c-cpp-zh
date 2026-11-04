
- 5. Send a reply to the client, or close the socket.
- 6. Go back to Step 3 (if not closed).

## Client

- 1. Create UDP socket.
- 2. Send a message to the server.
- 3. Wait until a response from the server is received.
- 4. Process reply.
- 5. Go back to step 2, or close the socket.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_325_0.png)

Figure 14.1 UDP communication

## 14.4 • Project 1 – Communicating with an Android smartphone using UDP
(Raspberry Pi is the server)

### Description:

In this project, UDP communication is used to receive and send data to/from an Android smartphone. In this project, Raspberry Pi is the server and the Android smartphone is the client

### Aim:

This project aims to show how UDP communication can be established between a Raspberry Pi and an Android smartphone

### Block diagram:

Figure 14.2 shows the block diagram of the project. The Raspberry Pi and Android smartphone communicate over a Wi-Fi router link.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_326_0.png)

Figure 14.2 Block diagram of the project

### Program listing:

The program listing is shown in Figure 14.3 (Program: **MyServer.c**). At the beginning of the program, the required header files are included in the program. The message **Hello from Raspberry Pi** is stored in character array **msg**. A UDP type socket is then created by calling the **socket** function and saving the handle in the **sock** variable. Details of the server computer (Raspberry Pi) are then given where the address is set to **INADDR_ANY** so any other computer on the same network with the port number set to 5000 will establish communication with the Raspberry Pi. The server computer details are then bound to the specified port by calling function **bind**.

The remainder of the program runs in a loop. Inside this loop, function **recvfrom** is called to wait to receive a data packet from the client computer (Android smartphone). Notice this is a blocking call and the function will wait until data is received from the client. The program terminates if character **x** is received from the client computer. A NULL character is added to the received data and is displayed on the PC screen of the Raspberry Pi as a string using the **printf** function. An integer variable called **count** is converted into character and added to the end of character array **msg**. This is sent to the client computer. The first time in the loop, the client computer will display **Hello from Raspberry Pi 1**. The second time, the client computer will display **Hello from Raspberry Pi 2** and so on. The socket is closed just before the program terminates. The program can be compiled and run as follows:

```c
gcc -o MyServer MyServer.c
sudo ./MyServer
```

```c
/*--------------------------------------------------------------------------------
        RASPBERRY PI - ANDROID SMARTPHONE COMMUNICATION
        ===============================================

This is UDP program. The program receives and then sends messages to
a smartphone over the UDP socket. Program terminates when character x
is sent from the smartphone

This is the UDP server program, communicating over port 5000

Author: Dogan Ibrahim
File  : MyServer.c
Date  : December 2020
--------------------------------------------------------------------------------*/

#include <netinet/in.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#define Port 5000
#define BUFFSIZE 1024

// Start of MAIN program
//
int main(void)
{
    int sock, len, num, count = 1;
    char buffer[BUFFSIZE];
    struct sockaddr_in serveraddr, clientaddr;
    char msg[26] = "Hello from Raspberry Pi  ";

    sock = socket(AF_INET, SOCK_DGRAM, 0);
    len = sizeof(clientaddr);

    serveraddr.sin_family = AF_INET;
    serveraddr.sin_addr.s_addr = INADDR_ANY;
    serveraddr.sin_port = htons(Port);
    bind(sock,(struct sockaddr *)&serveraddr, sizeof(serveraddr));

    while(1)
    {
        num = recvfrom(sock, buffer, BUFFSIZE,MSG_WAITALL,
               (    struct sockaddr *)&clientaddr, &len);
        if(buffer[0] == 'x')break;
        buffer[num] = '\0';

printf("%s\n",buffer);

sprintf(&msg[24], "%d",count);
count++;
sendto(sock, &msg, strlen(msg), MSG_CONFIRM,
    (struct sockaddr *)&clientaddr, len);
}
close(sock);
}
```

Figure 14.3 MyServer.c

There are many UDP apps available on the Play Store free of charge. In this project, the UDP Terminal by mightyIT is used (see Figure 14.4). Enter the port number and IP address of your Android smartphone and click Start Terminal as shown in Figure 14.5. An example run of the program is shown in Figure 14.6, where both the smartphone and PC screen are shown.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_328_0.png)

Figure 14.4 UDP Terminal apps on Android smartphone

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_328_1.png)

Figure 14.5 Enter the port numbers

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_329_0.png)

Figure 14.6 Example run of the program

**Note:** you can find the IP address of your Raspberry Pi by using the **ifconfig** command.

## 14.5 • Project 2 – Sending temperature readings to Android smartphone
(Raspberry Pi is the server)

### Description:

In this project, a TMP102 temperature sensor chip (see Chapter 7) is connected to a Raspberry Pi. The ambient temperature reading is sent to an Android smartphone when a request is made by the smartphone. The smartphone makes a request by sending character T to Raspberry Pi over the Wi-Fi link using UDP protocol. Sending character x terminates the program.

### Aim:

This project aims to show how the temperature reading can be sent to an Android smartphone over a Wi-Fi link using the UDP protocol.

### Block diagram:

Figure 14.7 shows the block diagram of the project. In this project, a TMP102 module is used (see Figure 7.16).

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_330_0.png)

Figure 14.7 Block diagram of the project

### Circuit diagram:

The circuit diagram of the project is as shown in Figure 7.18. On-chip pull-up resistors are available on the TMP102 I2C bus lines. I2C bus lines SDA and SCL pins of the TMP102 are connected to GPIO 2 and 3 respectively.

### Program listing:

Figure 14.8 shows the program listing (Program: TMP102UDP.c). In this program, the wiringPi library and GPIO pin numbering is used. The program is in two parts: the function that reads the temperature from the TMP102 and the main program that sends the temperature reading to the Android smartphone. Function ReadTemperature reads the temperature from the TMP102 sensor module and returns it to the main program as a floating-point number (see Section 7.5 for details). The main program runs in a loop and waits to receive commands from the Android smartphone. If the received command is character x, the program terminates and the message End of program is sent to the smartphone. If the command is T, function ReadTemperature is then called. Temperature is converted into integer and stored in variable temperature. This is then converted into a string and stored in array msg. Character C (Centigrade) is then added to the end of msg and is sent and displayed on the Android smartphone. If the user command is anything other than x or T, the error message Error – expected T or x is sent and displayed on the Android screen. You can compile and run the program as follows:

```c
gcc -o TMP102UDP TMP102UDP.c -lwiringPi
sudo ./TMP102UDP
```

```c
/* SENDING TEMPERATURE TO ANDROID SMART PHONE

In this program a TMP102 type temperature sensor chip is connected to Raspberry Pi. The program sends the temperature reading to an Android smartphone when a request is made. A request is made when the smartphone sends character T to Raspberry Pi over a Wi-Fi link. Sending character x terminates the program. Any other character generates an error message on the Android screen

This is the UDP server program, communicating over port 5000

Author: Dogan Ibrahim
File : TMP102UDP.c
Date : December 2020
*/

// wiringPi includes and defines
//
#include <wiringPi.h>
#include <wiringPiI2C.h>
#define DeviceAddress 0x48
#define PointerReg 0x00

// UDP includes and defines
//
#include <netinet/in.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#define Port 5000
#define BUFFSIZE 1024

int handle;

// This function reads the temperature from TMP102 and returns to
// the calling main program as a floating point number
//
float ReadTemperature()
{
    int Temp, buf[2];
    float temperature, LSB = 0.0625;
```
