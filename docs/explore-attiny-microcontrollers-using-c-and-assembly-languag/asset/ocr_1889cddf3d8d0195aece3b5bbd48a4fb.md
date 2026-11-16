format is 0xFF, as can be seen in the line of code that follows. Again, one line of C code converted to one line of assembly language code. The line of C code is shown above the assembly language code that it converted to.

```
count++; // Increment count
0000001E SUBI R24,0xFF Subtract immediate
```

SUBI, like other register direct addressing mode instructions, uses an immediate value that is encoded as part of the instruction. SUBI only operates on registers R16 to R31. In the led_count.asm project, the INC instruction was used on R18 to increment the count value.

As in the led_count.asm project, ANDI is used to clear the top 3 bits of the count register. This converts from one line of C code again, as shown below.

```
count &= 0b00001111; // Clear unused bits
0000001F ANDI R24,0x1F Logical AND with immediate
```

The last instruction in the program does a relative jump back to address 0x0014 as follows.

```
00000020 RJMP PC-0x000C Relative jump
```

This jump uses a negative value relative to the current value in the PC. 0x0020 is in the PC at the time this instruction is executed, so 0x0020 – 0x000C gives an address of 0x0014. Address 0x0014 is the top of the while(1) loop, where the count value is written to the LEDs via the PORTB register at address 0x18. The reason that we do not use addresses, whether positive or negative, with the RJMP instruction in assembly language programs like led_count.asm, is that we use labels in these programs, letting the assembler program resolve the addresses when it is run at build time.

The above line of code is what makes the while(1) loop from the C program, and is found at the closing brace position of the while(1) loop in the original C code.

As a comparison between led_count.asm and the disassembled code from led_count.c, the following listing shows the two programs side by side, with the delay routines removed. The vector table and C runtime code is also removed from the disassembled code. The original C code is shown at the right, lined up with the assembly language code that it produced on its left.