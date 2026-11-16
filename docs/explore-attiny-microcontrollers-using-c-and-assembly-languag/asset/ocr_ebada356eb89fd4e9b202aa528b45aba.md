# 10.2.2.1 Principle of Operation

The principle of operation of the wait_1s subroutine is to decrement a 32-bit number until it is zero in order to waste enough time to cause the desired delay of 1 second. If the frequency that the microcontroller is running at is 1MHz, then the subroutine must use up one million clock cycles to create a 1s time delay. This is because 1MHz is 1 million cycles per second, meaning that at this frequency, 1 million cycles take one second to complete.

Some of the ATtiny microcontrollers used in this book can operate up to a maximum clock frequency of 20MHz. Because frequency is measured in Hertz (Hz), which is clock cycles per second, and the wait_1s subroutine is to delay for 1 second, the number of clock cycles to use up for a 1s delay equals the frequency that the microcontroller is operating at. For the maximum frequency of 20MHz, 20 million clock cycles must complete to use up 1s. If the microcontroller is operating at 1.2MHz, then 1.2 million cycles must complete to use up one second, and so on for whichever frequency is being used. F_CPU at the top of the code must be changed to the frequency that the microcontroller is operating at in order for the wait_1s subroutine to correctly delay for 1s.

# 10.2.2.2 32-bit Subtraction with 8-bit Registers

In order to perform subtraction from a 32-bit number on an 8-bit processor, four 8-bit registers are needed to hold the 32-bit number. In the wait_1s subroutine, registers R16, R17, R18 and R19 are used to hold the 32-bit number to subtract from. If the subtraction process took only one clock cycle, then we would only need to load the value of the frequency that the microcontroller is operating at to these registers, as follows.

```
ldi   R16, low (F_CPU)
ldi   R17, byte2(F_CPU)
ldi   R18, byte3(F_CPU)
ldi   R19, byte4(F_CPU)
```

In the above code, we have the familiar low() assembler function that gets the lower byte of the F_CPU value. New in this code is byte2(), byte3() and byte4() which operate in the same way as low(), but get the second, third and fourth bytes of a 32-bit number. These functions are found in the AVR Assembler document. What the above code therefore does is load the value of F_CPU to R16, R17, R18 and R19, byte by byte in order, starting from the least significant byte up to the most significant byte. As it turns out, the subtraction process takes more than one clock cycle. The code in the wait_1s.asm listing therefore does not directly load the value of F_CPU to the registers, but does some mathematical compensation, that is explained in the next section.