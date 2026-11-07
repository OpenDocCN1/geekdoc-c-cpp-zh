
the character in the row marked 6 (the number in the first column) and the column marked 5 (the number in the second row) is A. Therefore, the character at position 65 (which is the 66th character) is A. Moreover, the character b at position 32 represents the space character.

The first 32 characters, that is, the characters at positions 00–31 and at position 127 are nonprintable characters. The following table shows the abbreviations and meanings of these characters.

| | | | | | |
|---|---|---|---|---|---|
| nul | null character | ff | form feed | can | cancel |
| soh | start of header | cr | carriage return | em | end of medium |
| stx | start of text | so | shift out | sub | substitute |
| etx | end of text | si | shift in | esc | escape |
| eot | end of transmission | dle | data link escape | fs | file separator |
| enq | enquiry | dc1 | device control 1 | gs | group separator |
| ack | acknowledge | dc2 | device control 2 | rs | record separator |
| bel | bell | dc3 | device control 3 | us | unit separator |
| bs | back space | dc4 | device control 4 | b | space |
| ht | horizontal tab | nak | negative acknowledge | del | delete |
| lf | line feed | syn | synchronous idle |  |  |
| vt | vertical tab | etb | end of transmitted block |  |  |

### EBCDIC (Extended Binary Coded Decimal Interchange Code)

The following table shows some of the characters in the EBCDIC character set.

**EBCDIC**

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 6 | | | | | b | | | | | |
| 7 | | | | | | . | < | ( | + | |
| 8 | & | | | | | | | | | |
| 9 | ! | $ | * | ) | ; | ¬ | - | / | | |
| 10 | | | | | | | , | % | _ | |
| 11 | > | ? |  |  |  |  |  |  |  |  |
| 12 | ` |  | : | # | @ | , | = | " |  | a |
| 13 | b | c | d | e | f | g | h | i |  |  |
| 14 |  |  |  |  |  | j | k | l | m | n |
| 15 | o | p | q | r |  |  |  |  |  |  |
| 16 |  | ~ | s | t | u | v | w | x | y | z |
| 17 |  |  |  |  |  |  |  |  |  |  |
| 18 | [ | ] |  |  |  |  |  |  |  |  |
| 19 |  |  |  | A | B | C | D | E | F | G |
| 20 | H | I |  |  |  |  |  |  |  | J |
| 21 | K | L | M | N | O | P | Q | R |  |  |
| 22 |  |  |  |  |  |  | S | T | U | V |
| 23 | W | X | Y | Z |  |  |  |  |  |  |
| 24 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

The numbers 6-24 in the first column specify the left digit(s), and the numbers 0-9 in the second row specify the right digits of the characters in the EBCDIC data set. For example, the character in the row marked 19 (the number in the first column) and the column marked 3 (the number in the second row) is A. Therefore, the character at position 193 (which is the 194th character) is A. Moreover, the character b at position 64 represents the space character. The preceding table does not show all the characters in the EBCDIC character set. In fact, the characters at positions 00–63 and 250–255 are nonprintable control characters.

*This page intentionally left blank*

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1263_0.png)

## APPENDIX D

## OPERATOR OVERLOADING

The following table lists the operators that can be overloaded.

**Operators that can be overloaded**

| | | | | | | | |
|---|---|---|---|---|---|---|---|
| + | - | * | / | % | & | \| | ^ |
| ! | && | \|\| | = | == | < | <= | > |
| >= | != | += | -= | *= | /= | %= | ^= |
| \|= | &= | << | >> | >>= | <<= | ++ | -- |
| ->* | , | -> | [] | () | ~ | new | delete |

The following table lists the operators that cannot be overloaded.

**Operators that cannot be overloaded**

| | | | | |
|---|---|---|---|---|
| . | .* | :: | ?: | sizeof |

*This page intentionally left blank*

## APPENDIX E: ADDITIONAL C++ TOPICS

### Binary (Base 2) Representation of a Nonnegative Integer

#### Converting a Base 10 Number to a Binary Number (Base 2)

Chapter 1 remarked that *A* is the 66th character in the ASCII character set, but its position is 65 because the position of the first character is 0. Furthermore, the binary number 1000001 is the binary representation of 65. The number system that we use daily is called the **decimal number system** or **base 10 system**. The number system that the computer uses is called the **binary number system** or **base 2 system**. In this section, we describe how to find the binary representation of a nonnegative integer and vice versa.

Consider 65. Note that:

$65 = 1 \times 2^6 + 0 \times 2^5 + 0 \times 2^4 + 0 \times 2^3 + 0 \times 2^2 + 0 \times 2^1 + 1 \times 2^0$

Similarly:

$711 = 1 \times 2^9 + 0 \times 2^8 + 1 \times 2^7 + 1 \times 2^6 + 0 \times 2^5 + 0 \times 2^4 + 0 \times 2^3 + 1 \times 2^2 + 1 \times 2^1 + 1 \times 2^0$

In general, if $m$ is a nonnegative integer, then $m$ can be written as:

$m = a_k \times 2^k + a_{k-1} \times 2^{k-1} + a_{k-2} \times 2^{k-2} + \cdots + a_1 \times 2^1 + a_0 \times 2^0,$

for some nonnegative integer $k$, and where $a_i = 0$ or $1$, for each $i = 0, 1, 2, \ldots, k$. The binary number $a_k a_{k-1} a_{k-2} \cdots a_1 a_0$ is called the **binary** or **base 2 representation** of $m$. In this case, we usually write:

$m_{10} = (a_k a_{k-1} a_{k-2} \cdots a_1 a_0)_2$

and say that $m$ to the base 10 is $a_k a_{k-1} a_{k-2} \cdots a_1 a_0$ to the base 2.

For example, for the integer 65, $k = 6$, $a_6 = 1$, $a_5 = 0$, $a_4 = 0$, $a_3 = 0$, $a_2 = 0$, $a_1 = 0$, $a_0 = 1$. Thus, $a_6 a_5 a_4 a_3 a_2 a_1 a_0 = 1000001$, so the binary representation of 65 is 1000001, that is:

$65_{10} = (1000001)_2$.

If no confusion arises, then we write $(1000001)_2$ as $1000001_2$.

Similarly, for the number 711, $k = 9$, $a_9 = 1$, $a_8 = 0$, $a_7 = 1$, $a_6 = 1$, $a_5 = 0$, $a_4 = 0$, $a_3 = 0$, $a_2 = 1$, $a_1 = 1$, $a_0 = 1$. Thus:

$711_{10} = 1011000111_2$.

It follows that to find the binary representation of a nonnegative integer, we need to find the coefficients, which are 0 or 1, of various powers of 2. However, there is an easy algorithm, described next, that can be used to find the binary representation of a nonnegative integer. First, note that:

$0_{10}=0_2$, $1_{10}=1_2$, $2_{10}=10_2$, $3_{10}=11_2$, $4_{10}=100_2$, $5_{10}=101_2$, $6_{10}=110_2$, and $7_{10}=111_2$.

Let us consider the integer 65. Note that $65 / 2 = 32$ and $65 \% 2 = 1$, where % is the mod operator. Next, $32 / 2 = 16$, and $32 \% 2 = 0$, and so on. It can be shown that $a_0 = 65 \% 2 = 1$, $a_1 = 32 \% 2 = 0$, and so on. We can show this continuous division and obtaining the remainder with the help of Figure E-1.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1266_0.png)

**FIGURE E-1** Determining the binary representation of 65

Notice that in Figure E-1(a), starting at the second row, the second column contains the quotient when the number in the previous row is divided by 2 and the third column contains the remainder of that division. For example, in the second row, $65 / 2 = 32$, and $65 \% 2 = 1$. In the third row, $32 / 2 = 16$ and $32 \% 2 = 0$, and so on. For each number in the second column, when it is divided by 2, the quotient is written in the next row, below the current row, and the remainder is written in the third column. When using a figure, such as E-1, to find the binary representation of a nonnegative integer, typically, we show only the quotients and remainders as in Figure E-1(b). You can write the binary representation of the number starting with the last remainder in the third column, followed by the second last remainder, and so on. Thus:

$65_{10} = 1000001_2$.

Next, consider the number 711. Figure E-2 shows the quotients and remainders.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1267_0.png)

**FIGURE E-2** Determining the binary representation of 711

From Figure E-2, it follows that:

$711_{10} = 1011000111_2$.

### Converting a Binary Number (Base 2) to Base 10

To convert a number from base 2 to base 10, we first find the weight of each bit in the binary number. The weight of each bit in the binary number is assigned from right to left. The weight of the rightmost bit is 0. The weight of the bit immediately to the left of the rightmost bit is 1, the weight of the bit immediately to the left of it is 2, and so on. Consider the binary number 1001101. The weight of each bit is as follows:

```
weight 6 5 4 3 2 1 0
       1 0 0 1 1 0 1
```
