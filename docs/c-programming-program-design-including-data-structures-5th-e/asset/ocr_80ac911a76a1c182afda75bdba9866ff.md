# Binary (Base 2) Representation  
of a Nonnegative Integer

# Converting a Base 10 Number to a Binary Number (Base 2)

Chapter 1 remarked that A is the 66th character in the ASCII character set, but its position is 65 because the position of the first character is 0. Furthermore, the binary number 1000001 is the binary representation of 65. The number system that we use daily is called the **decimal number system** or **base 10 system**. The number system that the computer uses is called the **binary number system** or **base 2 system**. In this section, we describe how to find the binary representation of a nonnegative integer and vice versa.

Consider 65. Note that:

$$65 = 1 \times 2^6 + 0 \times 2^5 + 0 \times 2^4 + 0 \times 2^3 + 0 \times 2^2 + 0 \times 2^1 + 1 \times 2^0$$

Similarly:

$$711 = 1 \times 2^9 + 0 \times 2^8 + 1 \times 2^7 + 1 \times 2^6 + 0 \times 2^5 + 0 \times 2^4 + 0 \times 2^3 + 1 \times 2^2 + 1 \times 2^1 + 1 \times 2^0$$

In general, if $m$ is a nonnegative integer, then $m$ can be written as:

$$m = a_k \times 2^k + a_{k-1} \times 2^{k-1} + a_{k-2} \times 2^{k-2} + \cdots + a_1 \times 2^1 + a_0 \times 2^0,$$

for some nonnegative integer $k$, and where $a_i = 0$ or $1$, for each $i = 0, 1, 2, \ldots, k$. The binary number $a_k a_{k-1} \cdots a_1 a_0$ is called the **binary** or **base 2 representation** of $m$. In this case, we usually write:

$$m_{10} = (a_k a_{k-1} \cdots a_1 a_0)_2$$

and say that $m$ to the base 10 is $a_k a_{k-1} \cdots a_1 a_0$ to the base 2.

For example, for the integer 65, $k = 6$, $a_6 = 1$, $a_5 = 0$, $a_4 = 0$, $a_3 = 0$, $a_2 = 0$, $a_1 = 0$, $a_0 = 1$. Thus, $a_6a_5a_4a_3a_2a_1a_0 = 1000001$, so the binary representation of 65 is 1000001, that is:

$$65_{10} = (1000001)_2.$$

If no confusion arises, then we write $(1000001)_2$ as $1000001_2$.