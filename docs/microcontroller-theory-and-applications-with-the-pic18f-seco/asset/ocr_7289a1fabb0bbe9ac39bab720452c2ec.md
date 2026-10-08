```
; MAIN PROGRAM
            ORG         0x00100    ; MAIN PROGRAM
MAIN_PROG    MOVWF    0x10        ; Initialize STKPTR to 0x10
             MOVWF    STKPTR
             BCF      TRISD, TRISD1 ; Configure bit 1 OF PORTD as output
             MOVWF    0x0F         ; Configure bit 0 of PORTB as INT0
             MOVWF    ADCON1       ; and bit 1 as input
             BCF      INTCON, INTOIF ; Clear INTOIF flag
             BSF      INTCON, GIE   ; Enable global interrupts
             BSF      INTCON, INTOIE ; Enable the external interrupt
WAIT          BRA      WAIT          ; Wait for interrupt
             BRA      MAIN_PROG     ; Repeat
; INTERRUPT SERVICE ROUTINE
             ORG      0x000008      ; Interrupt Address Vector
INT_SERV      MOVFF    PORTB, PORTD ; Output switch status to turn LED ON/OFF
            BCF      INTCON, INTOIF ; Clear the external interrupt flag to avoid
                                     ; double interrupt
             RETFIE                 ; Enable interrupt and return
             END
```

(b) Using C:

In this example, an LM339 comparator is interfaced with the PIC18F4321 using C and external interrupts. An external interrupts allows the microcontroller to trigger an interrupt from a source outside the PIC18F4321 such as a comparator. As with the previous interrupt example, the code starts with the #pragma command which will place code fragments at specific locations in memory; when the interrupt is triggered, the microcontroller will automatically jump to memory location 0x000008 and finally to COMP_ISR.

In the main program, PORTD is configured as an output, and PORTB is configured as a digital input. The external interrupt flag and the global interrupt enable are enabled. The main program then waits in an infinite ‘while’ loop that turns the LED OFF until the comparator output is HIGH, interrupting the microcontroller. After recognizing the interrupt, the code will automatically jump to address 0x000008, and then jump to the service routine at COMP_ISR via the code at Int_Output. Within the service routine, the code will continue to take the switch data from PORTB and output the data to the LED via PORTD. It will continue to do this as long as the comparator output stays HIGH. When

![](bbox=[0.15, 0.7, 0.95, 0.9])

FIGURE 9.10 Figure for Example 9.2