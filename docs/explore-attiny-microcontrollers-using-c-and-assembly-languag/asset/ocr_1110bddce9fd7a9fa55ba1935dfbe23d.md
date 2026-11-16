where A is the address of the I/O register, and b is the bit to test. SBIC and SBIS were both used in section 8.2.5 of Chapter 8 to test the state of a switch connected to a pin. To test the bit in an I/O register that has an address greater than 31, it is necessary to first read the value into the I/O register into a general purpose register, and then use SBRC or SBRS to test the bit in the general purpose register.

# 11.2.2.6 Branch Instructions

Branch instructions branch depending on if a bit is set or clear in the status register or SREG. BRBS and BRBC that immediately follow check for a specified bit in the status register. All other branch instructions are synonyms for BRBS and BRBC that check specific status register bits. BRBS and BRBC take two operands – the bit number in the status register to check and the address to branch to. All other branch instructions take only one operand – the address to branch to, because the bit to check in the status register is fixed with these instructions. All of the branch instructions are limited to branching to a relative address that can be between -64 and +63 relative to the PC.

After BRBS and BRBC, there are 9 pairs of branch instructions that test the 8 flags in the status register to see whether they are set or clear. The reason that there are 9 pairs of instructions instead of 8 is because two of the pairs check the status of the C flag.

# Branch if Bit in SREG Set or Cleared

+   BRBS (Branch if Bit in SREG is Set)
+   BRBC (Branch if Bit in SREG is Cleared)

Of the two instructions BRBS and BRBC, BRBC was used to check the status of the Z flag in the status register for the basic delay subroutine, starting in the code of section 2.3.2 of Chapter 2. BRBC was used to check if the Z bit was cleared, in other words if the contents of a register was not zero. BRBC branched to a DEC instruction that decremented the register. So long as the register did not contain zero, BRBC branched to DEC. When DEC finally decrements the register to zero, then the Z flag is automatically set to indicate that the last arithmetic operation resulted in zero. BRBC then does not branch, but rather runs the instruction directly below it. This part of the delay subroutine code is as follows.

```
...
delloop2:
    dec r17
    brbc SREG_Z, delloop2
...
```