# 18 1 Introduction

```
[+0] = 0 0...0
[-0] = 11...1 + 1 = 0 0...
n digits
n digits
Auto discarded
```

The above method of getting complement code is usually called "ones-complement plus 1". We will not prove this method here. Readers only need to get a basic understanding of complement code and not to get bewildered by the data storage form in memory for future studies.

c) Arithmetic rules in complement code operation
Another advantage of using complement code is that it is the simplest representation method when numerical information is taken apart in arithmetic operations. Firstly, the sign can be treated as part of the value in operations and we can still get the correct sign of the result. Secondly, subtractions can be converted into additions, which number lead to simpler arithmetic circuits.

For example, let's see how to calculate 67 - 10 in a computer (here the number's system is indexed by subscripts):

```
+67_10 = 01000011_2 [+67]_10complementcode = [+67]_10true
[-10]_10true = 10011010_2, [-10]_10complementcode = 11110110_2
01000011_2
[+67]_10complementcode
+ 11110110_2
[-10]_10complementcode
1 00111001_2 = 57_10
The carry bit is discarded
```

Since the word is only 8 bits, the carry bit of the most significant bit in addition is automatically discarded, in order to get the effect of mod operation (discarding a modulus).

Note that the result of arithmetic operations on complement code is still complement code. In the example above, we can know from the sign bit that the result is positive, and the complement code is the same as its true code, which is the decimal number 57.

If the result is negative, the result is the complement code of the negative number:

For example: 10 - 67 = ?

```
[+10]_10true = 00001010_2 = [+10]_10complementcode
[-67]_10true = 11000011_2, [-67]_10complementcode = 10111101_2
```