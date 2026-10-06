Disassemblers Decompilers

+   - jump tables,
- calculated jumps, and,
- a parameter after the call instruction.

# 2.6.1 jump tables and other calculated jumps

8-bit CPUs, calculated jumps are often implemented by pushing a calculated 'return' address to the stack, then jumping to that address using the 'return' instruction. For example, the RTS Trick⁵ uses this technique to implement jump tables (w:branch table⁶).

# 2.6.2 parameters after the call instruction

Instead of picking up their parameters off the stack or out of some fixed global address, subroutines provide in the addresses of memory that follow the instruction called that subroutine. Subroutines that use this technique adjust the return address to skip over the constant data, then return to an address many bytes after the 'call' instruction. One of the most famous programs that used this technique is the 'Sweet 16' virtual machine.

The technique may make disassembling more difficult.

# 2.7 Disassembly of 32 bit CPU code

Most 32-bit CPUs use the ARM instruction set⁷⁸⁹.

Typical ARM assembly code is a series of subroutines, with literal constants scattered between subroutines. The standard prolog and epilog¹⁰ for subroutines is pretty easy to recognize.

# 2.8 A list of disassemblers

+   - asgen¹¹ 'contains generic tools and has been used to make assemblers for 8080 8086
80386 Alpha 6809 is used for Pentium 68000 6502 8051.¹¹

| 5 | http://wiki.nesdes.com/w/index.php/RTS_Trick |
| 6 | http://en.wikipedia.org/wiki/branch32table |
| 7 | Jim Turley. "The Two Percent Solution" [http://www.eetimes.com/discussion/other/4024488/The-Two-Percent-Solution.] (2002). |
| 8 | Max Huffman. "ARM Core Club Into 3G Territory" [http://www.extremetech.com/extreme/52186-arm-cores-club-into-3g-territory.] (2002). Although Intel and AMD receive the bulk of attention in the court, ARM's 32-bit architecture, ... has sold out others.
| 9 | Tom Kraitz. "ARMed for the living room [http://www.cnet.com/ARMed-for-the-living-room/2100-1056-3-6056729.html] - ARM licensed 1.6 billion cores [in 2005]. 2006. |
| 10 | http://en.wikibooks.org/wiki/Embedded_Systems/Mixed_C_and_Assembly_Programming%
ZARMY20 |
| 11 | http://home.hccnet.nl/a.w.man.der.horst/asgen.fr |

18