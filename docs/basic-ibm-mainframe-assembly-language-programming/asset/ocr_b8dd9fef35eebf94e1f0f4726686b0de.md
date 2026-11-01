assembler will gather all the pieces of each together into separate sections of you object module.

Figure 60 gives an example. Initially, we begin coding CSECT FIRST. This is interrupted by some code for CSECT SECOND which is interrupted by code for DSECT TMPLT1. We resume coding CSECT FIRST. This continues coding from where we left off. Likewise we next resume coding CSECT SECOND which will continue SECOND. The assembler will organize these into continuous blocks.

# 18.2 Base Register Addressing

As we have seen, in the original architecture, memory resident operands in RX, SI, SS, and RS instructions are addressed by a combination of base register, index register and displacement in RX format, or displacement and base (in all others). To this list more recent versions of the architecture have added formats: RSL, RSY, RXE, RXF, RXY, S, SIY and SSE. In the original architecture and in most of the more recent instructions, base/displacement addressing of operands is the norm. However, formats RI, RIE, RIL and RSI have signed immediate operands that in some instructions are added to the current instruction address to form a memory address.

In formats RX, SI, SS, RS, RSL, RXE, RXF, S and SSE, the displacement is a 12 bit unsigned positive number. In RSY, RXY and SLY, the displacement is a 20 bit signed number in 2s complement.

When addressing a memory operand with base and displacement, the base register (any register between R1 and R15 but usually in the range R2 to R13) contains the address of a location in memory. The operand address is calculated by summing the displacement and the contents of the base and, optionally, the contents of an index register.

Displacements in the basic architecture are positive 12 bit numbers and thus can range from 0 to 4095. In some recent instructions the displacements are 20 bit signed numbers that can range from +524,288 to -524,289. In the case of 20 bit displacements, a single base register is often adequate for an entire program. However, many legacy programs use the 12 bit displacement model and this usually means that a program must use more than one base register.

Ordinarily, at the beginning of an assembly language program the assembler is told which register will be the base register and then it is loaded with an address at or near the beginning of the program. From this point on, the assembler will calculate the