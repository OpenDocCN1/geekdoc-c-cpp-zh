
# 8.2.6 Programmed I/O examples using C Language

g f e d c b a Hex:
| | g | f | e | d | c | b | a | Hex |
|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0x40 |
| 1 | 1 | 1 | 1 | 1 | 0 | 0 | 1 | 0x79 |
| 2 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 0x24 |
| 3 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0x30 |
| 4 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 0x19 |
| 5 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0x12 |
| 6 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0x03 |
| 7 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0x78 |
| 8 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0x00 |
| 9 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0x18 |

Note that for a common-anode seven segment display, a ‘0’ will turn a segment ON and a ‘1’ will turn it OFF. Also, bit 7 of PORTB is assumed to be ‘0’. The above table must be stored in the data memory using MOVLW and MOVWF instructions or using the MPLAB assembler directive DB along with the PIC18F assembly language instruction TBLRD (Table Read) with appropriate addressing mode.

The PIC18F assembly language program is provided in the following:

```assembly
INCLUDE <P18F4321.INC>
ORG 0x70
MOVLW 0x40 ; Store 7-segment codes
MOVWF 0x100
MOVLW 0x79
MOVWF 0x101
MOVLW 0x24
MOVWF 0x102
MOVLW 0x30
MOVWF 0x103
MOVLW 0x19
MOVWF 0x104
MOVLW 0x12
MOVWF 0x105
MOVLW 0x03
MOVWF 0x106
MOVLW 0x78
MOVWF 0x107
MOVLW 0x00
MOVWF 0x108
MOVLW 0x18
MOVWF 0x109
MOVLW 0x0F ; Configure PORTA as input
MOVWF ADCON1
CLRF TRISB ; Configure PORTB as output
LFSR 0, 0x100 ; Initialize FSR0 with the starting
; address of lookup table
LOOP MOVF PORTA, W ; Input switch data to the WREG
ANDLW B'00001111' ; Mask the lower 4-bits
MOVF PLUSW0, PORTB ; Output BCD data to PORTB
BRA LOOP ; Loop
END
```

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_228_0.png)

**FIGURE 8.17** Figure for Example 8.3

Before we go on, a summary of the basic characteristics of typical C-programs will be discussed in the following:

### Preprocessor directives

The C-preprocessor directives are part of the C compiler. The purpose of a preprocessor is to execute a specific command associated with the preprocessor. These preprocessors are not part of the C language. Instead, they are part of the C compiler software. Each preprocessor directive begins with the symbol #.

Before compiling a C-program, the C compiler first initiates execution of the preprocessor software module. This module then goes through the program looking for the “#” sign. If the symbol “#” is found, the preprocessor module performs the function specified by the command. The C compiler may then start compiling the program.

Typical preprocessor directives are “#include”, “#define”, and “#pragma config”. The “#include” preprocessor directive transfers texts (commands, comments, etc.) from another document into the program. For example, consider

```c
#include <p18f4321.h>
```

In the above, the extension .h means header file. Note that the header file includes standard library functions that are used in the C program. The above statement instructs the compiler to include the source code from the file p18f4321.h into the program. The file p18f4321.h is a PIC18F4321-specific header file, and primarily contains definitions for the variables used to access the Special Function Registers (SFRs) of the PIC18F4321. For example, PORTA of the PIC18F4321 is mapped as a Special Function Register (SFR) with data memory address 0xF80. The header file contains this information. This means that the user can use PORTA in the C-program. The compiler will insert the address 0xF80 during compilation whenever it encounters PORTA in the program.

The “#define” preprocessor directive can be used to declare constants. For example, consider

```c
#define y 4
```

The “#define” preprocessor will assign 4 to y. Constants defined with the preprocessor “#define” are textual replacements performed before the program is compiled.

The “#pragma config” preprocessor directive tells the compiler to perform a specific action before compilation. This directive can be used to turn certain on-chip devices ON or OFF. For example, the statement “#pragma config WDT = OFF” placed after the “#include” directive will turn the watchdog timer OFF.

In this section, programmed I/O examples using C language are included. As mentioned before, in order for the I/O programs to work properly, the following “#pragma config” statements should be included in all the programming examples after the “#include <p18f4321.h>” statement:

```c
#pragma config OSC = INTIO2 // Select internal oscillator
#pragma config WDT = OFF // Watch Dog Timer OFF
#pragma config LVP = OFF // Low Voltage Programming OFF
#pragma config BOR = OFF // Brown Out Reset OFF
```

### main ( ) function

All C-programs must include a “main ( )” function which can appear only once. The keyword “void” can optionally be placed within the brackets to clarify that there are no parameters. The statement,

```c
main (void)
```

means no arguments are required for function call. The “void” type does not provide a result value to the caller. Hence, “main ( )” means that it does not return a value. Since “main” is classified as a function, all codes must be placed within curly brackets.

### while (1)

In microcontrollers including the PIC18F, after completion of program execution, there is no operating system to return to. Hence, an infinite “while (1)” loop is used to keep the microcontroller running and prevent it from exiting the “main( )”. This will prevent attempts in executing codes at undefined memory locations. Note that the keyword “while” defines an iteration loop that continues or breaks based on a condition that is inserted inside the parentheses of the while statement. For example, the statements within the curly brackets in the following “while” loop

```c
while ( x < 2)
{
Statements
}
```

are executed as long as the variable ‘x’ is less than 2 and the loop condition is true. Hence, before each iteration, the program determines whether the condition is “TRUE” (represented by non-zero in C) or “FALSE” (represented by zero in C). This means that “while (1)” with ‘1’ inside the loop is always a TRUE condition. Hence, the loop will run forever. Therefore, while(1) is an infinite loop.

### PIC18F data types

Data types for C are discussed in Chapter 4. An overview of common PIC18F data types will be covered in this section. Common data types with the PIC18F are listed below:

- unsigned char (8-bit). Since the PIC18F is an 8-bit microcontroller, this is normally used for positive variables (8-bit positive temperature) by the PIC18F.
- signed char (8-bit): This is called “char” in the PIC18F since signed char is a default data type in the PIC18F. This data type can be used by an 8-bit signed temperature.
- unsigned int (16-bit): Since memory addresses are unsigned (always positive), this data type can be used by the PIC18F4321 for program memory addresses. Note that the program memory address for the PIC18F4321 is 13-bit wide.
- signed int (16-bit): Since memory contents are 16-bit wide in the PIC18F4321, this data type can be used to store 16-bit signed data in program memory.

### Functions in C

As mentioned in Chapter 4, a function in C is similar to subroutine in assembly. Hence, a function is a block of C codes that perform a particular task.

A typical example of a C-function is provided below. The following C-function does not return the result to the main; the reserved word “void” can be used in such a situation. A simple example for the C18 C-compiler for the PIC18F is provided in the following:

```c
#include <p18f4321.h>
// Initializations
void CONVERT (void);
void main (void)
{
Statements
CONVERT (); // Function Call
} // end of main
void CONVERT ()
{ Body of the Function
}
```

### Arrays in C

As mentioned in Chapter 4, an array contains a number of the same type of data elements stored under a common name in consecutive memory locations. The same type of data elements means that data elements can be, for example, character (char) elements or integer (int) elements.

An array of BCD codes for a common-anode seven-segment display can be created using the C18 compiler of the PIC18F as follows:

```c
#include <pic18f4321.h>
void main ()
{
unsigned char code [10] = {0x40, 0x79, 0x24, 0x30, 0x19, 0x12, 0x03, 0x78,
0x00, 0x18};
// ...
}
```

In the above program, the array name is “code” with 10 (total number of elements) inside the square brackets and each element is listed within curly brackets. For example,
