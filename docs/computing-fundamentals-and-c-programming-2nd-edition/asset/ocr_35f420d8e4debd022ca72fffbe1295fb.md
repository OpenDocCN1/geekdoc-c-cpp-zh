# ## 2.7 BINARY ARITHMETIC OPERATIONS

The computer arithmetic is also referred to as *binary arithmetic* because the computer system stores and processes the data in the binary form only. Various binary arithmetic operations can be performed in the same way as the decimal arithmetic operations, but by following a predefined set of rules. Each binary arithmetic operation has an associated set of rules that should be adhered to while carrying out that operation. The binary arithmetic operations are usually simpler to carry out as compared to the decimal operations because one needs to deal with only two digits, 0 and 1, in the binary operations. The different binary arithmetic operations performed in a computer system are:

+   * Binary addition
+   * Binary multiplication
+   * Binary subtraction
+   * Binary division

# ### 2.7.1 Binary Addition

Binary addition is the simplest arithmetic operation performed in the computer system. Like decimal system, we can start the addition of two binary numbers column-wise from the right-most bit and move towards the left-most bit of the given numbers. However, we need to follow certain rules while carrying out the binary addition of the given numbers. Table 2.8 lists the rules for binary addition.

**Table 2.8** *Binary addition rules*

| A | B | A + B | Carry |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

In the above table, the first three entries do not generate any carry. However, a carry would be generated when both A and B contain the value, 1. The carry, if it is generated, while performing the binary addition in a column would be forwarded to the next most significant column.

**Example 2.27** *Perform the binary addition operation on the following binary numbers:*

```text
0 0 1 0
0 1 1 1
```

**Solution**
The given binary numbers are 0010 and 0111.
Now, perform the binary addition of the given numbers as:

```
Binary number       Decimal value

0 0 1 0             2
0 1 1 1             7
-------             -
1 0 0 1             9
```

Therefore, the result of the binary addition performed on 0010 and 0111 is 1001.

> **Note** In the above example, a carry is generated in the 2nd and the 3rd column only.