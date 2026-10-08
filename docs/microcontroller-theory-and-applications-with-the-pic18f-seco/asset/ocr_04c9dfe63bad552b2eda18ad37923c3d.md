```
BSF       INTCON, GIEH  ; Enable global high interrupts
            BSF       INTCON, GIEL  ; Enable global low interrupts
OVER        CLRF      PORTD     ; Turn both LED’s off
            BRA       OVER      ; Wait for interrupt
; SERVICE ROUTINE FOR HIGH PRIORITY
            ORG       0x200
HIGH_INT_ISR BCF      INTCON,INT0IF ; Clear the interrupt flag
CHECK       BTFS      PORTB,RB0 ; Check to see if comparator output is
                              ; still one
            RETFIE
            MOVLW     0x01      ; Turn on LED at bit 0 of PORTD
            MOVWF     PORTD
            BRA       CHECK
; SERVICE ROUTINE FOR LOW PRIORITY
            ORG       0x300
LOW_INT_ISR BCF      INTCON3,INT1IF ; Clear the interrupt flag
CHECK1      BTFS      PORTB,RB1 ; Check to see if switch is still one
            RETFIE
            MOVLW     0x02      ; Turn on LED at bit 1 of PORTD
            MOVWF     PORTD
            BRA       CHECK1
            END
```

# (b)		C-program

Implementing the above design, this example demonstrates the interrupt priority system of the PIC18F microcontroller. Using interrupt priority, the user has the option to have various interrupts assigned as either low priority or high priority interrupts. If a low priority interrupt and a high priority interrupt occur at the same time, the PIC18F will always service the high priority interrupt first.

In the above example, the high priority is assigned to the comparator while the switch is assigned with the low priority. Hence, if both interrupts were triggered at the same time, then the LED associated with the comparator would be turned ON first, and then the LED associated with the switch will be turned ON. Note that the external interrupt INT0 can only be a high priority interrupt. Hence, INT0 is connected to the comparator output while the switch is connected to INT1 since it has the low priority. At the end of the code provided below, it can be seen that there are two interrupt service routines, HP_COMP_ISR and LP_SWITCH_ISR, which are the high priority and low priority service routines.

The following code implements priority interrupts on the PIC18F using C-language:

```
#include <P18F4321.h>
void HP_COMP_ISR(void);
void LP_SWITCH_ISR(void);

#pragma code High_Priority_COMP_Int=0x08  //High interrupt code jumps here
void COMP_Int(void)
{
  _asm  //Using assembly language
  GOTO HP_COMP_ISR()
```