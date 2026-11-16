the subroutine is called. In this way, a new value can be passed to the subroutine each time that it is called. This is shown in the main.asm listing of the wait_pass_val_asm project below.

```
wait_pass_val.asm : main.asm

.equ	F_CPU		 = 1000000
.equ	MS_DELAY_1	 = (((F_CPU * 200) / 1000) - 10) / 10) ; 200ms
.equ	MS_DELAY_2	 = (((F_CPU * 500) / 1000) - 10) / 10) ; 500ms

start:	sbi	DDRB, DDB4		 ; Set pin PB4 as output

loop:	sbi	PORTB, PORTB4		 ; Set LED pin high
	ldi	R16, low (MS_DELAY_1)	 ; Pass 32-bit value
	ldi	R17, byte2(MS_DELAY_1)	 ; to the wait_pass_val
	ldi	R18, byte3(MS_DELAY_1)	 ; subroutine
	ldi	R19, byte4(MS_DELAY_1)	 ;
	rcall	wait_pass_val		 ; LED on delay
	cbi	PORTB, PORTB4		 ; Clear LED pin low
	ldi	R16, low (MS_DELAY_2)	 ; Pass 32-bit value
	ldi	R17, byte2(MS_DELAY_2)	 ; to the wait_pass_val
	ldi	R18, byte3(MS_DELAY_2)	 ; subroutine
	ldi	R19, byte4(MS_DELAY_2)	 ;
	rcall	wait_pass_val		 ; LED off delay
	rjmp	loop

.include "wait_pass_val.asm"
```

At the top of the code, two names are equated with values that are worked out using the formula that we are now familiar with. The first value works out the number of cycles for the subroutine to delay for to generate a 200ms delay, and the second for a 500ms delay. These values are then loaded to registers R16 to R19 before wait_pass_val is called. In this way, the values have been passed to the wait_pass_val subroutine because the subroutine uses these values to generate the time delays.

Note that in the above code, if measuring the number of cycles used by the subroutine in the simulator, the cycles must be measured starting from where the first part of the 32-bit number is loaded to R16. The reason for this is that the formula for calculating the number of cycles to generate has not been modified to remove the cycles used to pass the value to the subroutine. In any case, this may be the behavior we prefer, as these instructions still use up cycles that can be considered part of the delay that we are generating. Note that 3 extra cycles are added to the total because of the RCALL instruction which is now