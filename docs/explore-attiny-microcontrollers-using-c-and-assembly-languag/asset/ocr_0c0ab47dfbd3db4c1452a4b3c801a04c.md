Although this project does not cover timers or timing, the subject of this chapter, we look at it here while on the subject of calling subroutines from C. As can be seen in the add8bit.S file, R24 and R22 are used as the two char arguments of the add8bit subroutine. The C prototype for the subroutine can be seen in add8bit.h. Because char arguments are allocated in pairs by the GCC C compiler, R25 and R24 represent the first char argument, but only R24 is used. For the second argument, R23 and R22 are allocated, but only R22 is used. R25 and R24 are allocated to hold the return value by the C compiler, but only R24 is used. In main.c the sum variable is declared volatile so that the C compiler does not optimize it away. It is necessary to look at the disassembly of the code to see what is really happening. The following disassembly listing was taken from the project built for an ATtiny45.

```
asm_add.c : disassembly

--- add8bit.S ----
        add   r24, r22        ; arg1: r25 and r24, arg2: r23 and r22
00000018  ADD R24,R22         Add without carry
        ret                   ; return registers are r25 and r24
00000019  RET                 Subroutine return
--- main.c ----
{
0000001A  PUSH R28            Push register on stack
0000001B  PUSH R29            Push register on stack
0000001C  PUSH R1             Push register on stack
0000001D  IN R28,0x3D         In from I/O location
--- main.c ----
0000001E  IN R29,0x3E         In from I/O location
        sum
0000001F  LDI R24,0x5B        ; 91
        sum                   LDI R22,0x5B
00000020  LDI R24,0x22        Load immediate
00000021  RCALL PC-0x0009     Relative call subroutine
00000022  STD Y+1,R24         Store indirect with displacement
}
00000023  LDI R24,0x80        Load immediate
00000024  LDI R25,0x80        Load immediate
00000025  POP R0              Pop register from stack
00000026  POP R29             Pop register from stack
00000027  POP R28             Pop register from stack
00000028  RET                 Subroutine return
--- No source file ----
00000029  CLI                 Global Interrupt Disable
0000002A  RJMP PC-0x8000      Relative jump
```

In the above disassembly, the interrupt vector table and C runtime code is not displayed. Values are passed to the add8bit subroutine at address 0000001F and 00000020. These value are 0x5B or 91 loaded to R22, and 0x22 or 34 loaded to R24. After this, is a call to