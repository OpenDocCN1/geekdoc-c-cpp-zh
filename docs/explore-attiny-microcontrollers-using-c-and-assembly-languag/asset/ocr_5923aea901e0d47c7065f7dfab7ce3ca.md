```
R16 = R17 = 3

C: = 3 x (R17 x R16 + R16)
   = 3 x (3 x 3 + 3)
   = 36
```

Testing with the Microchip Studio simulator gives the same result of 36.

Now test the formula with the original values for R16 and R17 used in the code examples from previous chapters. This value is 0xFF (can also be written 0xff), which is 255 in decimal, and is also the upper extreme of any value that can be used with R16 and R17.

```
R16 = R17 = 255

C: = 3 x (R17 x R16 + R16)
   = 3 x (255 x 255 + 255)
   = 195840
```

When testing with the simulator in Microchip Studio, don't forget to change the values for R16 and R17, then save the changes and build the project before running the code in the simulator. Remember also to reset the Cycle Counter at the first breakpoint. The value of 195840 calculated above matches the value from the Cycle Counter in Microchip Studio.

Examining the delay subroutine code, we can see that it decrements the two count registers before testing the result of the decrement. From this we can see that loading 0 to either R16 or R17 will cause 1 to be subtracted from 0 when either of these registers is decremented. This results in -1 in two's compliment format which is 0xFF in an 8-bit register. Because of this, we will leave the test case for 0 in either of the count registers for the end of our testing.

For now we test the formula with R16 and R17 equal to 1.

```
R16 = R17 = 1

C: = 3 x (R17 x R16 + R16)
   = 3 x (1 x 1 + 1)
   = 6
```

Testing the code with R16 and R17 both containing 1 in the Microchip Studio simulator, we get 6 cycles, the same as the result from the formula.

The next test loads R16 and R17 with values at opposite extremes between 1 and 255. Although 0 is the actual lowest extreme, it is tested last in this series of tests.