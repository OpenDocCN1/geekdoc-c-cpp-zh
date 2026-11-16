
the constant data were to be placed at the top of the code with no RJMP instruction before it, then this data would be loaded to Flash program memory from address 0. When the AVR microcontroller starts running, it would try to execute this data as instructions, which will result in undefined behavior.

| test_asm : main.asm | DB Example Code |
| :--- | :--- |
| .CSEG | |
| .ORG 0 | |
| .rjmp main | |
| | |
| .CSEG | |
| message: .DB "Hello", 0 | |
| message2: .DB "Hi", 0, 0 | |
| numbers: .DB 3, 2, 1, 0 | |
| letters: .DB 'A', 'B', 'C', 0 | |
| | |
| .CSEG | |
| main: | |
| ldi ZH, high(message << 1) | ; Initialize Z pointer (R31) |
| ldi ZL, low(message << 1) | ; Initialize Z pointer (R30) |
| | |
| check_0: | |
| lpm r16, Z+ | ; Load byte from program memory |
| subi r16, 0 | ; Force status register update |
| brbc SREG_Z, check_0 | ; Loop if result not zero |
| | |
| loop: | |
| rjmp loop | ; Infinite loop |

## Usage of the DB Assembler Directive

Four lines of DB constant byte data follow the first RJMP instruction in the code. DB data has the same format used with BYTE. A label with colon precedes the DB directive, giving the data that follows a human readable name. This name resolves to the address of the 16-bit program memory location that each line of data starts at in Flash program memory.

## Data Formats and Null Terminating Strings

The four lines of data show that data can be in the form of a string between double quotes, numbers separated by commas, and letters between single quotes, also separated by commas. Each line of data defined by DB has been null terminated with the number zero in this code example to follow the C language convention of null terminating strings in order to be able to identify the end of a string. To add a zero to the end of a string, list of numbers or letters, the number zero is simply placed at the end of the line, after a comma.

## Location of DB Data in Program Memory and Alignment

Remember that program memory is 16 bits wide, and that each 16-bit wide memory location has an address that is one bigger than the previous address. This means that we are moving up two bytes at a time when counting through sequential program memory locations. When byte wide data is placed in this program memory, two bytes of data are placed at one single address location, because each address location addresses a 16-bit, or two byte wide memory location. If an odd number of bytes is placed in program memory using the DB directive, then the assembler program will pad the odd number of bytes with a zero byte to make the data an even number of bytes and therefore use up both bytes of the last 16-bit memory location that the data is placed in. This ensures that the next data or program instruction starts at the next 16-bit instruction address. When DB is used to define an odd number of bytes in a Microchip Studio assembly language project, and the project is built, a warning message is displayed in the bottom pane. This warning message is to notify the programmer that the bytes are misaligned because they do not fill up all bytes of the two byte wide program memory locations. The following warning message is seen.

```
.cseg .db misalignment - padding zero byte
```

Try removing the 0 off the end of any of the DB data lines in the code from the previous listing and then build the project in Microchip Studio to see the above message. Be sure to also remove the comma before the zero, so that the line does not end with a comma, otherwise a syntax error will be reported instead. A second zero was added to the end of message2, the “HI” message in order to suppress the warning message. This is a legitimate way to suppress the warning message.

## 16-bit Address Pointer Registers

When we looked at the AVR registers in section 5.1 of Chapter 5, including the diagram in Figure 5.1 of that chapter, we did not look at details of the X, Y and Z registers, except to see them marked in the figure. The code that we are using to show how the DB assembler directive works uses the Z register, so we will look at the details of this register now. Although register R30 and R31 can be used as separate 8-bit wide registers, some instructions use them as a single Z register, such as the LPM instruction in our current example. This Z register is effectively two bytes, or 16 bits wide, made up of R30 being the LSB of the Z register, and R31 being the MSB.

## Loading the Z Register

In the example code that we are using from the previous listing, we have the following,

```
main:
    ldi    ZH, high(message << 1) ; Initialize Z pointer (R31)
    ldi    ZL, low(message << 1)  ; Initialize Z pointer (R30)
```

At the start of the code, we have the `main:` label, which is just an entry point to the main program code. The first RJMP instruction in the program jumps to this label in order to jump over the constant data that was placed in program memory using DB. The name `main` was chosen in this example to mimic the main() function or entry point in a C program – the point where the main program code starts running. It is just a name, and we could have called it anything else that we desired, such as `start` or `begin`. After this label, data is loaded into the high byte and low byte of the Z register. Note that the code uses ZH (Z register high byte) and ZL (Z register low byte) as the destination registers when using LDI, the Load Immediate instruction. ZH refers to register R31 and ZL refers to register R30, which are the two 8-bit registers making up the 16-bit Z register. The data loaded to the two bytes of the Z register is actually the address of the data at the `message:` label. Because the `message` label resolves to the address of a 16-bit word in program memory, we need to multiply it by two to get a byte address instead of a 16-bit word address. This is done by using the left shift operator `<<`, followed by 1, which left shifts the bits making up the address by 1 bit position – each bit moves one position left, and the LSD is filled with 0. This left shift is effectively a multiplication by two. Because we are working on two 8-bit registers, on an 8-bit AVR, this is done in two steps, first for the high byte of the address, using the high() function to get the high byte after the shift. Second, the same shift is done on the same left shifted address, but the low byte is retrieved using the low() function. At the end of these two lines of code we have the address of the start of the message data loaded into the Z register, but converted into a byte address.

## Reading Bytes from Program Memory

The remainder of the code from our example is as follows.

```
check_0:
    lpm    r16, Z+    ; Load byte from program memory
    subi   r16, 0     ; Force status register update
    brbc   SREG_Z, check_0 ; Loop if result not zero

loop:
    rjmp   loop       ; Infinite loop
```

The LPM (Load Program Memory) instruction is used to get a byte from the program memory address that the Z register currently contains. The Z register is effectively pointing to this address location, and can be referred to as a pointer register. There are two options when using the Z register with LPM. One is to simply do the following.

```
lpm r16, Z
```

This fetches the byte that the Z register is pointing to in program memory and puts the byte into R16. The other option is the following, as used in our example program.

```
lpm r16, Z+
```

When Z is followed by +, this means, “get the byte that Z is pointing to and then increment Z by 1”, which means that after the instruction has executed, Z will point to the next byte, following the byte just read. Using LPM in this way lets us access each DB byte in order, starting from the first byte, without the need for a separate increment instruction to increment the Z register. SUBI (Subtract Immediate) is used to subtract 0 from R16 after the LPM instruction. This is done to force the status register and the zero flag in the status register to update. We are looking for the null terminator at the end of the string of data, in order to determine when we have reached the end of the data defined by DB. When this null terminator, or value of zero, does get loaded into R16, the status register does not change. Even though R16 contains zero, the Z flag in the status register does not change because this flag only changes after an arithmetic or logic operation. By subtracting 0 from R16, an arithmetic operation is performed, causing the status register to update. Subtracting 0 from R16 updates the status register, but does not alter the data in R16. After SUBI has executed, the Z flag from the status register is checked using the BRBC instruction to see whether we have reached the end of the constant data string. BRBC (Branch if Bit in SREG is Cleared) is used to jump back to the LPM instruction and get the next constant data byte from program memory if the zero flag of the status register is not clear, when R16 does not contain 0. When R16 does contain zero, BRBC will not branch, but execute the code below it, which is an infinite loop.

## Running the Example Code

If you have not done so already, enter the DB example code from the previous listing into the main.asm file from the test_asm project, as we have been doing to test various code
