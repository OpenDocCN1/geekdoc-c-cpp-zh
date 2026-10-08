The C18 compiler contains a function called “Delay 10KTCYx( )” which allows the programmer to specify a time delay in multiples of 10,000 instruction cycles. This “Delay” function is included in the C18 compiler’s header file “delays.h”. Note that the instruction cycle is the time taken to execute the machine code instruction of a PIC18F instruction. As mentioned before, the PIC18F performs one machine code instruction every four clock cycles. The details of the function name “Delay 10KTCYx( )” can be broken down as follows:

+   - Function “Delay” is used to provide a fixed time delay.
- “10K” means ten thousand.
- “TCY” means the instruction cycle. Tcy.
- “x” multiplied by the argument (number) specified in the bracket. The number in the bracket must be an 8-bit unsigned integer (0-255). Hence, the time delay created will be the number in brackets multiplied by 10,000 instruction cycles.

As an example, consider writing a C-program to generate a time delay of 10 sec with an internal clock of 4-MHz using the C18 function “Delay10KTCYx( )”.

With $OSC = 4\text{MHz}$, Timer frequency is $(4\text{MHz})/4 = 1\text{MHz}$. Hence, period is $1\mu sec$. For 10 sec delay, Cycles $= (10)/(10^{-6}) = 10^7 = 10,000,000$. The C18 function “Delay10KTCYx(250)” will provide delays of 2,500,000 cycles. Performing a loop with the function “Delay10KTCYx(250)” four times will create a delay of 10 sec.

The C-program is provided below:

```
```
#include <P18F4321.h>
#include <delays.h>    // delay function library
{
unsigned char count;
void main()
    OSCCON = 0x60; // 4Mhz
    for (count = 0; count < 4; count++) // Use delay function 4 times
    Delay10KTCYx(250); // Delay in multiples of 10,000 instruction cycles.
}
```
```

# **Example 8.4**

Assume PIC18F4321. Suppose that three switches are connected to bits 0-2 of PORTC and an LED to bit 6 of PORTD. If the number of HIGH switches is even, turn the LED on; otherwise, turn the LED off. Write a C language program to accomplish this.

# *Solution*

The C language program is shown below:

```
```
#include <p18f4321.h>
#define    portc0   PORTCbits.RC0
#define    portc1   PORTCbits.RC1
#define    portc2   PORTCbits.RC2
void main (void)
{
    unsigned char mask = 0x07;              // data for masking off upper 5 bits of PORTC
    unsigned char masked_in;
```
```