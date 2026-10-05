# C.4.7 Bitwise operators are often used in data coding in network communications. For example, some specific bits in the header of a Transfer Control Protocol (TCP) packet are coded as follows:

| bit8 | bit7 | bit6 | bit5 | bit4 | bit3 | bit2 | bit1 |
|---|---|---|---|---|---|---|---|n| | | URG | ACK | | | SYN | FIN |

FIN(bit1): If it is 1, it indicates the release of the TCP connection.
SYN(bit2): If it is 1, it indicates the establishment of the TCP connection. That's the famous bit responsible for Denial-of-Service (DoS) flooding attacks, but this is another story ...
ACK(bit5): If it is 1, it indicates the acknowledgement of data reception.
URG(bit6): If it is 1, it indicates the transfer of urgent data.

Write a program that reads the values of URG, ACK, SYN, and FIN and encodes this information in a program variable. Then, the program should decode the value of this variable and display the values of the respective bits.

```
#include <iostream>
using std::cout;
using std::cin;

int main() {
    unsigned int temp
```