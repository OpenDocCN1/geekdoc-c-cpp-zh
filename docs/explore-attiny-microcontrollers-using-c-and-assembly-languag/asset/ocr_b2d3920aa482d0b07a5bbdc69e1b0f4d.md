# 9.3.3 Defining Names for Registers with DEF

DEF is a directive that can be used to give a register a human readable name. In the example that follows, R16 is given the name count. After being given the name count at the beginning of the code using DEF, R16 is referred to as count in the rest of the program. Enter this code into the test_asm project and run it in the simulator to see that when count is cleared, R16 is cleared, and when count is incremented using the INC instruction, R16 is incremented.

```
.DEF count = R16
ldi count, 0x00 ; Clear count register
loop:
inc count ; Increment count register
rjmp loop
```

# 9.3.4 Equating Names to Expressions using EQU and SET

EQU is used to set a human readable name equal to an expression. The expression can be a simple number, as the following example code shows.

```
.DEF count = R16
.EQU count_start = 5
ldi count, count_start ; Value to start counting from
loop:
inc count ; Increment count register
rjmp loop
```

The above code shows that EQU is used to make count_start equal to 5. Wherever count_start is used in the code, 5 is substituted. In this example code, count_start is used to load a value of 5 to R16, by using R16 defined as count using DEF, and making count_start equal to 5 using EQU. This causes the value in R16 to start incrementing from 5 instead of 0. Enter this code into the test_asm project and run it in the simulator.

SET assigns a value to a label in the same way as EQU, but unlike EQU, a label assigned to a value by SET can be changed or redefined later in a program. In the previous code example, SET can directly be substituted in place of EQU.