In decimal, rounding means adding 1 to the result when the next digit is 5 or greater; for example, rounding the decimal fraction 0.12345 to three digits yields 0.123, while rounding it to four yields 0.1235. In binary, rounding means adding 1 to the result when the next digit is 1; for example, rounding the binary fraction 0.11101 to three digits yields 0.111, while rounding it to four digits 0.1111.

In effect, rounding requires that we increment the result when what we discard is at least halfway to the next result. Rounding decimal and binary values only requires that we look at the next digit, but that is only because 10 and 2 are even numbers. When the number base is odd, “halfway” cannot always be determined by a single digit. Consider base 3 fractional number 0.221XX... X, where “XX...X” is an arbitrary sequence of base 3 digits. If we want to round to three digits, the result will certainly be 0.221 when the left-most X is 0, and 0.222 when the left-most X is 2, but what if it is a 1? Then you have to look at the next X, and so on. Sigh...

# 2.2.3 Hexadecimal: A Shorthand for Binary

When we work with binary numbers by hand, the greater number of digits required increases the likelihood of a transcription error. The *hexadecimal* (base 16) number system solves this problem by essentially serving as a shorthand notation for binary numbers.

When two number bases have a power relationship, as in R₁ = (R₂)ᵏ, converting a number from one number base representation to the other becomes trivial. Specifically, each digit in the base R₁ representation will be in one-to-one correspondence with k digits of the corresponding base R₂ representation. This is exactly why hexadecimal (base 16) is used as a shorthand for binary. Since 16 = 2⁴, each hexadecimal digit will correspond to *four* binary digits.

Hex numbers use digit symbols with values between 0 and 15. The first 10 symbols are the same as in the decimal system (“0” through “9”); the remaining six symbols are taken from the first six letters of the alphabet (“A” through “F”).

First, we have to memorize the 4-bit binary representations of the numbers 0 through 15 shown in Table 2-1. Once we have mastered that, conversion between binary and hex happens almost by inspection. To convert from hex to binary, simply replace every hex symbol by its corresponding 4-bit binary pattern. To convert from binary to hex, start at the binary point and identify groups of four bits each, filling in partial groups with 0’s on the outside, and then replace each group by the corresponding hex digit (Figure 2-3).

We just saw that converting between binary and hexadecimal requires a simple table lookup. But, what if you do not have a copy of the table? Fortunately, recreating the table from scratch is also trivial once you recognize the binary counting pattern.

The principle behind counting is the same in all positional number systems. First, remember what you do in decimal: Add 1 to the least significant digit. If the result is