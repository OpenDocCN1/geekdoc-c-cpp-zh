In the code example, values in register R16 and R17 are compared using CP. The BREQ (Branch if Equal) instruction is used after CP to determine if the compared values were equal or not. If the values are equal, then program execution branches to the next NOP instruction at the equal label. If the values are not equal, program execution continues at the first NOP instruction below BREQ. Other conditional branch instructions can be used after CP to determine the outcome of the comparison. Conditional branch instructions are found in section 11.2.2.6 that follows after the next section.

# CPC (Compare with Carry)

CPC is like the CP instruction, but also takes into consideration the carry flag in the status register. As with CP, CPC is usually followed by a conditional branch instruction.

# CPI (Compare with Immediate)

CPI is like the CP instruction, but instead of comparing two registers, it compares one register with an immediate value. It has the form CPI Rd,K where K is an 8-bit immediate value.

# 11.2.2.5 Skip Instructions

# SBRC (Skip if Bit in Register is Cleared)

SBRC tests a bit (0 to 7) in a register (R0 to R31) to see if it is clear. If the bit is clear, it skips the next instruction. It has the form SBRC Rr,b where Rr is the register to test, and b is the bit in the register to test. SBRC was used in section 8.2.3 of Chapter 8 to limit a count value. Any I/O register read into a general purpose register can have its bits tested using SBRC.

# SBRS (Skip if Bit in Register is Set)

SBRS works the same way as SBRC, but tests if a bit is set in a register rather than cleared. If the bit is set, the next instruction is skipped. SBRS was used in the timer polling code from section 10.4.2 of Chapter 10 to test the OCF0A bit in the TIFR register. The TIFR register was first read into a general purpose register before testing the OCF0A bit.

# SBIC (Skip if Bit in I/O Register is Cleared)

# SBIS (Skip if Bit in I/O Register is Set)

SBIC and SBIS work in the same way as SBRC and SBIS, but operate on I/O registers 0 to 31, rather than the general purpose registers. Both instructions have the form SBIC A,b