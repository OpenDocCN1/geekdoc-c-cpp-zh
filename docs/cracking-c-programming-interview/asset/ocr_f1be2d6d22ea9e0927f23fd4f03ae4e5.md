# LSB get stored at higher address

**Figure 3.3:** Memory Representation of an integer into Little Endian mode

**Big-Endian:** Just an opposite of Little-Endian, here LSB gets stored at lower addresses and MSB gets stored at higher addresses. The 258 can be represented in a machine with big-endian as follows:

LSB get stored at lower address

| 00000010 | 00000001 | 00000000 | 00000000 |
|---|---|---|---||
| 1000 | 1001 | 1002 | 1003 |

MSB get stored at higher address

**Figure 3.4:** Memory Representation of an integer into Big Endian mode

Almost all the machines we use for programming purposes Intel, AMD, Our concern is to build your concepts without misconception. Practically, these machines are following little-endian but if we want to trace addresses of arrays, structures, etc. from the C program it would be difficult. But if we think about big-endian, it is always easy to trace the memory addresses through the C program.
int a[3] = {5, 6, 7}; stored in machine following little endian architecture as follows:

| 00 | 00 | 00 | 05 | 00 | 00 | 00 | 06 | 00 | 00 | 00 | 07 |
|---|---|---|---|---|---|---|---|---|---|---|---||
| 1000 | 1001 | 1002 | 1003 | 1004 | 1005 | 1006 | 1007 | 1008 | 1009 | 1010 | 1011 |

**Figure 3.5:** Representation of an array element in hexadecimal form in Little Endian mode

In our discussion for this question, we'll explain the concept using big-endian for better understanding. The representation of an array in the machine using big-endian is as follows:

```
int a[3]={5,6,7};
```

| 05 | 00 | 00 | 00 | 00 | 00 | 07 | 00 | 00 | 00 | 00 |
|---|---|---|---|---|---|---|---|---|---|---|---||
| 1000 | 1001 | 1002 | 1003 | 1004 | 1005 | 1006 | 1007 | 1008 | 1009 | 1010 | 1011 |