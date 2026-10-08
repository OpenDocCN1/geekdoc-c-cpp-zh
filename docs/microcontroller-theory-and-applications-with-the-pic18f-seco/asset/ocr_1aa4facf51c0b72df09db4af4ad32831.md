**Assigning interrupt priorities using the C18 compiler** The C18 compiler uses the directives "interrupt" and "interruptlow" to specify high and low priority interrupt levels. The programmers can use these directives which allow a program to branch automatically from the respective interrupt address vector to a different program to find the source of the interrupt (for multiple interrupts with priorities), and then to the appropriate service routine.

As mentioned before, the PIC18F supports up to two levels of interrupt priority. Most interrupts have a priority bit associated with the interrupt flag enable bits that assigns it to one of the two priority levels. Use of priority level is optional, and the PIC18F may be configured to use only one level priority. When two levels of interrupt priority are used, an interrupt of either priority level may interrupt the main program. However, only a High Priority Interrupt may interrupt a Low Priority Interrupt, and nothing may interrupt a High Priority Interrupt.

If only a single level of interrupts were used (IPEN bit in RCON register = 0), then it is only necessary to define the interrupt vector 0x00008 and a single interrupt service routine function with the directive "#pragma interrupt". All priority bit settings are ignored. The functions of GIEH and GIEL bits in the INTCON register become GIE (Global Interrupt Enable) and PIE (Peripheral Interrupt Enable) bits, with the following functions:

| INTCONbits.GIE | INTCONbits.PIE | Interrupt Functions |
| :--- | :--- | :--- |
| 0 | 0 | No interrupts;all interrupts disabled since GIE = 0. |
| 0 | 1 | No interrupts;all interrupts disabled since GIE = 0. |
| 1 | 0 | Only interrupts in INTCONx enabled; all peripheral interrupts remain disabled |
| 1 | 1 | All interrupts including peripherl interrupts are enabled |

**A typical structure for interrupt programs using C** The default interrupt INT0 with vector address 0x00008 is used in the following to illustrate the interrupt programs using C. Typical structures for the main program and the service routine (when the service routine requires more than eight words) are provided below:

```
#include <PIC4321.h>
void ISR (void);
#pragma code Int=0x08 // At interrupt code jumps here
void Int(void)
{
 _asm // Using assamblea language
 GOTO ISR
 _endasm
}
#pragma code // Main program
void main()
{
// Typically configure ports, enable INTOIE, clear INTOIF
while(1){ // Wait in an infinite loop for the interrupt to occur
}
```