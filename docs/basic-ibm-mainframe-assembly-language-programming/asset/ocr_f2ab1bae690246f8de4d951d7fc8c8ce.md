# 6.8.7 RSY Format

The RSY format, shown in Figure 23, is similar to the RS format but has additional opcode information and an extended 20 bit displacement. While 12 bit displacements are treated as unsigned, positive numbers, 20 bit displacements are treated as 20 bit signed numbers. A 12 bit displacement can range in value from 0 to 4095 while a 20 bit displacement can range from -524,288 to +524,287.

# 6.8.8 RXE Format

The RXE format, shown in Figure 24, is used mainly with floating point operations.

![](bbox=[0.1, 0.27, 0.9, 0.45])

Figure 23 RSY Format

# 6.8.9 RXF Format

The RXF format, shown in Figure 25, is used mainly with floating point operations.

![](bbox=[0.1, 0.62, 0.9, 0.72])

Figure 24 RXE Format

# 6.8.10 RXY Format

RXY instructions, shown in Figure 26, are similar to RX instructions except they have a 20 bit signed displacements and a 16 bit opcode. One or both of the operands are 64 bit values.

![](bbox=[0.1, 0.89, 0.9, 0.95])

Figure 25 RXF Format