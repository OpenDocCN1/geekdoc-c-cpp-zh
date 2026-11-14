The double ** symbols preceding the operands in the indirect access mode indicate that two levels of indirection are necessary to reach the final operand in memory.

The flow and two representative instructions to the assembly and the C and C++ levels are illustrated in Figure 1.22.

# 1.9.2.1.3 REGISTER DIRECT AND REGISTER INDIRECT MODES

The distinction between the register direct and register indirect modes lies in the content of the referenced register. In the former case, the register contains the value of the operand and in the latter case the address (in memory) of the operand. The register indirect mode provides the means to easily implement pointer-type operations that are commonly used in C and C++.

The major disadvantage of indirect addressing is that an additional memory access is necessary to retrieve the operand’s value. In contrast, when utilizing direct addressing, the value of the operand is found in the register.

In Figure 1.23, two different data transfer operations are shown. For the register direct operation, at the C/C++ level, the value of one variable, y, is assigned to a second variable, x. At the assembly language level, we assume that the values for x and y have previously been stored in registers R2 and R3, respectively. The MOVE instruction directs that the contents of R3 is copied to R2.

![](bbox=[0.25, 0.4, 0.9, 0.85])

# Figure 1.23 Register Direct and Register Indirect Data Transfer Operations