
Note that BCD (packed or unpacked) takes up more space because each of the decimal digits is codified separately. This wastage can be justified in situations where fractional numbers are involved. A decimal number having a fractional component can be accurately converted only to BCD and not to binary.

## 3.3 NEGATIVE BINARY NUMBERS

In arithmetic, we use the - symbol on the left of the most significant digit (MSD) to signify a number as negative. So, binary -1111 is mathematically equivalent to decimal -15. But computers are designed to handle only 0s and 1s; there's no room for a third symbol. Computers handle negative numbers by using the left-most bit to indicate the sign. This bit is known variously as the Most Significant Bit (MSB), sign bit or high-order bit. Positive numbers have the MSB set to 0 and negative numbers have it set to 1. The remaining bits are used for the magnitude (value) of the number.

Positive one-byte integers use all 8 bits for the magnitude and none for the sign. This makes it possible to represent the 256 numbers between 0 and 255 (2^8 - 1). However, if a number can be negative, then the MSB must be reserved for the sign. The range of numbers then changes from -127 to +127 or -128 to +127, depending on the scheme used by the computer to store negative numbers. It's the programmer's job to tell the computer whether it should treat a number or a numeric variable as signed or unsigned.

There are mainly three schemes for storing the magnitude of a negative number. Let's briefly examine them with reference to byte-sized (8 bits) integers.

### 3.3.1 Sign-and-Magnitude Representation

In this system, the left-most bit (MSB) is allocated for the sign as usual: 0 for positive and 1 for negative numbers. The remaining 7 bits are reserved for the magnitude or value. For instance, the number (127)10 is represented as 01111111 in binary, where the MSB or high-order bit is set to 0. To negate this number to -127, set this bit to 1 and the number then becomes 11111111. Here are two more examples:

| Decimal | Binary | Decimal | Binary |
|---|---|---|---|
| 6 | 0000110 | 56 | 00111000 |
| -6 | 1000110 | -56 | 10111000 |

Using a byte-sized integer, the sign-magnitude system can represent values between -127 and +127, but it has an inherent flaw: it creates two zeroes. The number 00000000 is positive zero and 10000000 is negative zero. Two zeroes create problems when comparing numbers, the reason why this system is not used today.

### 3.3.2 One's Complement

In this system, a negative number is represented as the one's complement of the positive number. This means inverting all bits of the number, i.e. changing 0s to 1s and 1s to 0s. The significance of the MSB remains the same—0 for a positive number and 1 for negative numbers. The following examples show how the one's complement of (15)10 and (85)10 are derived:

| Decimal | Binary | Decimal | Binary |
|---:|---:|---:|---:|
| 15 | 00001111 | 85 | 01010101 |
| -15 | 11110000 | -85 | 10101010 |

The one’s complement of zero (00000000) is 11111111, which is -0. The problem of positive and negative zero remains here as well. The one’s-complement system was once used by IBM and PDP for some of their machines. Today, it plays the role of an “assistant” to the two’s-complement system.

> **Note:** Testing for a zero in both sign-magnitude and one’s complement forms becomes tedious because one has to test for both +0 and -0.

### 3.3.3 Two's Complement

This is the most widely accepted system for representing negative numbers. The two’s complement of a number is simply its one’s complement with a 1 added to it. The following example illustrates the point:

| Description | Binary | Note |
|---|---:|---|
| Decimal +15 | 00001111 | |
| -15 in one’s complement form | 11110000 | *High-order bit set* |
| Adding 1 to one’s complement | +1 | |
| -15 in two’s complement form | 11110001 | *High-order bit set* |

How does two’s complement handle the “two-zero” problem? In the one’s complement system, -0 is represented as 11111111. When you add 1 to it, an overflow is generated which is ignored in the two’s complement system:

| Description | Binary | Note |
|---|---:|---|
| Decimal +0 | 00000000 | |
| -0 in one’s complement form | 11111111 | |
| Adding 1 to one’s complement | +1 | |
|  | 100000000 | *Overflow to be ignored* |
| -0 in two’s complement form | 00000000 | *Same as +0* |

You’ll soon learn that binary addition of 1 and 1 creates 10 (2 in decimal), where the 1 is carried over to the left bit. That’s how adding 1 to 11111111 reset all of these 1s to 0s but it also resulted in a carry of 1. By ignoring this carry, two’s complement ensures that there is only one zero in the system. The range of numbers changes slightly; it’s -128 to 127 compared to -127 to 127 that is possible with the one’s complement system.

With negative binary numbers encroaching on half of the domain of the unsigned ones, how does one interpret a binary number, say, 11111111 that has its MSB set? The answer is one of the following:

- (i) 255 if the number is declared as unsigned, i.e., a positive number.
- (ii) -127 in sign-magnitude form.
- (iii) -0 in one’s complement form.
- (iv) -1 in two’s complement form.

The answer in (i) depends on us—the way we *declare* the number in a program. The other answers depend on the computer—the way it internally stores negative numbers. Declaration of a number belongs to a later topic (5.2.2).

> **Takeaway:** By simply looking at a binary number that has its MSB or high-order bit set, you can't determine its actual value. If the number is declared to the computer as unsigned, then the *entire* number is the actual value. However, if the number is signed, the value would depend on the system used by the processor to store negative numbers.

## 3.4 BINARY ARITHMETIC

We have just added 1 to a binary number without knowing the formal rules related to binary addition. If you thought that there is nothing special in binary arithmetic, then you are absolutely right. The rules of arithmetic were not based on a specific numbering system. The standard “carry” and “borrow” techniques used for decimal arithmetic apply equally to binary arithmetic (or, for that matter, any arithmetic).

### 3.4.1 Binary Addition

How do you add two decimal integers? Right-align the numbers and then sum the columns from right to left. If the sum of one column can't be held in a single digit, carry the extra digit to the next column. The following example shows the carry-over generated by columns 2 and 3 when adding the decimal numbers 398 and 56:

```text
  11                  Carry over digits
 398
+ 56
----
 454                  Sum
```

The addition of 8 and 6 takes place first. It generates a carry of 1 (from 14) which is shown at the top of column 2. This column, which uses the carry, generates yet another carry which is used by column 1.

Binary addition is no different except that (i) digits are restricted to 0 and 1, (ii) addition of 1 and 1 generates a carry of 1 (1 + 1 = 10). Here are three examples of binary addition; the first one doesn't create a carry but the others do:

|  | 11 | 1111 | *Carry over bits* |
|---|---|---|---|
| 1010 | 1110 | 1111 | |
| + 101 | + 111 | + 1 | |
| 1111 | 10101 | 10000 | *Sum* |
|  | 1234 | 1234 | *Column ruler* |

The first example computes 1111 or (15)10 as the sum. This is based on the principle that the sum of 0 and 1 evaluates to 1. The second example features two carry operations. Column 3 generates a carry from 1 + 1. This carry is then embedded in the expression 1 + 1 + 1 of column 2, which creates 11 as the sum. Another carry is thus generated for column 1 which sums 1 and 1 to 10. The third example generates a carry for every column summed. That’s how (1111)₂ is incremented to (10000)₂.

### 3.4.2 Binary Subtraction (Regular Method)

There are two ways of performing binary subtraction—the normal way and using the two’s complement form. The normal way is to simply right-align the numbers and then subtract the *subtrahend* from the *minuend* while moving from right to left. If the subtrahend is larger than the minuend, you borrow a 1 from the left column. Consider the following example that features decimal subtraction:

|  |  |
|---:|---:|
| 81 | *Borrowed digit* |
| 967 | *Minuend* |
| - 483 | *Subtrahend* |
| 484 | *Difference* |

Subtraction in column 2 requires a 1 to be borrowed from column 1. *This 1 has a weight equal to the base*, i.e., 10. It is thus multiplied by 10 and added to 6, yielding 16 from where 8 is subtracted. Because the previous column has “lent” this 1 to the next column, the minuend 9 gets reduced to 8.

The same principles are followed in binary subtraction where 0 - 1 = 1 after borrowing 1 from the previous bit. Also, a borrowed bit has a weight of 2 and not 10. Consider the following three examples of which two feature borrowing:

|  |  |  |  |
|---:|---:|---:|---:|
|  | 0111 | 01111 | *Borrowed bit* |
| 1111 | 10101 | 10000 | *Minuend* |
| - 101 | - 111 | - 1 | *Subtrahend* |
| 1010 | 1110 | 1111 | *Difference* |
| 1234 | 12345 | 12345 | *Column ruler* |

The first example needs no explanation. In the second example, borrowing begins from column 4. The borrowed 1 is multiplied by the base (2) and then the subtrahend 1 is subtracted from it. The minuend of column 3 (which has now become 0) borrows from column 2. But column 2 can only lend after it has borrowed from column 1. The third example shows how continuous borrowing reduces (10000)₂ by 1 to (1111)₂.

### 3.4.3 Binary Subtraction Using Two’s Complement

We have known since high school that 7 - 3 is the same as 7 + -3. In other words, subtraction is the same as addition of the minuend with the negative representation of the subtrahend, i.e., its two’s complement. Subtraction using two’s complement is easily achieved by following these simple steps:

- Ensure that both minuend and subtrahend have the same number of bits by padding one of them with 0s if necessary.
- Convert the subtrahend first to its one’s complement, i.e. by inverting all of its bits. Add 1 to the one’s complement to obtain the two’s complement.
