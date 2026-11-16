Now that the result of the formula is easily available as WAIT_MS_CYCLES, assembler directives are used to detect if this value is out of range or not. This is done with the following code.

```
.if (WAIT_MS_CYCLES > (exp2(32) - 1))
    .error "F_CPU MS_TIME_DEL combination out of range in wait_ms subroutine."
.endif
```

In the above code, the .if directive is used to determine if the 32-bit value calculated by the formula and equated to WAIT_MS_CYCLES is within range. We know that the maximum value that a 32-bit number can be is 2^32 - 1. The AVR assembler program supports a function called exp2() that calculates 2 to the power of the number passed to it. In the code, exp2() is used to calculated the biggest 32-bit value by passing it 32. One is then subtracted from the result which gives us the highest number that a 32-bit number can hold. In other words, the following code calculates 2^32 - 1.

```
(exp2(32) - 1)
```

Within the brackets after the .if directive, the greater-than operator (>) is used to determine if the value of WAIT_MS_CYCLES is bigger than the result of the above calculation, as shown below.

```
.if (WAIT_MS_CYCLES > (exp2(32) - 1))
```

In the above line of code, if WAIT_MS_CYCLES is less than 2^32 - 1, then the code between the .if directive and the closing .endif directive is ignored. On the other hand, if the value of WAIT_MS_CYCLES is bigger than 2^32 - 1, then the code between the .if directive and the .endif directive is executed. This code contains the .error directive followed by a text string. The .error directive flags an error in Microchip Studio and prints the text string that follows the .error directive. This message is our own message that describes what the problem is. As can be seen, the message states that the F_CPU MS_TIME_DEL combination is out of is of range in the wait_ms subroutine, which is a good description of the problem. We can test this code using the limits that we calculated. To avoid any confusion, the full modified code from the wait_ms.asm project follows.