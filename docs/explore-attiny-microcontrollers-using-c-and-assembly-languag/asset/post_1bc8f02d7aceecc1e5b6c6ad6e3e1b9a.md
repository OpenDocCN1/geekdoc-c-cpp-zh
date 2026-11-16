
## 10.3.2 Returning a Value from an Assembly Subroutine in C

Once again we refer to section 6 of the Atmel AT1886: Mixing Assembly and C with AVRGCC document called Parameter passing in order to find information on how to return a value from an assembly language subroutine that is called from a C program. The document says the following about returning a value: " Return values use the registers r25 through r18, depending on the size of the return value. " It also says the following about passing char arguments to a subroutine: " All arguments use an even number of registers. This results in char arguments consuming two registers. " In the next project called asm_add_c, two char arguments are passed to an assembly language subroutine from C code, added together by the subroutine, and a char result returned from the subroutine. Create the project in Microchip Studio and add the add8bit.S and add8bit.h files to the project, in the same way that extra files were added to the previous project. Enter the code from the following listings in the project files.

```
asm_add.c : main.c
#include <avr/io.h>
#include "add8bit.h"

int main(void)
{
  volatile char sum;
  sum = add8bit(34, 91);
}
```

```
asm_add.c : add8bit.h
#ifndef ADD8BIT_H_
#define ADD8BIT_H_

extern char add8bit(char, char);
#endif /* ADD8BIT_H_ */
```

```
asm_add.c : add8bit.S
.global add8bit

add8bit:
  add  r24, r22  ; arg1: r25 and r24, arg2: r23 and r22
  ret          ; return registers are r25 and r24
```

Although this project does not cover timers or timing, the subject of this chapter, we look at it here while on the subject of calling subroutines from C. As can be seen in the add8bit.S file, R24 and R22 are used as the two char arguments of the add8bit subroutine. The C prototype for the subroutine can be seen in add8bit.h. Because char arguments are allocated in pairs by the GCC C compiler, R25 and R24 represent the first char argument, but only R24 is used. For the second argument, R23 and R22 are allocated, but only R22 is used. R25 and R24 are allocated to hold the return value by the C compiler, but only R24 is used. In main.c the sum variable is declared volatile so that the C compiler does not optimize it away. It is necessary to look at the disassembly of the code to see what is really happening. The following disassembly listing was taken from the project built for an ATtiny45.

```
asm_add.c : disassembly

--- add8bit.S ----
        add   r24, r22        ; arg1: r25 and r24, arg2: r23 and r22
00000018  ADD R24,R22         Add without carry
        ret                   ; return registers are r25 and r24
00000019  RET                 Subroutine return
--- main.c ----
{
0000001A  PUSH R28            Push register on stack
0000001B  PUSH R29            Push register on stack
0000001C  PUSH R1             Push register on stack
0000001D  IN R28,0x3D         In from I/O location
--- main.c ----
0000001E  IN R29,0x3E         In from I/O location
        sum
0000001F  LDI R24,0x5B        ; 91
        sum                   LDI R22,0x5B
00000020  LDI R24,0x22        Load immediate
00000021  RCALL PC-0x0009     Relative call subroutine
00000022  STD Y+1,R24         Store indirect with displacement
}
00000023  LDI R24,0x80        Load immediate
00000024  LDI R25,0x80        Load immediate
00000025  POP R0              Pop register from stack
00000026  POP R29             Pop register from stack
00000027  POP R28             Pop register from stack
00000028  RET                 Subroutine return
--- No source file ----
00000029  CLI                 Global Interrupt Disable
0000002A  RJMP PC-0x8000      Relative jump
```

In the above disassembly, the interrupt vector table and C runtime code is not displayed. Values are passed to the add8bit subroutine at address 0000001F and 00000020. These value are 0x5B or 91 loaded to R22, and 0x22 or 34 loaded to R24. After this, is a call to the add8bit subroutine in the form of RCALL PC-0x0009. This subroutine is located at the top of the listing at address 00000018. RCALL simply calls the subroutine which then performs the addition of R24 and R22, putting the result in R24. We know that R24 is one of the registers that holds the return value, and as this is a single byte or char return value, the other register (R25) is ignored. When the subroutine returns, execution continues at address 00000022. At this stage, R24 contains the result of the addition which is 0x7D, or 125. The next instruction which is STD Y+1,R24 assigns the return value found in R24 to the sum variable which is in SRAM. STD is a store indirect with displacement instruction that stores a register to an SRAM location, but using the Y register as an index or pointer into SRAM. The Y register currently contains a value of 0x015A on an ATtiny45, but the STD instruction specifies Y+1, so the value in R24 is saved to 0x015A+1 which is SRAM address 0x015B. Thus the result of the addition, 0x7D, is now found at address 0x015B of SRAM, which is the sum variable.

## 10.4 Polled Timer Delay

Both ATtiny13(A) and ATtiny25/45/85 microcontrollers have an 8-bit timer/counter 0. These timer/counter peripherals are highly configurable for many purposes. In this section we look at how to use these timers to generate a simple time delay, with a view to using them to generate an interrupt in the next section. For now a timer is set up to start timing, and code is used to continually check whether the timer has timed out. This continual checking of the timer in code is called polling the timer.

ATtiny25/45/85 microcontrollers actually have two 8-bit timer/counter modules or units, namely, Timer/Counter0 and Timer/Counter1. Because ATtiny13(A) microcontrollers have only Timer/Counter0, we use this timer/counter as it is common between the two 8-pin microcontroller ranges.

### 10.4.1 Timer/Counter0 Registers

I/O registers for controlling timer and counter modules all fall in the address range above 0x1F (31) which means that direct bit manipulation instructions SBI and CBI can't be used on these registers. Instructions for directly testing the states of bits in I/O registers, namely SBIS and SBIC, also only operate on addresses 0x00 to 0x1F, so can't be used with timer/counter registers. This means that to be able to use any register of a timer/counter, the register must first be read into a general purpose register R0 to R31. Figure 10.6 shows the registers used to control Timer/Counter0.

### Control Registers A and B

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| COM0A1 | COM0A0 | COM0B1 | COM0B0 | - | - | WGM01 | WGM00 |

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| FOC0A | FOC0B | - | - | WGM02 | CS02 | CS01 | CS00 |

| WGM02 | WGM01 | WGM00 | Mode | CS02 | CS01 | CS00 | Description |
|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | CTC | 1 | 0 | 1 | clkI/O/1024 |

### Output Compare

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| OCR0A7 | OCR0A6 | OCR0A5 | OCR0A4 | OCR0A3 | OCR0A2 | OCR0A1 | OCR0A0 |

### Interrupt Flag - TIFR Registers Differ Between ATtiny25/45/85 and ATtiny13(A)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| - | OCF1A | OCF1B | OCF0A | OCF0B | TOV1 | TOV0 | - |

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| - | - | - | - | OCF0B | OCF0A | TOV0 | - |

Figure 10.6: Timer/Counter0 Registers

### 10.4.1.1 Timer/Counter0 Register Addresses

The first thing to notice in Figure 10.6 is that some of the addresses of the registers are different for the ATtiny25/45/85 and ATtiny13(A). This is indicated at the Address items in the figure that have the ATtiny25/45/85 register address first, followed by the ATtiny13(A) address in brackets. For example, the register at the top of Figure 10.6 is the TCCR0A register that has an address of 0x2A on the ATtiny25/45/85, but is 0x2F on the ATtiny13(A) – check this in the Register Summary section of the datasheets. Address differences like these do not matter too much because registers names are defined in a header file which
