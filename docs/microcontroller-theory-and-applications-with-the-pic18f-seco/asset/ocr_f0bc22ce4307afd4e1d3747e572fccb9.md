PIC18F4321. The ACON1 register is also used to configure AN0 (bit 0 of PORT A) as an analog input by writing 1101 (13 decimal in Figure 10.17) at PCFG3–PCFG0 (bits 3–0 of ADCON1). Note that there are several choices to configure AN0 as an analog input. In the program, the ADCON1 is loaded with 0x0D which will select VSS and VDD as reference voltage sources, and AN0 as analog input.

In the program, the ADCON2 is loaded with 0x08 which will provide the 8-bit result left justified, select 2 TAD, and select Fosc/2. Note that proper selection of T_AD and T_acq is discussed in the last section.

The ADCON2 is used to set up the acquisition time, converter clock, and also if the result is to be left or right justified. In this example, an 8-bit result is assumed. The A/D result is configured as left justified, and therefore, the 8-bit register ADRESH will contain the result. The contents of ADRESL are ignored. As discussed in the last section, the contents of ADRESH are divided by 51 to obtain the integer part of the voltage. The fractional part of the voltage can be obtained by dividing the remainder by 5.

The final result will be in decimal with one integer digit (Integer part) followed by one digit after decimal point (Fractional part). Both integer and fractional parts of the result will be outputted to two 7447’s (BCD to 7-segment decoder) in order to display them on two seven-segment displays arranged in a row as shown in Figure 10.21. Note that both integer and fractional parts are in BCD (0–9) since the voltage is from 0 to 5V.

(a)

Using polled I/O, the PIC18F assembly language program for the voltmeter is provided in the following:

```
INCLUDE <P18F4321.INC>
D0 EQU 0x30 ; contains data for right (fractional) 7-seg
D1 EQU 0x31 ; contains data for left (integer) 7-seg
ADCONRESULT EQU 0x34 ; contains 8-bit A/D result

ORG 0x100 ; starting address of the program
MOVLW 0x10 ; Initialize STKPTR to 0x10 (arbitrary value)
MOVWF STKPTR ; since subroutines are used
CLRF TRISC ; Configure PortC as input
CLRF TRISD ; Configure PortD as output
SETF TRISA ; Configure PortA as input
MOVLW 0x01
MOVWF ADCON0 ; Select AN0 for input and enable ADC
MOVF 0x0D
MOVWF ADCON1 ; Select VDD and VSS as reference
; voltages and AN0 as analog input.

MOVLW 0x08
MOVWF ADCON2 ; Select Left justified, 2TAD and Fosc/2
START BSF ADCON0, GO ; Start A/D conversion
INCONV BTSS ADCON0, DONE ; Wait until A/D conversion is done
BRA INCONV
MOVF ADRESH,ADCONRESULT ; Move ADRESH of result
; into ADCONRESULT register
CALL DIVIDE ; Call the divide subroutine
CALL DISPLAY ; Call display subroutine
BRA START
```