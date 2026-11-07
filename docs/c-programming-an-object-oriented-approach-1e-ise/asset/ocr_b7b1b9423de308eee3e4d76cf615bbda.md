# Program 10.27 Changing a binary string to a decimal integer (Continued)

```
Run:
Enter binary string: 11 101
Enter binary string: 11101
Decimal value: 29

Run:
Enter binary string: 1181
Enter binary string: 11111
Decimal value: 31

Run:
Enter binary string: 111000111
Decimal value: 455
```

There are three important points about Program 10.27: First, in lines 21 to 25 we process a line of text that represents a binary string. The string we need must be made only of the characters '0' and '1', which means the input string must be validated before being used. This is done by the find_first_not_of function we learned earlier in the chapter. This function looks for characters that are not '0' or '1' and returns the corresponding index. If the returned index is less than the size of the string, it means that a character other than 0 or 1 was found in the string, and we loop back to read again.

Second, consider line 31. Each time we enter the loop, we must reset the value of decimal to decimal times the value of base, as for the algorithm given in Table 10.3.

Third, consider the popFront function. We know that in each iteration we must extract the next character in the string, which is correctly done by the popFront function defined in the header file.

# Conversion from Decimal to Any Other Base

Figure 10.15 shows how we convert a decimal to a string of three characters.

We use a loop that is controlled by the value of the decimal number. When the value is 0, we stop. Before starting the loop, the string is empty. In each iteration, we divide the previous value of decimal by base and get the remainder. We then change the resulting value to a character and push it to the front of the string. Note that in each iteration, the value of the decimal decreases until it becomes 0, but the size of the string is increased. When we come out of the loop, the string is ready. Table 10.5 shows the algorithm.

![](bbox=[0.27, 0.655, 0.88, 0.91])