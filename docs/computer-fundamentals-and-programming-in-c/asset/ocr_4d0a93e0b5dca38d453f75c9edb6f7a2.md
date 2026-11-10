the computer’s natural format. The number of bytes used to represent a floating-point number depends on the precision of the variable. float is used to declare single-precision variables, whereas the type double denotes double-precision values. The representation of the mantissa and exponent in these variables is in accordance with the IEEE floating-point standards. This representation is followed by most of the C compilers. The IEEE format expresses a floating-point number in a binary form known as a normalized form. Normalization involves adjusting the exponent so that the binary point (the binary analog of the decimal point) in the mantissa always lies to the right of the most significant non-zero digit. In binary representation, this means that the most significant digit of the mantissa is always 1. This property of the normalized representation is exploited by the IEEE format when storing the mantissa. Consider an example of generating the normalized form of a floating-point number. For instance, the binary equivalent to represent the decimal number 5.375 can be obtained as shown in the following example.

# **EXAMPLE**

| Integer part conversion to binary | Fraction part conversion to binary |
|---|---|
| 2 ) 5 | 0.375 × 2 = 0.750 &nbsp; 0 |
| 2 ) 2 &nbsp; 1 | 0.750 × 2 = 1.500 &nbsp; 1 |
| 2 ) 1 &nbsp; 0 | 0.500 × 2 = 1.000 &nbsp; 1 |
| 0 &nbsp; 1 | Whole numbers |
| Quotient &nbsp; Remainder | Writing the whole numbers part in the same order in which they are obtained, the fraction part in binary is 011 |
| Writing the remainders in reverse order, the integer part in binary is 101 | |

Thus, the binary equivalent of 5.375 would be 101.011. The normalized form of this binary number is obtained by adjusting the exponent until the decimal point is to the right of the most significant 1. In this case, the result is 1.01011 × 2². The IEEE format for floating-point storage uses a sign bit, a mantissa, and an exponent for representing the power of 2. The sign bit denotes the sign of the number: 0 represents a positive value and 1 denotes a negative value. The mantissa is represented in binary. Converting the floating point number to its normalized form results in a mantissa whose most significant digit is always 1. The IEEE format takes advantage of this by not storing this bit at all. The exponent is an integer stored in unsigned binary format after adding a positive integer bias. This ensures that the stored exponent is always positive. The value of the bias is 127 for floats and 1023 for doubles. Thus, 1.01011 × 2² is represented as follows:

![](bbox=[0.55, 0.06, 0.96, 0.14])

Consider another example. Suppose the number −0.25 has to be represented in IEEE format. On conversion to binary, this number would become −0.01 and in its normalized form it would be −1.0 × 2⁻². This normalized form when represented in IEEE format would look like

![](bbox=[0.55, 0.24, 0.96, 0.3])

Now it is known that converting the floating point number to its normalized form results in a mantissa whose most significant digit is always 1. The IEEE format takes advantage of this by not storing this bit at all. The exponent is an integer stored in an unsigned binary format after adding a positive integer bias. This ensures that the stored exponent is always positive. The value of the bias is 127 for floats and 1023 for doubles. Figure 8.15 shows how any float and double are generally represented in the IEEE format.

![](bbox=[0.55, 0.46, 0.98, 0.7])

According to most C literature, the valid range for floats is 10^−38 to 10^38. But, how is such an odd range used? Well, the answer lies in the IEEE representation. Since the exponent of a float in IEEE format is stored with a positive bias of 127, the smallest positive value that can be stored in a float variable is 2^−127, which is approximately 1.175 × 10^−38. The largest positive value is 2^128, which is about 3.4 × 10^38. Similarly for a double variable, the smallest possible value is 2^−1023, which is approximately 2.23 × 10^−308. The largest positive value that can be held in a double variable is 2^1024, which is approximately 1.8 × 10^308.

There is one more quirk. After obtaining the IEEE format for a float, when the time comes to actually store it