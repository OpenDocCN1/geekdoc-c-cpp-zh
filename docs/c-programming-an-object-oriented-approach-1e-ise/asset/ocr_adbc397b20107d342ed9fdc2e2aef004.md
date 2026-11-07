![](bbox=[0.251, 0.091, 0.822, 0.292])

> > In C++, a number in the decimal system is used as an integer; numbers in other systems are used as a string of characters.

This means that when we are working with different numbering systems, we must change a string to an integer or vice versa. In this section we give a general design for doing so. Before studying the rest of this section, we recommend that you review Appendix B.

# Conversion from Any Other Base to Decimal

Figure 10.14 shows how we convert a string of three characters to an integer.

We use a loop that is controlled by the size of the string. When the string is empty, we exit the loop. Before starting the loop, we set the value of the decimal variable to 0. In each iteration, we multiply the previous value of decimal by its base. We then pop the first character, convert it to decimal, and add it to the value of decimal. Note that in each iteration, the value of decimal is increased, but the size of the string is decreased. When we come out of the loop, the value of decimal is computed. Table 10.4 shows the algorithm.

| Table 10.4 — Algorithm for converting a string to a decimal |  |
|---|---|
| set base | // set base to 2, 8, 16 |
| decimal = 0 |  |
| input string |  |
| while (string not empty) |  |
| { |  |
|   decimal *= base; |  |
|   ch = popFront(string) | // Use popFront function developed before |
|   decimal += findValue(ch) | // Use a function to change ch to its value |
| } |  |
| output decimal |  |