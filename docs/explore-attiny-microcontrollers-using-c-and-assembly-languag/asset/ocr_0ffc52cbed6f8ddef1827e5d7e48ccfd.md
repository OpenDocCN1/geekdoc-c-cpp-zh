A subroutine called delay is found below the loop in the main program, and can be seen in the next code snippet. It is a piece of code that can be called or run by the main program or by another subroutine. A subroutine is the equivalent of a function in the C language.

```
; Delay subroutine
delay:
 ldi  r16, 0xff
delloop1:
 ldi  r17, 0xff
delloop2:
 dec  r17        ; Delay by decrementing
 brbc SREG_Z, delloop2
 dec  r16        ; Delay by decrementing
 brbc SREG_Z, delloop1
 ret
```

The advantage of a subroutine is that a single piece of code in the subroutine can be used over and over again without having to include the entire subroutine code each time that it is used. For example, in the LED blink program the delay subroutine code is written once and called whenever needed in the main program. The delay subroutine is used to waste time while the LED is on or off so that the LED on and off states are visible to the eye. The delay subroutine is called from the main program using the RCALL assembly instruction.

The basic principle of operation of the delay subroutine is to waste time by decrementing numbers that are stored in registers. At this stage, the delay subroutine code and instructions in the main loop will not be fully explained because it is necessary to understand some of the internal registers of the microcontroller for a proper explanation. Chapter 5 looks at the AVR registers and memory map. Using the simulator in the next section also helps understanding the code. The intention here is to get a basic understanding that assembly language instructions are being executed to cause various actions to take place in the microcontroller and ultimately blink the LED.

# 3.6 Using the Debugger and Simulator

This section describes basic use of the AVR simulator and debugger in Microchip Studio. The first section that follows shows how to use the simulator with the debugger, and the second section shows how to use the debugger with physical hardware by using a USB programmer/debugger such as an Atmel-ICE.