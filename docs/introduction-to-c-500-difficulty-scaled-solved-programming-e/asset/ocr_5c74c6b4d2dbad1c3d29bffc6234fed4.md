# 398 Introduction to C++

# EXERCISE

**C.13.10** In an ISDN network, the SETUP message of the Q.931 signalling protocol is sent by the calling user to the called user to initiate the call establishment procedure. A simplified format of the SETUP message is depicted in the following:

| PD | CRV | MT | BC | CPN | LLC | HLC | D/T |
|---|---|---|---|---|---|---|---|n| 1 byte | 3 bytes | 1 byte | 12 bytes | 20 bytes | 18 bytes | 5 bytes | 8 bytes |

The ALERTING message (see the figure) is sent by the ISDN network to the calling user to indicate that the called user is notified for the incoming call (e.g., ring tone).

| PD | CRV | MT | BC | CI |
|---|---|---|---|---|n| 1 byte | 3 bytes | 1 byte | 4 bytes | 6 bytes |

The CONNECT message (see the figure) is sent by the ISDN network to the calling user to indicate that the called user accepted the call (e.g., picks up the phone).

| PD | CRV | MT | BC | PI | SIG | HLC |
|---|---|---|---|---|---|---|n| 1 byte | 3 bytes | 1 byte | 8 bytes | 4 bytes | 3 bytes | 5 bytes |

These messages traverse the ISDN switches along the path between the two users. Each node value contains the content of the received messages. Let's write a program to simulate this message analysis. Define the structure that uses Isdn_Msg with one member union. The members of union are three structures to represent the SETUP, CONNECT, and ALERTING messages. Write a program that reads a byte stream, uses the figures above to parse the data and stores them in the proper union member. To parse the program should check the value of the MT field. Its value in the SETUP, CONNECT, and ALERTING messages is 5, 7, and 1, respectively. To get the byte stream program read 100 integers in [0, 255] and store them in an array. If the user enters -1, the insertion of data should terminate.

```
#include <iostream>
using std::cout;
using std::cin;

using BYTE = unsigned char;

struct Header {
    BYTE pd;
    BYTE crv[3];
    BYTE mt;
}
```