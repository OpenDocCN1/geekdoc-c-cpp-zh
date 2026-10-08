Consider hexadecimal. We need to name the 16 values from 0 to 15. Usually, we use 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, where A has the decimal value 10, B the decimal value 11, and so on:

**A===10, B===11, C===12, D===13, E===14, F===15**

We can now write the decimal value **123** as **7B** using the hexadecimal notation. To see that, note that in the hexadecimal system **7B** means **7\*16+11**, which is (decimal) **123**. Conversely, hexadecimal **123** means **1\*16^2+2\*16+3**, which is **1\*256+2\*16+3**, which is (decimal) **291**. If you have never dealt with non-decimal integer representations, we strongly recommend you try converting a few numbers to and from decimal and hexadecimal. Note that a hexadecimal digit has a very simple correspondence to a binary value:

| Hexadecimal and binary | |
|---|---|
| hex | **0** | **1** | **2** | **3** | **4** | **5** | **6** | **7** |
| binary | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 |
| hex | **8** | **9** | **A** | **B** | **C** | **D** | **E** | **F** |
| binary | 1000 | 1001 | 1010 | 1011 | 1100 | 1101 | 1110 | 1111 |


This goes a long way toward explaining the popularity of hexadecimal notation. In particular, the value of a byte is simply expressed as two hexadecimal digits.

In C++, (fortunately) numbers are decimal unless we specify otherwise. To say that a number is hexadecimal, we prefix **0X** (“X for hex”), so **123===0X7B** and **0X123===291**. We can equivalently use a lowercase **x**, so we also have **123===0x7B** and **0x123===291**. Similarly, we can use lowercase **a, b, c, d, e**, and **f** for the hexadecimal digits. For example, **123===0x7b**.

Octal is base-8. We need only eight octal digits: **0, 1, 2, 3, 4, 5, 6**, **7**. In C++, base-8 numbers are represented starting with a **0**, so **0123** is not the decimal number **123**, but **1\*8^2+2\*8+3**, that is, **1\*64+2\*8+3**, or (decimal) **83**. Conversely, octal **83**, that is, **083**, is **8\*8+3**, which is (decimal) **67**. Using C++ notation, we get **0123===83** and **083===67**.

Binary is base-2. We need only two digits, **0** and **1**. In C++14, but not in earlier standards, we can represent binary literals using the prefix **0b**. For example, (decimal) **123** is **0b1111011**. Earlier, you had to say something like **1\*64+1\*32+1\*16+0\*8+0\*4+1\*2+1**.

When a literal has many digits, it can be hard to read. In that case, we can use another C++14 feature, digit separators. For example:

```
0b1010'1111'0110      0xFF00'AAAA'77BB'00FF      1'000'000'345.75
```