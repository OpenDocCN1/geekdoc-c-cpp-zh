A signed binary number, on the other hand, can be converted from lower to higher length using sign extension. For example, an 8-bit signed number FF (hex) can be converted to a 16-bit signed number FFFF (hex) by extending the sign bit ('1' in this case) to the upper byte of FFFF (hex). Both FF (hex) and FFFF (hex) have the same decimal value of -1. Sign extension is useful for performing arithmetic operations between two signed binary numbers of different lengths.

Sign extension is useful when one wants to perform an arithmetic operation on two signed numbers of different lengths. For example, the 16-bit signed number 0020 (hex) can be added with the 8-bit signed number E1 (hex) by sign-extending E1 as follows:

![](bbox=[0.1, 0.19, 0.85, 0.29])

An error (indicated by overflow in a microcontroller) may occur while performing two's complement arithmetic. The microcontroller automatically sets an overflow bit to 1 if the result of an arithmetic operation is too big for the microcontroller's maximum word size; otherwise, it is cleared to 0. For signed arithmetic operations such as addition, the overflow V = Cf ⊕ Cp where Cf is the final carry and Cp is the previous carry. This can be illustrated by the following examples.

Consider the following examples for two 8-bit signed numbers. Let Cf be the final carry (carry out of the most significant bit or sign bit) and Cp be the previous carry (carry out of bit 6 or seventh bit). We will show by means of numerical examples that as long as Cf and Cp are the same, the result is always correct. If, however, Cf and Cp are different, the result is incorrect and sets the overflow bit to 1. Now, consider the following cases.

Case 1: Cf and Cp are the same.

![](bbox=[0.28, 0.6, 0.8, 0.74])

![](bbox=[0.28, 0.75, 0.8, 0.9])