
This chapter has everything to do with instruction timing, software time delay subroutines, hardware timers, and interrupts on ATtiny microcontrollers.

While studying the above topics, this chapter also covers additional assembler instructions and assembler directives, as well as how to split an assembly language project into more than one file. It takes a look at how to derive a formula for the time taken by a software delay subroutine, and how to pass a value to a subroutine as well as how to call an assembly language subroutine from C code.

## In this Chapter

- AVR CPU versions and instruction timing
- An analysis of an assembly language software time delay subroutine
- How to write a cycle accurate software delay subroutine
- Split an assembly language program into multiple files
- Call an assembly language subroutine from a C program
- Polled operation of a hardware timer
- Interrupt operation of a hardware timer

## 10.1 Instruction Timing

The time that an instruction takes to execute is determined by the number of clock cycles that a particular instruction takes to execute as well as the frequency that the microcontroller is operating at. Find the number of clock cycles that instructions take to execute on an ATtiny or other 8-bit AVR microcontroller in the AVR Instruction Set Manual. This information can also be found in the Instruction Set Summary section of the datasheet for a particular AVR part or range of parts.

### 10.1.1 AVR CPU Versions

According to the AVR Instruction Set Manual, there are six different versions of the AVR 8-bit CPU, namely AVR, AVRe, AVRe+, AVRxm, AVRxt and AVRrc. These different CPU versions came about because of updates and enhancements to the AVR CPU over a period of time. Some differences in instruction timing exist between some of the different CPU versions. Instruction timing for AVR, AVRe and AVRe+ CPU versions are identical.

ATtiny25/45/85 and ATtiny13(A) microcontrollers fall into the AVR, AVRe and AVRe+ group of AVR CPU versions. It is important to know that there are differences in instruction timing if ever writing software for AVR devices that must run on different AVR CPU versions, if the software relies on the timing of certain instructions.

### 10.1.2 Instruction Timing Examples

Examples of timing for some instructions follow and help to illustrate what instruction timing is about.

#### 10.1.2.1 The NOP Instruction

A simple instruction such as the NOP (No Operation) instruction takes one clock cycle to execute on all of the different AVR 8-bit CPU versions. A NOP instruction does nothing, except use up one clock cycle of CPU time. In other words, it does not cause any changes to memory or any registers including the status register.

To work out how much time an instruction takes to execute, we need to find out at what frequency the microcontroller is being clocked, and the number of clock cycles that the particular instruction takes to execute. For the NOP instruction, we know that one clock cycle is used up to execute it. For the ATtiny25/45/85 we know that the default clock frequency is 1MHz and for the ATtiny13(A) the default clock frequency is 1.2MHz.

As we have already seen in section 6.1.2.5 of Chapter 6, the period of a clock cycle is calculated by dividing 1 by the frequency of the clock source. This gives us a period of 1 / 1MHz which is 1µS for the ATtiny25/45/85, and 1 / 1.2MHz which is 0.833µS for the ATtiny13(A). A NOP instruction therefore takes 1µS to execute on an ATtiny25/45/85 running at the default 1MHz clock frequency, and 0.833µS on an ATtiny13(A) running at a default clock frequency of 1.2MHz.

You may be wondering what the purpose of the NOP instruction is, as it does not do any calculation or move any data. One basic use of the NOP instruction is to use it in a software time delay function or subroutine to use up some of the CPU time, but there are other uses for the NOP instruction in the AVR.

In the datasheets for the ATtiny microcontrollers that are covered in this book, there is an example of the use of the NOP instruction in the I/O Ports section. This example shows that when a write to a port register is immediately followed by a read from a port register, a NOP instruction must be inserted between the write and read. Because of timing factors in this situation, a NOP instruction must be included to be able to read back the value recently assigned to some of the pins. Part of this code from the datasheets is shown below, where a NOP is inserted between the OUT and IN instructions.

```
out DDRB, r16 ; Port pin data direction setup
nop ; Insert NOP for synchronization
in r17, PINB ; Read port pins
```

The same must be done in a C program as the following example code shows.

```
DDRB = (1 << DDB0); // Port pin data direction setup
_NOP(); // Insert NOP for synchronization
i = PINB; // Read port pins
```

In order to use _NOP() (which is a macro not a function, and simply inserts a NOP), in a C program, the cpufunc.h header must be included in the C program as follows.

```
#include <avr/cpufunc.h>
```

Other uses of NOP are to make sure that there is a line of code on which to place a breakpoint when debugging optimized C code. NOP can also be used in the interrupt vector table at unused vector locations to ensure that the used vector entries occur at the correct address, although there are other solutions for unused interrupt vectors.

#### 10.1.2.2 16-bit and 32-bit Instruction Timing

Most AVR instructions are 16 bits wide, as has already been mentioned. These instructions usually execute in one clock cycle, but there are some exceptions. We have already seen the 16-bit NOP instruction that executes in one clock cycle. Another example of a 16-bit instruction that executes in one clock cycle is the ADD instruction, that takes one clock cycle on all of the AVR CPU versions.

One of the exceptions of a 16-bit instruction that executes in two clock cycles is the ADIW (Add Immediate to Word) instruction. The 16-bit CBI instruction takes two clock cycles to execute on the AVRe CPU version, but one clock cycle on the AVRxm, AVRxt and AVRrc CPU versions. An example of a 32-bit instruction that executes in two clock cycles on the AVRe CPU version is the LDS instruction. The LPM instruction, although 16-bits wide takes three clock cycles to execute.

The point of this discussion on instruction timing is that one really needs to consult the datasheet for a particular AVR part, and the instruction set manual, if execution time of instructions is important in a particular application.

#### 10.1.2.3 Timing of Branch Instructions

Some branch instructions take a different number of clock cycles to execute, depending on the result of the test that the instruction performs. The RJMP instruction is one of the branch instructions that does not jump depending on a result, it always jumps to a specific location. The RJMP instruction therefore always executes in two clock cycles.

SBIC (Skip if Bit in I/O Register is Cleared) is a branch instruction that we have previously used. This instruction executes in either 1 clock cycle, 2 clock cycles or 3 clock cycles, depending on whether 1) the condition is false (does not skip), 2) the instruction skipped over is one word (16 bits), or 3) the instruction skipped over is two words (32 bits). The timing of the SBIS (Skip if Bit in I/O Register is Set) instruction works the same as the SBIC instruction, except that the skip occurs if the bit that is tested in the register is set.

Looking at the read_switch_asm code listing from section 8.2.5 of Chapter 8, which follows with instruction timing added, we can see that the first three instructions each take two clock cycles to execute. These times are for the AVRe CPU version found in ATtiny13 and ATtiny25/45/85 devices. On the AVRxm, AVRxt and AVRrc, these same SBI and CBI instructions take one clock cycle each to execute. The first SBIC instruction, found under the loop label executes in either 1 clock cycle or 2 clock cycles. In this particular case, it will never take 3 clock cycles to execute because it is followed by a CBI instruction, which is a one word or 16-bit instruction.

```
read_switch.asm : main.asm
sbi   DDRB, DDB4      ; 2 clock cycles -------- LED connected to PB4
cbi   DDRB, DDB3      ; 2 clock cycles -------- Switch connected to PB3
sbi   PORTB, PORTB3   ; 2 clock cycles -------- Enable pull-up on PB3
loop:
sbic  PINB, PINB3     ; 1 or 2 clock cycles --- Skip if switch closed
cbi   PORTB, PORTB4   ; 2 clock cycles, 16-bit -- Switch LED off
sbis  PINB, PINB3     ; 1 or 2 clock cycles --- Skip if switch open
sbi   PORTB, PORTB4   ; 2 clock cycles, 16-bit -- Switch LED on
rjmp  loop            ; 2 clock cycles
```

With the switch open, the timing of the above code works as follows.

```
sbi   DDRB, DDB4      ; 2 clock cycles -------- LED connected to PB4
cbi   DDRB, DDB3      ; 2 clock cycles -------- Switch connected to PB3
sbi   PORTB, PORTB3   ; 2 clock cycles -------- Enable pull-up on PB3
loop:
sbic  PINB, PINB3     ; 1 clock cycle, no skip --- Skip if switch closed
cbi   PORTB, PORTB4   ; 2 clock cycles, 16-bit -- Switch LED off
sbis  PINB, PINB3     ; 2 clock cycles, skip word -- Skip if switch open
sbi   PORTB, PORTB4   ; 0 clock cycles, skipped over
rjmp  loop            ; 2 clock cycles
```

Thus 6 clock cycles are used up before entering the loop, which gives 6 x 1µS = 6µS for the ATtiny25/45/85, and 6 x 0.833µS = 5µS for the ATtiny13(A). Add all of the clock cycles from the loop in the above listing to calculate the total number of clock cycles that it takes to execute. This gives us 7 clock cycles. Execution time of the loop is therefore 7 x 1µS = 7µs for the ATtiny25/45/85, and 7 x 0.833µs = 5.833µs for the ATtiny13(A).

With the switch closed, the timing of the loop works as follows.

```
loop:
sbic  PINB, PINB3     ; 2 clock cycles, skip ----- Skip if switch closed
cbi   PORTB, PORTB4   ; 0 clock cycles, skipped over
sbis  PINB, PINB3     ; 1 clock cycle, no skip --- Skip if switch open
sbi   PORTB, PORTB4   ; 2 clock cycles, 16-bit --- Switch LED on
rjmp  loop            ; 2 clock cycles
```
