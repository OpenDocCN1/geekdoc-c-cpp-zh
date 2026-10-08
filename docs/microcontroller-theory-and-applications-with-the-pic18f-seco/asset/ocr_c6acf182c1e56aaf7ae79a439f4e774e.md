register), the internal clock source is also enabled. The time delay provided by the WDT varies from 4 ms to 131.072 seconds. If the timer associated with the WDT is enabled and then times out after a specific amount of time during program execution, the PIC18F resets itself automatically and clears the bit in the RCON register. This “time out” may happen in certain situations such as if the program is “caught in an infinite loop” or if the program takes unexpectedly longer execution time. The WDT can be useful for debugging programs.

In this book, for all I/O examples, the WDT will be turned OFF. In C18 directive, “#pragma config” can be used to accomplish this as follows:

```
#pragma config  WDT = OFF        // Turn WDT OFF
```

**RESET Instruction**  This is a software RESET. Upon execution of the RESET instruction, the PIC18F resets all registers and flags that are affected by a power-on Reset, and the  bit in the RCON register is cleared to 0 indicating the reset instruction is not executed.

# 8.1.3 High Voltage and Low Voltage Programming (HVP and LVP)

There are two ways to program the PIC18F microcontroller. They are:

**HVP (High Voltage Programming)** This a is normal programming method. The downloading hardware interface such as the PICKit3 can be used for this purpose. Programming voltage of usually up to 13V is applied at the VPP pin during downloading. The assembled or compiled programs from a computer (Personal Computer or Laptop) can be downloaded into the PIC18F chip by connecting the PICKit3 between them.

**LVP (Low Voltage Programming)**  LVP is basically the same as the HVP except the programming voltage is set to the normal supply voltage of 5V. The real benefit of using the LVP mode is that one can program several PIC18F on a board without having to program each one individually. One could daisy chain each extra PIC18F to a master PIC18F which would then program each one in turn. This is only possible since the Vpp signal is a normal logic level in LVP mode. Hence, this mode is a specialized operation and is not normal for standard use. Also, in the LVP mode, the PGM pin cannot be used for anything else such as RB5 since the PGM and RB5 are multiplexed. Hence, it is a good idea to disable the LVP mode by using the C18 directive “#pragma config” as follows:

```
#pragma config  LVP = OFF        // Turn LVP OFF
```

# 8.1.4  “pragma config” and “config” directives

The C18 directive “#pragma config” is discussed in the previous sections. The equivalent directive in the PIC18F MPLAB assembler is the “config” directive. This directive tells the MPLAB PIC18F assembler that the assembler needs to do something specific to the hardware. Some of these functions include selecting an appropriate oscillator and turning ON or OFF certain features such as WDT (Watch Dog Timer), BOR (Brown Out Reset), and LVP (Low Voltage Programming). Since an internal oscillator will be used in all the I/O examples in this book, the following “config” commands are necessary for PIC18F assembly language I/O programs for the PIC18F chips to function properly. After downloading the assembled code into the PIC18F4321 on the breadboard using the PICKit3, the following configuration commands should be inserted after “#include <P18F4321.INC>” as follows: