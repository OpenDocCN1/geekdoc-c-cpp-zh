# 1.9.3.6 Arithmetic and Logic

Arithmetic and logical operations are essential elements in affecting what the processor is to do. Such operations are executed by any of several hardware components comprising the ALU. Figure 1.43 presents a block diagram for a possible functional ALU architecture.

![](bbox=[0.28, 0.2, 0.78, 0.5])

Figure 1.43 An ALU Block Diagram

Data are brought into the ALU and held in local registers. The op-code is decoded, the appropriate operation is performed on the selected operand(s), and the result is placed in another local register.

# 1.9.3.1 ARITHMETIC

Typically, the processor will support the four basic arithmetic functions: add, subtract, multiply, and divide. Simpler processors will only implement the first two, relegating the last two to a software implementation by the designer. The add and subtraction operations may be supported in two versions, with and without carry and borrow.

The last two versions are intended to support double-precision operations. Such an operation is performed in two steps: the first computation holds any carry (borrow) and then utilizes that value as a carry (borrow in) to the second step. Most such operations are implemented to support integer-only computations. If floating point mathematics is supported, a separate floating point hardware unit may be included. In addition to the four basic functions, the processor may also implement hardware increment and decrement operations.