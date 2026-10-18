# 7

# Computer Arithmetic

We know that computers store information in bits: that is, in a binary format, 1 or 0. In this chapter, we discuss how this affects computations.

# 7.1  Integer Value Representation

In Section 2.1, we showed the architecture of a simplified microprocessor system that serves as our computational programming interface. In Section 3.1, we discussed various C++ arithmetic types, which we have used in computations presented in this book. In this section, we present some basic information and discuss integer computer arithmetic. For clarity, let’s start with the following definitions:

+   - The basic unit of information is a *bit*, which conveys a value of either 0 or 1. This gives rise to the binary system with base \(B = 2\).
+   - A *byte* is an ordered series of eight bits.
+   - A different *weight* value is associated with each bit position in a byte. For example, the fifth bit, counting from the rightmost 0th position, can be assigned a weight of \(2^4 = 16\). There can be different weight assignments, resulting in different arithmetic values.
+   - A byte is the lowest addressable memory unit in a computer system.
+   - A computer *word* is a concatenation of one or an even number of bytes. A word usually corresponds to the bus width of a microprocessor system. For example, in 32-bit systems, words are four bytes long, whereas in 64-bit systems, they are eight bytes long, and so on.

Figure 7.1 shows the structure of a byte, including the bit positions, indices \(i\), and weights \(w_i\). Similar to the value 125, which in a decimal system is interpreted as \(1 \cdot 10^2 + 2 \cdot 10^1 + 5 \cdot 10^0\), the value \(D\) of a byte shown in Figure 7.1 can be computed as follows

$$D = b_7 \cdot 2^7 + b_6 \cdot 2^6 + \ldots + b_0 \cdot 2^0$$  \hfill (7.1)

where \(b_i\) are bit values of 1 or 0 in the byte. Given this interpretation, \(D\) is always positive and in the range [0...255]. For example, the value of the following byte

| 0 | 1 | 0 | 1 | 0 | 1 | 1 | 1 |
|---|---|---|---|---|---|---|---|