# register indirect yPtr, x

For the register indirect operation, at the C/C++ level, the value of one variable, stored in memory and pointed to by the pointer variable yPtr, is assigned to a second variable, x. At the assembly language level, once again we assume that the values for x and yPtr have been previously stored in registers R2 and R3, respectively. The MOVE instruction now directs that the contents of R3 serve as an address into memory; the value of the variable at that address is to be retrieved and to be copied into R2.

If the values and address modes of the two operands are interchanged, the data transfer would be from R2 into the location in memory pointed to by the contents of R3.

The flow and two representative instructions at the assembly and the C and C++ levels are illustrated in Figure 1.23.

The * preceding the second operand in the indirect instruction indicates that the assembler is to set the indirect addressing mode for the instruction.

# indexed, displacement

# 1.9.2.1.4 INDEXED MODE

The indexed or displacement addressing mode provides support for accessing container-type data structures such as arrays. The effective address is computed as the sum of a base address and the contents of the indexing register. It is important to note here that following the execution of the instruction, neither the base address nor the index values are changed.

The major disadvantage of indexed addressing is the time burden associated with computing the address of the operand and then retrieving the value from memory. Indexing adds a greater burden to system performance than does indirect addressing.

Figure 1.24 illustrates the retrieval of an indexed variable using code fragments written at the assembly and the C or C++ levels.

![](bbox=[0.2, 0.68, 0.91, 0.78])

# Figure 1.24 Indexed Mode Data Transfer Operations

Starting at the C/C++ level, we have an array variable named y and an integer variable x. The variable x is to be assigned the value contained in the fourth element of the array.