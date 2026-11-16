Overflow occurs silently during addition and subtraction of integer data types; there is no run-time checking provided by the compiler. It is entirely the programmer's responsibility to anticipate the range of values possible for each variable and to allocate a data type of the appropriate size to avoid overflow.

# 2.4 BINARY REPRESENTATION OF REAL NUMBERS

Real numbers are those that contain a fractional part. Although floating-point is the usual representation used for real numbers, a fixed-point representation is also possible and has certain advantages that are especially important for low-cost embedded applications.

# 2.4.1 Floating-Point Real Numbers

Floating-point numbers are like scientific notation, that is, they consist of two pieces of information: significant digits and a scale factor. The significant digits (or significand) are stored as a fractional value with an implied binary point at the far left; the scale factor is a power of 2, with only the exponent stored in the representation.

Today, all desktop microprocessors include hardware to implement floating-point arithmetic, including any necessary prealignment of binary points or postnormalization of results.

Floating-point representations use a sign-plus-magnitude format and add a bias to the exponent before encoding it. The sign-plus-magnitude format is more convenient for the algorithms required by floating-point arithmetic, and the biased exponent simplifies the hardware that compares exponents for prealignment of operands.

The ANSI/IEEE standard does not impose any particular bit layout for floating-point numbers. However, the typical implementation uses the layout shown in Figure 2-8, in which the sign bit is placed in the most significant bit position of the representation, followed by the exponent and significand fields, respectively. This traditional arrangement is consistent with keeping all the information about the real number in decreasing order of significance.

An interesting characteristic of the ANSI/IEEE format is that one bit of the significand is not stored in the representation! Remember that to maintain maximum precision, we always normalize every result. This forces the most significant bit of every nonzero significant to always be 1. This bit is the integer bit of the significand, and thus

![](bbox=[0.22, 0.69, 0.85, 0.9])

FIGURE 2-8 ANSI/IEEE floating-point representations.