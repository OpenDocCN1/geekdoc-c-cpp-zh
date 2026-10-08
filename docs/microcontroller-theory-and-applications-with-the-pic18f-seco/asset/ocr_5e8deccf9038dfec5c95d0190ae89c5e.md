```
MAIN
    MOVW    0x60
    MOVWF   OSCCON                ; Setting the internal clock to 4MHz
    MOVW    0x10
    MOVWF   STKPTR                ; Initialize STKPTR
                                  ; since interrupt is used
    MOVW    0x00
    MOVWF   TRISC                 ; Make PORTC output
    MOVW    0x02
    MOVWF   T2CON                 ; Configure Timer2 with prescale 16 and
                                  ; no postscale
    CLR     TMR2
    BCF     PIR1,TMR2IF           ; Clears Timer2 flag
    MOVW    0x31                  ; Use AN12 as ADC
    MOVWF   ADCON0
    MOVW    0x00
    MOVWF   ADCON1                ; Enable pins for analog input
    MOVW    0x08
    MOVWF   ADCON2                ; 2 TAD and Fosc/2, Left justified
    MOVW    0x0C
    MOVWF   CCP1CON               ; Select PWM mode
    MOVW    D'77'                 ; Set period of PWM signal
    MOVWF   PR2
START   BSF     ADCON0,GO         ; Start the ADC
WAIT    BRA     WAIT              ; Wait for ADC to interrupt
        BRA     START             ; Start ADC again
        ORG     0x200             ; start of the Service routine
ADIF_ISR  MOVFF   ADRESH, 0x20     ; Move value in ADRESH to 0x200
                                  ; Divide by 3 using repeated addition
        MOVW    0x03              ; Move 3 into the WREG
        CLRF    0x21              ; Clear value in 0x21
DIVIDE  CPFSGT  0x20              ; Compare the value to 3 skip if greater than
        BRA     FINISHED          ; Division is done
        INC     0x21, F           ; Increment 0x21
        SUBWF   0x20              ; Subtract 3 from 0x20
        BRA     DIVIDE            ; Subtract again
FINISHED MOVFF   0x21, CCP1L     ; Move final value into CCP1L
        BCF     PIR1,TMR2IF       ; Clear Timer2 flag
        BSF     T2CON,TMR2ON      ; Turn on Timer2
AGAIN   BTFSS   PIR1,TMR2IF       ; Wait until cycle is over
        BRA     AGAIN
        RETFIE                    ; Return to start ADC again
        END
```

(b) The C-program is provided below:

```
#include <p18f4321.h> 
void ADINT_ISR(void); 
#pragmama interrupt check_int 
void check_int(void) 
{ 	ADINT_ISR();
```