The previous line of C code is converted by the C compiler to the following line of assembly language:

```
sbi DDRB, DDB4
```

This particular example happens to convert from one line of C code to one line of assembly language code. In other cases a line of C code may convert to more than one line of assembly code. In this section, we look at the assembly language code that the C compiler and linker generated from the led_count.c project, and that actually gets loaded to the Flash memory of the AVR. Although binary machine code is ultimately loaded to Flash memory, we look at the assembly language code after the disassembly of these machine code instructions. This is done in the debugger in Microchip Studio. Start the debugger using Start Debugging and Break with either the actual hardware and hardware programmer/debugger, or using the simulator. After the debugger starts, select Debug ▶ Windows ▶ Disassembly from the top menu, or use the keyboard shortcut Alt + 8 — there is also a Disassembly icon on the second from top toolbar. After opening the disassembly window, the disassembled code comes into view in Microchip Studio. The first part of this disassembled code is shown in the listing below for an ATtiny13(A).

```
--- No source file ---
00000000 RJMP PC+0x0008A Relative jump
00000001 RJMP PC+0x0008F Relative jump
00000002 RJMP PC+0x0008E Relative jump
00000003 RJMP PC+0x0008D Relative jump
00000004 RJMP PC+0x0008C Relative jump
00000005 RJMP PC+0x0008B Relative jump
00000006 RJMP PC+0x0008A Relative jump
00000007 RJMP PC+0x00089 Relative jump
00000008 RJMP PC+0x00088 Relative jump
00000009 RJMP PC+0x00087 Relative jump
0000000A RJMP PC+0x00086 Relative jump
--- /.../ : </crt1/gcrt1.S
0000000A CLR R1 Clear Register
0000000B OUT 0x3F,R1 Out to I/O location
0000000C LDI R28,0x9F Load immediate
0000000D OUT 0x3D,R28 Out to I/O location
0000000E RCALL PC+0x00083 Relative call subroutine
0000000F RJMP PC+0x00012 Relative jump
00000010 RJMP PC-0x0010 Relative jump
```

The disassembly window displays disassembled code from Flash memory. At the top is the interrupt vector table that was inserted automatically by the C tools. We don't look at interrupts in detail here. For now just know that the first entry in the interrupt vector table is the reset vector. The instruction at this location simply causes a jump to the entry point of the C code. When the AVR is powered up or reset, it runs this instruction first, which