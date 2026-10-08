The compiler will insert the address 0xF80 during compilation whenever it encounters PORTA in the program.

The "config" directive in the above tells the MPLAB assembler to perform a specific action before assembly. This directive can be used to turn certain on-chip devices ON or OFF. For example, the statement "config WDT = OFF" placed after the "include" directive will turn the watchdog timer OFF.

**Example 8.1**
Write a PIC18F assembly language program at 0x100 to drive an LED connected to bit 0 of Port D based on a switch input to bit 0 of Port C as shown in Figure 8.16. If the switch is opened, turn the LED OFF; turn the LED ON if the switch is closed.

# *Solution*

From Figure 8.16, since the cathode of the LED is connected to bit 0 of Port C, a ‘0’ output from the PIC18F4321 will turn the LED ON, and a ‘1’ will turn it OFF. The PIC18F sinks (for LOW output) adequate current to turn an LED OFF or ON without any buffer such as 74HC244; only a current limiting resistor R = 330 ohm is required.
The 0PIC18F assembly language program is provided below:

```
INCLUDE       <P18F4321.INC>
ORG           0x100
BSF           TRISC, TRISCO  ; Configure bit 0 of Port C as an input
```

![](bbox=[0.35, 0.4, 0.65, 0.55])

**FIGURE 8.15**
PIC18F4321 interface to a common cathode seven-segment display via PORT C

![](bbox=[0.25, 0.58, 0.75, 0.85])

**FIGURE 8.16**
Figure for Example 8.1