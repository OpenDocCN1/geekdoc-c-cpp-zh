
In the calculator application, click the following keys to start counting in binary: click 1, *, = and then keep clicking = to count up by 1 on each click. The first time that the equals button is clicked, the count increments from 1 to 10 in binary which is the same as counting from 1 to 2 in decimal. The decimal equivalent of the current binary number can be seen next to DEC in the calculator. Figure 4.2 shows the Windows calculator used to count up in binary.

![](img/83ef13a6c66cc7882b2f357e97f451dc_71_0.png)

Figure 4.2: Windows Calculator in Binary Mode

Table 4.1 shows binary numbers with preceding zero place holders, for example 0000 instead of 0 and 0001 instead of 1. It does not matter whether these preceding place holders are shown or not, the number will always have the same value, so the binary number 0011 is the same as 11 and has a decimal value of 3.

Experiment with counting up in binary with the calculator to get a clearer understanding of how binary works. Still to come in this chapter is a look at how the binary numbering system is a weighted system which will further enhance understanding of binary.

Note that 0b is used to indicate binary numbers in this book, except where context indicates that the number is binary, for example in the above paragraphs on this page.

### 4.1.2 Bytes and Nibbles

When a microcontroller is designed, a size of binary number is chosen that the microcontroller can fetch and operate on. In an 8-bit microcontroller architecture the microcontroller fetches and operates on 8-bit wide data. An 8-bit wide number can have a value from 0, or 0b00000000 (0 decimal) to a maximum of 0b11111111 (255 decimal). Figure 4.3 shows examples of 8-bit wide memory locations storing binary numbers.

![](img/83ef13a6c66cc7882b2f357e97f451dc_72_0.png)

Figure 4.3: 8-bit Wide Memory Storing Binary Numbers

A byte refers to an 8-bit wide number or memory location that consists of 8 memory cells and is therefore 8 bits wide. Half a byte, or four bits is referred to as a nibble.

## 4.2 Weighted Number Systems

Both the decimal and binary number systems are weighted number systems. A quick explanation of weighting in the decimal system will help with understanding the same concept for binary numbers.

### 4.2.1 Weighted Decimal Numbers

Table 4.2 shows an example of the decimal weights for a four digit number 4692. The weight of each digit is ten raised to the power of the digit position number. Digit position numbering starts at the right of the number with a value of 0. The digit at the very right of the number is the least significant digit (LSD) and is 2 in this example. The digit at the very left of the number is known as the most significant digit (MSD) and is 4 in this example.

Table 4.2: Weighted Decimal Number Example

| Digit Number | 3 | 2 | 1 | 0 |
|---|---|---|---|---|
| Weight | 10³ | 10² | 10¹ | 10⁰ |
| | 10 x 10 x 10 | 10 x 10 | 10 | 1 |
| | 1000 | 100 | 10 | 1 |
| Number | 4 | 6 | 9 | 2 |
| | 4 x 1000 | 6 x 100 | 9 x 10 | 2 x 1 |

The point of this explanation of weights in numbers is to show that a number such as 4692 used in this example does not consist of four numbers each consisting of units, namely 4, 6, 9 and 2. Rather the position of a digit in a number determines its value, and the value is determined by its weight. In other words the number 4692 consists of 4000, 600, 90 and 2 rather than 4, 6, 9 and 2. The explanation that follows shows how the weight of a digit in a number is determined mathematically.

Starting at the very right of the number (the least significant digit, or LSD), the weight of the number is calculated by raising 10 to the power of zero (10^0). Any number raised to the power of zero is 1, so the LSD has a weight of 1. The value of the LSD in this example is 2, because we have two ones, or 2 x 1.

The digit to the left of the LSD has a position number 1. The weight value of the digit in this position is calculated by raising 10 to the power of 1 (10^1). Any number raised to the power of 1 is itself, so the weight of this digit is 10. The value of the number at this position in this example is 9, but because of its position and therefore its weight it has a value of ten nines (10 x 9) or 90.

The weight of the third digit from the right has a position number 2 and a weight of ten to the power of two (10^2) which is ten times ten or 100 (raising ten to the power of two shows how many times ten must be multiplied by itself, in this case two times). In the example number this means that we have six one-hundreds (6 x 100) or 600.

Finally the most significant digit or MSD has a position number of 3, a weight of ten to the power of three (10^3) or 1000. The example number therefore has a value of four one-thousands (4 x 1000) or 4000. If the number had a fifth digit, it would have a position number of 4 and a weight of ten to the power of four or 10000, and so on for each additional digit in the number. This new digit would then become the MSD.

### 4.2.2 Weighted Binary Numbers

The binary number system works in the same way as the decimal number system explained in the previous section, except that the weight of each digit is calculated by raising two to the power of the digit position.

Table 4.3 shows a binary number with a value of 1011 and the weight of each digit in the number. The right most digit can be called the least significant digit or least significant bit (LSB). The left most digit can be called the most significant digit or most significant bit (MSB).

| Digit Number | 3 | 2 | 1 | 0 |
|---|---|---|---|---|
| Weight | 2³ | 2² | 2¹ | 2⁰ |
| | 2 x 2 x 2 | 2 x 2 | 2 | 1 |
| Number | 1 | 0 | 1 | 1 |
| | 1 x 8 | 0 x 4 | 1 x 2 | 1 x 1 |

Starting at the LSB, the weight of this digit is two to the power of zero (2⁰). Again, any number raised to the power of zero is 1, so the weight of this digit is 1 and the value of the digit is therefore one times one (1 x 1).

The next digit to the left has a weight of two to the power of one (2¹) which is two. The value of the digit is therefore one times two (1 x 2) in this example. The next digit has a weight of two to the power of two (2² or 2 x 2) which is four. The value of the digit in this example is 0, or zero fours (0 x 4) which is zero. The next digit has a weight of two to the power of three (2³) or 2 x 2 x 2 which is eight. We therefore have one eight (1 x 8) in the example number. Adding up the value of each digit times its weight gives us the decimal value of the number, as shown below.

0b1011 = (1 x 8) + (0 x 4) + (1 x 2) + (1 x 1) = 11 decimal

This can be checked on a calculator by typing 1011 into the calculator when it is in binary mode and then changing it to decimal mode (some calculators require the = key to be pressed after typing the number in, but before changing to decimal mode). As with the weighted decimal number system, if we added another digit to the number it would have a weight that can be calculated in the same way. A fifth digit would have a weight of two to the power of four, or 16, and so on for each additional digit. When a new digit is added to the left of a number it becomes the new MSD or MSB.

## 4.3 Hexadecimal Numbers

Hexadecimal numbers are a compact way of representing binary numbers. Decimal has 10 digits and is known as a base ten numbering system. Binary is a base two number system with two different digits. Hexadecimal has 16 different digits and is known as a base sixteen numbering system.

### 4.3.1 Counting in Hexadecimal

Counting in hexadecimal starts the same way as decimal from 0 to 9. After 9, there are six more numbers to count through that are represented by the letters A to F. Counting therefore goes 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F.

After counting up to F in hexadecimal we are out of digits. To count higher than F, the next most significant digit is incremented by one and the hexadecimal number becomes 10. The number 10 hexadecimal has a decimal value of 16. After 10 hexadecimal, the least significant digit is incremented the same way again, as follows: 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 1A, 1B, 1C, 1D, 1E, 1F. We are out of digits again, so increment the MSD by 1 and count through the numbers 0 to F again at the LSD: 20, 21, ..., 2A, 2B, 2C, and so on. In this book hexadecimal numbers are written starting with 0x (zero ex), for example 0xA1, 0xFF, 0x14, and so on.

In the same way that the Windows calculator was used to count up in binary, we can count up in hexadecimal. With the calculator in Programmer mode, click the Hex option. Now click 1, +, = and then continue to click = to count up by 1 on each click. The Windows 10 calculator shows the decimal value of the current hexadecimal number, next to DEC. BIN on the calculator shows the binary value of the current number. Other calculators may require the mode to be changed from hexadecimal to decimal to see the decimal value, or to binary mode to see the number in binary.

### 4.3.2 Using Hexadecimal to Represent Binary

Hexadecimal digits 0 to F directly represent a four bit binary number from 0b0000 to 0b1111 as shown in Table 4.4. This allows an eight bit binary number to be represented by only two hexadecimal digits which makes the number easier to read and understand. For example the binary number 0b11110111 can be written as 0xF7, which is shorter and easier to read. Once you are experienced in using hexadecimal numbers, it is easy to see the binary equivalent of a hexadecimal number in your head.
