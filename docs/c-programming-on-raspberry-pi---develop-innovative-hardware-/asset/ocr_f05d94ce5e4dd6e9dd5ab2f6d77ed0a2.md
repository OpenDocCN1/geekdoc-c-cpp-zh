![](bbox=[0.321, 0.091, 0.71, 0.384])

Figure 12.25 Circuit diagram of the project

# **Program Listing:**

Before driving the display, we have to know the relationship between the numbers to be displayed and the corresponding segments to be turned ON. This is shown in Table 9.2. GPIO ports 21, 20, 16, 12, 7, 8, 25 are collected together to form an 8-bit port (top bit not used), and display data is sent to this port. For example, to display number 3, we have to send the hexadecimal number 0x4F to the port which turns ON segments **a,b,c,d,** and **g**. Similarly, to display number 9, we have to send the hexadecimal number 0x6F to the port which turns ON segments **a,b,c,d, f,** and **g**.

x is not used, taken as 0

| Number | x | g | f | e | d | c | b | a | Data to send |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 0 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 0x3F |
| 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0x06 |
| 2 | 0 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 0x5B |
| 3 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | 0x4F |
| 4 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | 0 | 0x66 |
| 5 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 1 | 0x6D |
| 6 | 0 | 1 | 1 | 1 | 1 | 1 | 0 | 1 | 0x7D |
| 7 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 0x07 |
| 8 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0x7F |
| 9 | 0 | 1 | 1 | 0 | 1 | 1 | 1 | 1 | 0x6F |

Table 9.2 Displayed number and data sent to LEDs