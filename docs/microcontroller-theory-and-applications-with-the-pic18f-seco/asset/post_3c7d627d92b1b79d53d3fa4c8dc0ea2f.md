
correct packed BCD using DAW.

Line #’s 1 through 4 initialize N1 and N2 so that [0x40] = 39H, [0x41] = 34H, [0x50] = 31H, [0x51] = 32H. Line #5 initializes COUNTER with loop count of 2 for converting the numbers from ASCII to unpacked BCD. Line #’s 6 and 7 initialize FSR0 and FSR1 with 0x40 and 0x50 respectively. Line #’s 8 through 11 convert the two bytes of ASCII codes in 0x41 (high byte) and 0x40 (low byte) into unpacked BCD in 0x41 (high byte) and 0x40 (low byte). Also, Line #’s 8 through 11 convert the ASCII numbers, N1 and N2, into their corresponding unpacked BCD bytes.

Line #’s 12 through 15 convert the unpacked BCD numbers (N1 and N2) into packed BCD bytes. This is done by swapping high unpacked bytes of N1 and N2, and then ORing with the corresponding low unpacked bytes. Line #16 performs binary addition of the two packed BCD bytes (N1 and N2), and stores the binary result in WREG. The DAW instruction at Line #17 adjusts the contents of WREG to provide the correct packed BCD result.

## 7.9 PIC18F Delay Routine

Typical PIC18F software delay routines can be written by loading a “counter” with a value equivalent to the desired delay time, and then decrementing the “counter” in a loop using typically MOVE, DECREMENT, and conditional BRANCH instructions. For example, the following PIC18F instruction sequence can be used for a delay loop:

```assembly
MOV LW COUNT
MOVWF 0x20
DELAY DECF 0x20, F
BNZ DELAY
```

Note that DECF in the above decrements the register 0x20 by one, and if Z = 0, the program branches to DELAY and if Z = 1, the PIC18F executes the next instruction. The initial loop counter value of “COUNT” can be calculated using the machine cycles (Appendix D) required to execute the following PIC18F instructions:

```text
MOV LW (1 cycle)
MOVWF (1 cycle)
DECF (1 cycle)
BNZ (2/1 cycles)
```

Note that the BNZ instruction requires two different execution times. BNZ requires 2 cycles when the PIC18F branches if Z = 0. However, the PIC18F goes to the next instruction and does not branch when Z = 1. This means that the DELAY loop will require 2 cycles for “(COUNT-1)” times, and the last iteration will take 1 cycle. The desired delay time can be obtained by loading register 0x20 with the appropriate COUNT value.

Assuming a 1-MHz default crystal frequency, the PIC18F’s clock period will be 1μs. Note that the PIC18F divides the crystal frequency by 4. This is equivalent to multiplying the clock period by 4. Hence, each instruction cycle will be 4 microseconds. For a 100 microsecond delay, total cycles = 100 micro sec / 4 micro sec = 25. The BNZ in the loop will require 2 cycles for (COUNT - 1) times when Z = 0 and the last iteration will take 1 cycle when no branch is taken (Z = 1). Thus, the total cycles including the MOVWF = Cycles for (MOVWF + MOVWF F + (BNZ for Z = 0 + DECF) × (COUNT - 1)) + BNZ(Z = 1) = 1 + 1 + 3 × (COUNT - 1) + 1 = 25. Hence, COUNT = 8.3. Therefore, register 0x20 should be loaded with an integer value of 8 for an approximate delay of 100 microseconds.

Now, in order to obtain delay of one millisecond, the above DELAY loop of 100 microseconds can be used with an external counter. Counter value = 1 millisecond / 100 microseconds = 10. The following instruction sequence will provide an approximate delay of one millisecond:

```assembly
      MOVW D'10'    ; Initialize counter 0x30 for one millisecond delay
      MOVWF 0x30
BACK  MOVW 8
      MOVWF 0x20    ; Initialize counter 0x20 for 100 microsecond delay
DELAY DECF 0x20, F  ; 100 microsecond delay
      BNZ DELAY
      DECF 0x30, F
      BNZ BACK
```

The above instruction sequence will provide an approximate delay of one millisecond. Note that execution times of certain instructions such as “MOVW D'10'”, “MOVWF 0x30”, “DECF 0x30, F” and “BNZ BACK” are discarded since their execution times are negligible compared to one millisecond.

## Example 7.10

Assume 1 MHz PIC18F. Consider the following subroutine:

```assembly
DELAY MOVW D'100'
      MOVWF 0x20
LOOP  DECFSZ 0x20, F
      BRA LOOP
      RETURN
```

- (a) Calculate the time delay provided by the above subroutine.

- (b) Calculate the counter value to be loaded into data register 0x20 for 1 ms delay.

### Solution

- (a) Each instruction in the above subroutine is executed in one cycle except for the DECFSZ instruction. DECFSZ is executed in one cycle if it does not skip, and two cycles if it skips (See Appendix D for instruction cycles).

Hence, total instruction cycles = Cycle for MOVW L + Cycle for MOVWF F + (100 - 1) (Cycles for DECFSZ if it does not skip and BRA instructions) + (Cycle for DECFSZ if it skips) + Cycle for RETURN = 1 + 1 + 99(1 + 1) + 2 + 1 = 203

Since for the PIC18F, one instruction cycle = 4 clock cycles, total delay = (203) × 4 = 812 clock cycles. Also, for 1 MHz clock, each clock cycle is 1 μsec. Hence, total time delay = 812 μsec.

- (b) Let n be the counter value. Hence, (2 + 2 × (n - 1) + 3) × 4 = 1000 μsec. Note that 1 ms = 1000 μsec. Therefore, n = 123.5. Therefore, data register 0x20 should be loaded with 124 for an approximate delay of 1 ms.

## QUESTIONS AND PROBLEMS

- 7.1 Write a PIC18F assembly language program at address 0x150 to subtract two 16-bit numbers as follows: [0x21][0x20] - [0x31][0x30] → [0x40][0x41], if [0x50] is odd. If [0x50] is even store 0's in [0x41] [0x40].

- 7.2 Write a PIC18F assembly language program at address 0x100 to add a 4-bit unsigned number stored in the high nibble of data register 0x30 with a 4-bit unsigned number stored in the low nibble of data register 0x30. Store the 8-bit result in 0x30.

- 7.3 Write a PIC18F assembly program at address 0x200 to multiply a 4-bit unsigned number in the low nibble of 0x30 by another 4-bit unsigned number in the high nibble of 0x30. Store the result in 0x31.

- 7.4 Write a PIC18F assembly language program at address 0x150 to convert temperature from Fahrenheit to Celsius using the equation: C = ([F - 32]/9) × 5; assume that the temperature in Fahrenheit is 8-bit wide to be loaded into data register 0x20. Assume that the temperature is always positive. Store the 8-bit result in data register 0x21.

- 7.5 Write a PIC18F assembly language program at address 0x100 to find X/128 where X is an 8-bit unsigned number stored in data register 0x40. The program will then compute X/128 and then store the 8-bit quotient in data register 0x50. Discard the remainder.

- 7.6 Write a PIC18F assembly language program at address 0x200 to perform (X² + Y²) where X is a signed 8-bit number and Y is an unsigned 8-bit number. Write subroutine for multiplication in PIC18F assembly as needed. Also, write the main program at address 0x100 in PIC18F assembly language that will initialize FSR0 to 0x0070, X and Y to arbitrary data, call the subroutines to compute (X² + Y²), and then push the 8-bit result onto the software stack pointed to by FSR0.

- 7.7 Write a PIC18F assembly program at address 0x100 which is equivalent to the following C language segment:

```c
sum = 0;
for (i = 0; i <= 9; i = i + 1)
    sum = sum + x[i] * y[i];
```

Assume that the arrays, growing from LOW to HIGH addresses, and x[i] and y[i], contain unsigned 8-bit numbers already stored in memory starting at data memory addresses 0x20 and 0x30 respectively. Store the 8-bit result at address 0x50.

- 7.8 Write a PIC18F assembly program at address 0x150 to compare two strings of 10 ASCII characters. The first string is stored starting at 0x30. The second string is stored at location 0x50. The ASCII character in location 0x30 of string 1 will be compared with the ASCII character in location 0x50 of string 2, [0x31] will be compared with [0x51], and so on. Each time there is a match, store 0xEE onto the software stack; otherwise, store 0x00 onto the software stack. Initialize software stack pointer at 0x60.
