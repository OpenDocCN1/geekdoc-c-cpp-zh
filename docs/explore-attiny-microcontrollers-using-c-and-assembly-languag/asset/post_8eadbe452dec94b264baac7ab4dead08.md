
In the polled timer projects, TIFR was directly used and is defined with a different name for the ATtiny13(A) and ATtiny25/45/85. We used the .ifndef directive to make the code work for both ATtiny device ranges. In the timer0_unit_int.asm project, TIFR is not directly used, but TIMSK is. This register is named TIMSK0 for an ATtiny13(A), but TIMSK for an ATtiny25/45/85, so the same .ifndef code is used, but this time for the TIMSK register rather than for the TIFR register, as can be seen at the top of the code listing. When the OCIE0A bit is set in the TIMSK register in the code, it works for both ATtiny13(A) and ATtiny25/45/85 devices even though this bit is at different positions in the registers of the two ATtiny ranges, as can be seen in the datasheets. Again, this works because it is correctly defined in the header file for the chosen device in Microchip Studio.

Unused vector table entries have been removed from the code. Timer 0 compare match A interrupt vector is included in the code using the name OC0Aaddr defined for this address in the ATtiny include files. As already explained, this name is used with the .org directive to set the correct address for the timer 0 compare match A interrupt vector. OC0Aaddr is defined as 0x0006 in ATtiny13(A) include files, but as 0x000A in ATtiny25/45/85 files, causing the vector to be placed at the correct address for the chosen device. Because the unused vector table entries were removed, there is no need for the dummy ISR code, which has also been removed from the bottom of the file.

### 10.5.4 C Program Timer Interrupt

A C program that is the equivalent of the previous assembly language timer 0 interrupt programs follows. Create a new GCC C Executable Project called timer0_interrupt_c and enter the code from the following listing into main.c. The project can be set up for an ATtiny13(A) or ATtiny25/45/85.

At the start of the code, the interrupt.h file is included below the usual io.h file. This allows interrupts to be implemented in the C code as the file contains the necessary definitions and functions for interrupt handling. As was done in the previous assembly language program, TIMSK is defined as TIMSK0 if TIMSK is not defined. This of course happens when an ATtiny13(A) is selected and only TIMSK0 is defined in the header file.

In the main code, pin PB4 is set up as an output pin and timer 0 is set up in CTC mode as before. A value is written to OCR0A for the compare match. As with the assembly language code, the OCIE0A bit is set in the TIMSK register to enable the timer 0 compare match interrupt. After this, the SEI instruction must be run. Because this is C code, SEI can not be inserted directly in the code. The sei() macro is made available by including the interrupt.h file in order for the global interrupt enable bit, or I bit, in the status register to be set. As before, the timer is started by selecting the system clock divided by 1024 as the timer 0 clock source.

```
timer0_interrupt.c : main.c

#include <avr/io.h>
#include <avr/interrupt.h>

#ifndef TIMSK
#define TIMSK TIMSK0
#endif

int main(void)
{
  DDRB = (1 << DDB4);       // Pin PB4 as output pin
  TCCR0A = (1 << WGM01);    // CTC mode
  OCR0A = 0xFF;             // Output compare value
  TIMSK = (1 << OCIE0A);    // Enable T0A compare match interrupt
  sei();                    // Set global interrupt enable bit
  TCCR0B = (1 << CS02) | (1 << CS00); // Prescaler clk/1024 and start timer
  while(1) {
  }
}

ISR(TIM0_COMPA_vect)
{
  PINB = (1 << PORTB4);     // Toggle pin PB4/LED
}
```

Because C does not have a standard way to handle interrupts, compiler manufacturers implement their own ISR scheme. In the AVR GCC C compiler used by Microchip Studio, an interrupt service routine must use the ISR() macro that is defined in the interrupt.h file, as can be seen at the bottom of the above code listing. The name of the interrupt to implementation must be passed to the ISR() macro. Interrupt names are found in the header file for the AVR part chosen in Microchip Studio, for example the iotn13.h file for the ATtiny13(A) or the iotn45.h for the ATtiny45. The correct file for the chosen part is automatically included in the project by including io.h in the project. This file can be found and opened by expanding the Dependencies folder in the Solution Explorer pane at the right of Microchip Studio. The definition name for the timer 0 compare match A interrupt that must be passed to the ISR() macro is found here and is called TIM0_COMPA_vect.

The C code project works exactly the same as the assembly language version of the project, toggling the LED on pin PB4 when timer 0 triggers a compare match A interrupt. Look at the disassembly of the code to see that the RETI instruction is automatically inserted at the end of the interrupt service routine, so that program execution returns correctly from the ISR. A breakpoint can be put on the closing brace of the ISR and the code run in the simulator. The changing bit in the PORTB register can then be seen, just as was done for the assembly language program.

### 10.6 Summary

This chapter has been rather long, but has covered a lot of important and interesting information to do with instruction timing, timers and interrupts. The following list summarizes what we have covered.

- 8-bit AVR microcontrollers have different CPU versions with the ATtiny13(A) and ATtiny25/45/85 CPU version being the AVRe.
- Instruction timing may be different for the same instruction, depending on the AVR CPU version. Refer to the AVR Instruction Set Manual for the actual instruction execution time in clock cycles.
- A software time delay can be accurately generated by writing a subroutine that uses an exact number of clock cycles.
- Assembly language programs can be split into more than one file by including external files in a main file.
- Assembly language subroutines can be called from within C code.
- Hardware timers on AVR microcontroller can be polled or interrupt driven.
- Each different AVR microcontroller has its own interrupt vector table that depends on how many interrupt sources the device has built into it.
- An interrupt service routine or ISR is a type of subroutine written to handle an interrupt. The RETI instruction must be used to return from an ISR.

## Chapter 11 • The AVR Instruction Set

Now that many of the AVR instructions from the AVR instruction set have been used in preceding chapters, and the AVR architecture has been covered, it is time to look at the remaining AVR instructions.

This chapter summarizes instructions from the AVR instruction set that have already been used, and looks at the remainder of the instructions that have not yet been covered.

### In this Chapter

- AVR instruction set overview and categories
- A guided tour through the ATtiny AVR instruction set
- Implement an LED chaser or “Knight Rider” display using shift instructions
- A look at AVR instructions that are not available in ATtiny parts

### 11.1 AVR Instruction Set Overview and Categories

There are two important things to note with regards to the AVR instruction set. Firstly, not all instructions are included in the instruction set of all devices because not all devices have the same memory, hardware, and built-in peripherals. Secondly, the AVR CPU has been updated several times since its inception, which means that there are several different versions of the AVR 8-bit CPU, as was covered in the previous chapter. This means that there are additional instructions in some of the newer CPU versions.

In the Instruction Set Summary section of the datasheets for AVR microcontrollers, instructions are categorized into five sections, namely 1) arithmetic and logic instructions, 2) branch instructions, 3) bit and bit test instructions, 4) data transfer instructions, and 5) MCU control instructions. In the guided tour through the entire instruction set that follows in the next section, instructions are covered in the same categories as the datasheet and using the same category headings for easy cross reference. Each main category has been further subdivided where appropriate.

### 11.2 A Guided Tour through the ATtiny AVR Instruction Set

This section looks at the part of the AVR instruction set implemented on ATtiny devices with a summary of the instructions that were used so far in the book, and commentary on instructions that were not used. Example code is included where appropriate.

### 11.2.1 Arithmetic and Logic Instructions

The arithmetic and logic instructions category includes addition, subtraction and the logic instructions AND, OR and EOR. It also includes increment, decrement, sign change, bit set, bit clear, register set, register clear and register test instructions. Arithmetic and logic instructions have been further divided down into more precise subcategories in the subsections that follow.

### 11.2.1.1 Add and Subtract Instructions

ATtiny25/45/85 and ATtiny13(A) microcontrollers implement three addition instructions and five subtraction instructions summarized in the following sections.

### Addition Instructions

- ADD (Add without Carry)
- ADC (Add with Carry)
