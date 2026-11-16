
## 10.2.4.2 Improved Way to Pass a Value

In the previous listing it can be seen that the code is rather messy and bulky, mainly because we are passing a 32-bit value to a subroutine, so have to load up four 8-bit registers to hold the 32-bit value before every subroutine call. A way to improve the readability of the code is to use a macro. Information on macros for the AVRASM2 assembler program is found in the AVR Assembler document from Microchip.

Create a new AVR Assembler Project in Microchip Studio called wait_ms_macro.asm. Add a new Assembler File to the project called wait_ms_macro.asm. Refer back to section 10.2.3, Figure 10.4 and Figure 10.5 for a reminder on how to add a new assembler source code file to a Microchip Studio project. Add a new include file (.inc file) to the project using the same method used to add a new assembler file, except click Include File in the dialog box in Figure 10.5 of section 10.2.3. Name the new file wait_ms_macro.inc. Add the code to the three files from the listings that follow.

```
wait_ms_macro.asm : main.asm

.Include "wait_ms_macro.inc"
.equ    F_CPU     = 1000000

start:
        sbi     DDRB, DDB4        ; Set pin PB4 as output
loop:   sbi     PORTB, PORTB4     ; Set LED pin high
        M_WAIT_MS 200             ; LED on delay
        cbi     PORTB, PORTB4     ; Clear LED pin low
        M_WAIT_MS 500             ; LED off delay
        rjmp    loop

.Include "wait_ms_macro.asm"
```

In the above code, the frequency that the microcontroller is operating at must be equated to F_CPU as before. Once again, the LED attached to pin PB4 via a series resistor is blinked on and off. The difference in the above code is that first a .inc file is included at the top of the code and the macro implemented in this file, called M_WAIT_MS is called to implement the two time delays in the code. This macro is passed a value of 200 the first time it is used, and 500 the second time it is used to generate 200ms and 500ms delays.

wait_ms_macro.asm: wait_ms_macro.asm

```
wait_ms_macro:
    subi  R16, 1
    sbci  R17, 0
    sbci  R18, 0
    sbci  R19, 0
    mov   R20, R16
    or    R20, R17
    or    R20, R18
    or    R20, R19
    brbc  SREG_Z, wait_ms_macro
    ret
```

wait_ms_macro.asm: wait_ms_macro.inc

```
; The M_WAIT_MS macro generates a millisecond delay time
;macro M_WAIT_MS
; Do limit checks on F_CPU and millisecond delay value passed to macro
.if   (F_CPU > 20000000)
    .error "F_CPU too high for M_WAIT_MS macro. Maximum 20MHz"
.elif (F_CPU < 4100000)
    .error "F_CPU too low for M_WAIT_MS macro. Minimum 410kHz"
.elif (@0 < 1)
    .error "Delay time too low for M_WAIT_MS macro. Minimum 1ms"
.elif (((((F_CPU * @0) / 1000) - 30) / 10) > 0xFFFFFFF)
    .error "Time delay too big for M_WAIT_MS macro."
.endif

; Save the registers that are to be used by the delay subroutine
    push  R16
    push  R17
    push  R18
    push  R19
    push  R20

; Pass calculated cycle value to wait_ms_macro subroutine
    ldi   R16, low ((((F_CPU * @0) / 1000) - 30) / 10))
    ldi   R17, byte2((((F_CPU * @0) / 1000) - 30) / 10))
    ldi   R18, byte3((((F_CPU * @0) / 1000) - 30) / 10))
    ldi   R19, byte4((((F_CPU * @0) / 1000) - 30) / 10))

; Now call the wait_ms_macro subroutine
    rcall wait_ms_macro

; Restore the registers used by the subroutine
    pop   R20
    pop   R19
    pop   R18
    pop   R17
    pop   R16

.endmacro
```

The only difference between the wait_ms_macro.asm code and the same code from the previous project is that the NOP instructions have been removed and the name of the subroutine has been changed to match the project name. The NOP instructions were removed to change the timing, as is explained shortly.

In the wait_ms_macro.inc file is the code for the macro used in this project. As can be seen in the code, the macro starts with the .macro directive, followed by the name chosen for the macro, which is M_WAIT_MS. The .endmacro directive at the very end of the code marks the end of the macro.

Immediately after the macro name at the top of the file is the code that we previously used to check the limits of F_CPU and the limits of the time delay in milliseconds. Some of the wording of the error messages in this code has been changed to refer to the M_WAIT_MS macro, so that the user will know where the error messages are coming from, should they be triggered. The expression next to the last .elif directive has been modified to subtract a value of 30, instead of 10 as was done in the previous code. This has to do with the changed timing of the code, as is explained later. The final change to this part of the code is that @0 has been substituted into two places that previously contained MS_TIME_DEL. As the AVR Assembler document explains, a macro can be passed up to 10 parameters, named @0 to @9. As we are only passing one parameter to the macro we use @0, which represents the first parameter passed to the macro. When the macro is used in the code from main.asm, as shown below, it is passed a value of 200 and then 500. In the macro, @0 takes on a value of 200 the first time and takes on a value of 500 the second time. This value represents the desired delay time in milliseconds.

```
sbi     PORTB, PORTB4    ; Set LED pin high
M_WAIT_MS 200            ; LED on delay
cbi     PORTB, PORTB4    ; Clear LED pin low
M_WAIT_MS 500            ; LED off delay
rjmp    loop
```

In the macro from wait_ms_macro.inc, after the directives that check the frequency and delay time limits, the registers used by the delay subroutine that the macro calls are pushed onto the stack. These are registers R16 to R20. The same registers are popped off the stack in reverse order before the end of the macro. This is done so that when the macro is used, there is no need to keep track of whether some value crucial to the main code will be wiped out because the macro and subroutine it calls use the same register that the crucial value is stored in.

After pushing the registers onto the stack, registers R16 to R19 are loaded with the 32-bit value calculated to generate the correct number of cycles for the desired time delay. The code to do this is the same as for the previous project, except that the calculation part takes into consideration the changed number of clock cycles used by the new code, so subtracts 30 instead of 10 that was subtracted in the previous code. After loading the calculated value to R16 to R19, the wait_ms_macro subroutine is called, effectively passing the calculated value to this subroutine.

The wait_ms_macro subroutine works in the same way that the equivalent subroutine worked in the previous project. The only difference is that the NOP instructions were removed to make the additional clock cycles generated by the code before and after the main loop of the subroutine into a multiple of 10.

In the following line of code, it can be seen that 30 is subtracted instead of 10, as was done in the previous code.

```
ldi R16, low ((((F_CPU * 80) / 1000) - 30) / 10)
```

The 30 that is subtracted above is worked out as follows and includes all instructions used by the macro and subroutine that it calls.

```
; Save the registers that are to be used by the delay subroutine
push R16 ; 2 clock cycles
push R17 ; 2 clock cycles
push R18 ; 2 clock cycles
push R19 ; 2 clock cycles
push R20 ; 2 clock cycles
push R29 ; 2 clock cycles
; Pass calculated value to wait_ms_macro subroutine
ldi R16, low ((((F_CPU * 80) / 1000) - 30) / 10) ; 1 clock cycle
ldi R17, byte2((((F_CPU * 80) / 1000) - 30) / 10)) ; 1 clock cycle
ldi R18, byte3((((F_CPU * 80) / 1000) - 30) / 10)) ; 1 clock cycle
ldi R19, byte4((((F_CPU * 80) / 1000) - 30) / 10)) ; 1 clock cycle
; Now call the wait_ms_macro subroutine
rcall wait_ms_macro ; 3 clock cycles
; Restore the registers used by the subroutine
pop R20 ; 2 clock cycles
pop R19 ; 2 clock cycles
pop R18 ; 2 clock cycles
pop R17 ; 2 clock cycles
pop R16 ; 2 clock cycles
```

In the above code, the PUSH and POP instructions take up 20 clock cycles together and the LDI and RCALL instructions take up 7 clock cycles. This totals 27 clock cycles. We must now look at the clock cycles in the wait_ms_macro subroutine, as follows.
