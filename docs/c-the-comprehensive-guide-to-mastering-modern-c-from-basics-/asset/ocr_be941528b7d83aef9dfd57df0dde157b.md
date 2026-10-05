| Name | suf | bits | d2/d10 | max e2 | max() | eps() | Time |
| --- | --- | --- | --- | --- | --- | --- | --- |
| long double | l | 128 | 64/18 | 16384 | 1.19e+4932 | 1.084e-19 | 81ms |
| float128_t | f128 | 128 | 113/33 | 16384 | 1.19e+4932 | 1.926e-34 | 514ms |

**Table 4.10** The floating-point types added in C++23 in comparison to the classic ones (in bold) on a 64-bit Linux system.

Let's go into even more detail. I will use an example to explain the exact conversion of a floating-point number into the machine representation of the **float**. When I use the term *floating-point number*, I mean the mathematically abstract notion of a number, but now specifically in the decimal system we are used to. float, I mean the IEEE 754 standardized binary representation of a floating-point number in single precision.

As an example, I take the number 45.45 and convert it into a 32-bit `float` representation with one sign bit, eight bits for the exponent, and 23 bits for the signifier.

The sign is quickly converted. The + for a positive number is saved as a bit. A negative number would result in a 1 bit. There's not much there yet, but in the machine it now looks as shown in Figure 4.5.

| | Exp. [8 Bits] | Significand (S) [23 Bits] |
| --- | --- | --- |
| 0 | | |

**Figure 4.5** The beginning of the conversion of a floating-point number.

The next step is to convert the decimal notation into binary notation. Here we take care of the parts before and after, the comma separately.

You can take the part before the decimal point—in this, 45—as an integer. You divide this number by 2 and write down the remainder (0 or 1) until there is nothing left, as described in Section 4.3 (see also Listing 4.25).

For $10^{45}$, you then get binary $_2010101.