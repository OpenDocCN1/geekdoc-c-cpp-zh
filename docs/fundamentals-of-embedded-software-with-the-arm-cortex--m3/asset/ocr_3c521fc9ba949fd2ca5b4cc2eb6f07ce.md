# # Implementing Arithmetic

# ## 3.1 2'S-COMPLEMENT AND HARDWARE COMPLEXITY

Computers manipulate bit patterns. *How* those patterns are assigned to the values they represent has a big effect on hardware complexity. For example, both the sign-plus-magnitude and the 2's-complement representation allow us to recognize whether a number is positive or negative simply by looking at the most significant bit. However, wouldn't be great if patterns were assigned to values in such a way that the same hardware could be used to perform integer arithmetic regardless of whether the operands were signed or unsigned? That is exactly what the 2's-complement representation is intended to do!

For example, suppose we were to add the two *unsigned* decimal values 9 and 3. The computer would be given their binary equivalents, 1001 and 0011. The correct decimal result is 12, so the hardware that performs addition is designed to produce the binary equivalent, 1100. But what happens if those same binary patterns are interpreted instead as *signed* numbers according to the 2's-complement scheme shown in Figure 3-1? Then, the operands would be -7 and +3, and the same binary result of 1100 produced by the hardware would correctly be interpreted as -4.

The fundamental characteristic of 2's-complement representation that makes this work is that it follows a count sequence<sup>1</sup> from full-scale negative to full-scale positive (with a rollover to zero), in much the same way that the representation of unsigned numbers follows a count sequence from the smallest magnitude (zero) to the largest. The sign-plus-magnitude representation does not share this characteristic.

In a similar manner, using the 2's-complement representation permits one hardware subtractor for both signed and unsigned integers. However, it also turns out that we do not even need separate hardware for addition and subtraction! All we need to do in order to compute the difference A - B is to *add* the negative of B to A, as in A + (-B). In other words, we simply need to add some hardware to form the 2's complement of B.

All hardware adders accept an initial “carry-in” that can be used to add a constant of 0 or 1 to the sum. Normally, this input is set to 0. However, if we set it to 1 and invert all the bits of B, the net effect will be the same as adding -B instead of B. We can

<sup>1</sup> The sequence of numeric values represented by the sequence of patterns is monotonically increasing, meaning that it increases by one at each step.