# **TABLE 6.8**  PIC18F Rotate Instructions

Instruction

Operation

RLCF F, d, a

![](bbox=[0.51, 0.13, 0.74, 0.18])

Rotate register F one bit to the left through carry. See notes for ‘d’ and ‘a’.

RLNCF F, d, a

![](bbox=[0.53, 0.23, 0.72, 0.29])

Rotate register F one bit to the left without carry. See notes for ‘d’ and ‘a’.

RRCF F, d, a

![](bbox=[0.51, 0.33, 0.74, 0.38])

Rotate register F one bit to the left through carry. See notes for ‘d’ and ‘a’.

RRNCF F, d, a

![](bbox=[0.53, 0.4, 0.72, 0.46])

Rotate register F one bit to the left without carry. See notes for ‘d’ and ‘a’.

+   - All instructions in the above are executed in one cycle.
- The size of each instruction is one word.
- a = 0 means that the data register is located in the access bank while a = 1 means that the contents of BSR specify the address of the bank.
- For destination: d = 0 means that the destination is WREG while d = 1 means that the destination is file register, F.
- RLCF and RRCF affect N, Z, and C flags according to the result while RLNCF and RRNCF affect N and Z flags based on the result.
- Note that the PIC18F does not have any shift instructions