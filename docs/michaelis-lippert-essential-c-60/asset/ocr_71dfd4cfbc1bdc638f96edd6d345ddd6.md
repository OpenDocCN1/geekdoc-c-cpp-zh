In many scenarios, particularly when dealing with low-level or system services, information is retrieved as binary data. To manipulate these devices and services, you need to perform manipulations of binary data.

In Figure 3.2, each box corresponds to a value of 2 raised to the power shown. The value of the byte (8-bit number) is the sum of the powers of 2 of all of the eight bits that are set to 1.

| 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
|---|---|---|---|---|---|---|---|

7 = 4 + 2 + 1

**FIGURE 3.2: Calculating the Value of an Unsigned Byte**

The binary translation just described is significantly different for signed numbers. Signed numbers (long, short, int) are represented using a “two’s complement” notation. This practice ensures that addition continues to work when adding a negative number to a positive number, as though both were positive operands. With this notation, negative numbers behave differently from positive numbers. Negative numbers are identified by a 1 in the leftmost location. If the leftmost location contains a 1, you add the locations with 0s rather than the locations with 1s. Each location corresponds to the negative power of 2 value. Furthermore, from the result, it is also necessary to subtract 1. This is demonstrated in Figure 3.3.

| 1 | 1 | 1 | 1 | 1 | 0 | 0 | 1 |
|---|---|---|---|---|---|---|---|

−7 = −4 −2 +0 −1

**FIGURE 3.3: Calculating the Value of a Signed Byte**

Therefore, 1111 1111 1111 1111 corresponds to −1, and 1111 1111 1111 1001 holds the value −7. The binary representation 1000 0000 0000 0000 corresponds to the lowest negative value that a 16-bit integer can hold.