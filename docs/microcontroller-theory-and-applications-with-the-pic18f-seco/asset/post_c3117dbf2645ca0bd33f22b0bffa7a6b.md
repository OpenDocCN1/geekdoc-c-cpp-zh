
### (b) Using C:

In this example, an LM339 comparator is interfaced with the PIC18F4321 using C and external interrupts. An external interrupt allows the microcontroller to trigger an interrupt from a source outside the PIC18F4321 such as a comparator. As with the previous interrupt example, the code starts with the `#pragma` command which will place code fragments at specific locations in memory; when the interrupt is triggered, the microcontroller will automatically jump to memory location `0x000008` and finally to `COMP_ISR`.

In the main program, PORTD is configured as an output, and PORTB is configured as a digital input. The external interrupt flag and the global interrupt enable are enabled. The main program then waits in an infinite 'while' loop that turns the LED OFF until the comparator output is HIGH, interrupting the microcontroller. After recognizing the interrupt, the code will automatically jump to address `0x000008`, and then jump to the service routine at `COMP_ISR` via the code at `Int_Output`. Within the service routine, the code will continue to take the switch data from PORTB and output the data to the LED via PORTD. It will continue to do this as long as the comparator output stays HIGH. When Vx is lower than Vy, the comparator will output 0 and the code will return to the infinite 'while' loop and turn the LED OFF. The PIC18F program using C is provided below:

```c
#include <PIC18F4321.h>
void COMP_ISR(void);
#pragma code COMP_Int=0x08 //At interrupt code jumps here
void COMP_Int(void)
{
_asm                // Using assembly language
GOTO COMP_ISR
_endasm
}
#pragma code
void main()
{
TRISD=0x00;                     // PORTD is output
ADCON1=0x0F;                   // Configure RB1 and INT0 as digital input
INTCONbits.INT0IE=1;           // Enable external interrupt
INTCONbits.INT0IF=0;          // Clear the external interrupt flag
INTCONbits.GIE=1;             // Enable global interrupts
PORTD=0;                      // Turn off LED;
while(1){  // wait in an infinite loop for the interrupt to occur
PORTD=0;                      // LED is off
}
}
# pragma interrupt COMP_ISR
void COMP_ISR(void) //start of the Comparator interrupt service routine
{
INTCONbits.INT0IF=0;          // Clear external interrupt flag
while(PORTBbits.RB0==1){ // Check if comparator is high
PORTD = PORTB;              // Move PORTB into PORTD
}
}
```

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_256_0.png)

**FIGURE 9.11** Figure for Example 9.3

## Example 9.3

In Figure 9.11, if Vx > Vy, the PIC18F4321 is interrupted via INT0. On the other hand, opening the switch will interrupt the microcontroller via INT1. Note that in the PIC18F4321, INT0 has the higher priority than INT1.

### (a) Write the main program in PIC18F assembly language at address 0x100 that will perform the following:

- Initialize STKPTR to 0x12
- Configure PORTB as interrupt inputs.
- Clear interrupt flag bits of INT0IF in INTCON reg and INT1IF in INTCON3 reg
- Configure PORTD (bits 0, 1) as outputs for LEDs
- Set INT1 as a low priority interrupt by clearing INT1IP bit in INTCON3 reg
- Enable priority interrupts by setting IPEN bit in RCON reg
- Enable global HIGH and LOW interrupts by setting GIEH and GIEL bits in INTCON reg
- Turn both LEDs at PORTD OFF.
- Wait in an infinite loop, and wait for one or both interrupts to occur.
- Turn both LEDs at PORTD OFF (Comparator LED at bit 0 of PORTD and Switch LED at bit 1 of PORTD)
- Wait in an infinite loop for one or both interrupts to occur.

Also, write a service routine in PIC18F assembly language at address 0x200 for the high priority interrupt (INT0) that will perform the following:

- Clear interrupt flag for INT0 (INT0IF)
- Check to see if the comparator output is still 1. If it is, turn the LED ON at bit 0 of PORTD.

Finally, write a service routine in PIC18F assembly language at address 0x300 for the low priority interrupt (INT1) that will perform the following:

- Clear interrupt flag for INT1 (INT1IF)
- Turn LED ON at bit 1 of PORTD

### (b) In Figure 9.11, if Vx > Vy, the PIC18F4321 is interrupted via INT0. On the other hand, opening the switch will interrupt the microcontroller via INT1. Note that in the PIC18F4321, INT0 has the higher priority than INT1. Write the main program in C that will perform the following:

- Configure PORTB as interrupt inputs.
- Clear interrupt flag bits of INT0IF in INTCON reg and INT1IF in INTCON3 reg
- Configure PORTD (bits 0, 1) as outputs for LEDs
- Set INT1 as low priority interrupt by clearing INT1IP bit in INTCON3 reg
- Enable priority interrupts by setting IPEN bit in RCON reg
- Enable global HIGH and LOW interrupts by setting GIEH and GIEL bits in INTCON reg
- Turn both LEDs at PORTD OFF.
- Wait in an infinite loop, and wait for one or both interrupts to occur

Also, write a service routine in C-language for the high priority interrupt (INT0) that will check to see if the comparator output is still 1. If it is, turn LED at bit 0 of PORTD ON. If the comparator output is 0, return.

Finally, write a service routine in C language for the low priority interrupt (INT1) that will perform the following:

- Clear interrupt flag for INT1
- Check to see if the switch is still 1. If it is, turn LED at bit 1 of PORTD ON, If the switch input is 0, return.

# Solution

This example will demonstrate the interrupt priority scheme of the PIC18F4321 microcontroller. With interrupt priority, the user has the option to have the interrupts declared as either low or high interrupts. If at anytime the low and high priority interrupts occur at the same time, the microcontroller will always service the high priority interrupt. In the above example, the comparator is set as the high priority and the switch is set as the low priority, so if both interrupts are triggered simultaneously, then only the LED associated with the comparator will be turned ON.

Note that the external interrupt INT0 can only be a high priority interrupt. When implementing a single interrupt, the interrupt service routine is written at address 0x08. On the other hand, when priority interrupts are enabled, the service routine for the high priority interrupt is written at address 0x08 while the service routine for the low priority interrupt is written at address 0x018.

In order to enable the second external interrupt, INT1, the register INTCON3 is configured. Also, INT1IE must be enabled, and INT1IF must be cleared to 0. Furthermore, the INT1IP bit in INTCON3 register that sets the priority of INT1 in the INTCON3 register must be cleared to 0 for low priority. Next, the IPEN bit in the RCON register that enables the interrupt priority functionality of the PIC18F4321 must be set to one. Finally, the GIEH and GIEL bits in the INTCON register must be set to one in order to enable global high and low interrupts.

### (a) PIC18F assembly language program:

```asm
INCLUDE <P18F4321.INC>
; RESET
                ORG             0       ; Reset vector
                BRA           MAIN      ; Jump to main program
; HIGH PRIORITY INTERRUPT ADDRESS VECTOR
                ORG             0x0008  ; High priority interrupt
                BRA           HIGH_INT_ISR
                                        ; Jump to service routine for the
                                        ; comparator
; LOW PRIORITY INTERRUPT ADDRESS VECTOR
                ORG             0x0018  ; Low priority interrupt
                BRA           LOW_INT_ISR
                                        ; Jump to service routine for the
                                        ; comparator
                ORG             0x0100
                ; MAIN PROGRAM
MAIN            MOVWF        0x12      ; Initialize STKPTR to 0x12
                MOVWF        STKPTR
                CLRF         TRISD     ; PORTD is output
                MOVLW        0x0F      ; Configure ADCON1 to set up
                MOVWF        ADCON1    ; INT0 and INT1 as digital inputs
                BSF          INTCON, INT0IE  ; Enable the external interrupt INT0
                BSF          INTCON3, INT1IE ; Enable the external interrupt INT1
                BCF          INTCON, INT0IF  ; Clear the INT0IF flag
                BCF          INTCON3, INT1IF ; Clear the INT1IF flag
                BCF          INTCON3, INT1IP   ; Configure INT1 as low priority
                BSF          RCON, IPEN      ; Enable priority interrupt
```
