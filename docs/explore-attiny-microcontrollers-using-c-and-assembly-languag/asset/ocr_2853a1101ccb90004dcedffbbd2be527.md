# 10.2.2 A Better Software Delay Subroutine

An improved software delay subroutine is included in the listing below as part of the led_blink_asm code. This new program is now called wait_1s_asm and includes a subroutine called wait_1s that delays for exactly one second. At the top of the listing, the frequency of the AVR that the code is to run on must be assigned to F_CPU. As can be seen, two frequencies have been provided, with one commented out. These are of course for the ATtiny25/45/85 and ATtiny13(A) default frequencies of 1MHz and 1.2MHz respectively. When the frequency is correctly set at the top of the code, the LED attached to pin PB4 stays on for 1 second as the code in the main loop runs.

```
wait_1s.asm : main.asm

; .equ F_CPU = 1000000
.equ F_CPU = 1200000

start:
    sbi DDRB, DDB4    ; Set pin PB4 as output

loop:
    sbi PORTB, PORTB4 ; Set LED pin high
    rcall wait_1s     ; LED on delay
    cbi PORTB, PORTB4 ; Clear LED pin low
    rcall wait_1s     ; LED off delay
    rjmp loop

; 1 second delay subroutine
wait_1s:
    ldi R16, Low ((F_CPU - 10) / 10) ; Load number of loop cycles
    ldi R17, byte2((F_CPU - 10) / 10) ; to registers R16 to R19
    ldi R18, byte3((F_CPU - 10) / 10)
    ldi R19, byte4((F_CPU - 10) / 10)

wait_1s_loop:
    subi R16, 1    ; Perform decrement on 32-bit
    sbci R17, 0    ; number in R16 to R19
    sbci R18, 0
    sbci R19, 0
    mov R20, R16   ; Determine if 32-bit number is
    or R20, R17    ; zero using OR and BRBC
    or R20, R18
    or R20, R19
    brbc SREG_Z, wait_1s_loop ; Balance BRBC to 2 clock cycles
    nop            ; Balance instructions outside of
    nop            ; loop to 10 clock cycles
    ret
```