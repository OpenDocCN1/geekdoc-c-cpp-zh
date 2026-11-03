The types can be classified as *fundamental* (integer and floating) versus *derived* (pointer, array, structure, union, function), or as *scalar* (fundamental plus pointer) versus *composite* (array, structure, union, function).

A summary of the types will be given in [0.7].

# 0.1 Integers

*Integers* are the workhorses of a C program. They are used for counting, for selecting elements of an array, for representing characters of text, logical values, and bit sequences, and for any arithmetic where the magnitude range is known to be limited and fractional results are not needed. It is no surprise that integers are implemented in a wide variety of ways.

The basic integer can be represented as a binary datum, although there is no presumption in the language about whether arithmetic is performed in one’s complement, two’s complement, signed magnitude, or some more exotic encoding. Integers in C always will be at least as big as are addresses on the target machine; they can be used unreservedly as subscripts or pointer modifiers.

Short integers can be used, in the hope of achieving storage economy, for counting things in the thousands. There is no guarantee, however, that a short integer actually will be any shorter than a basic integer. Similarly, long integers are used for counting things in the hundreds of millions; they also may be no longer than basic integers.

Unsigned integers are typically the same size as basic integers and behave much the same in arithmetic, except that their values are always taken as zero or positive. On two’s complement computers, this has the net effect of treating the sign bit as just another magnitude bit. Their primary use is not so much to double the range of counting with positive numbers as to permit arithmetic that is compatible with the treatment of addresses on machines where an address fills up an integer-sized word.