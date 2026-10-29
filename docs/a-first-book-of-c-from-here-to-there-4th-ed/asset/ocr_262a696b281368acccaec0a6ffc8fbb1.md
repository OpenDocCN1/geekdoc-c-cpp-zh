Hexadecimal symbols work well for representing the 8 bits in a byte because each byte consists of two groups of 4 bits. (Sometimes 4-bit patterns are referred to as nibbles.) Therefore, a byte's binary code can be represented conveniently with two hexadecimal symbols.

In reviewing the hexadecimal symbols in Table 2.10, notice that the first 10 are the same as those used in the decimal system. After using the familiar 0 to 9 symbols, however, unique symbols are needed for the last six binary patterns in the table. The symbols you recognize as 10 through 15 can't be used because they consist of two symbols, so the letters A through F are used for these six additional symbols. To indicate clearly that hexadecimal numbers are being used, often they're preceded by 0X or 0x, as in 0xF0ACE37B.

# Octal Representation

Although they have almost been superseded by hexadecimal numbers, you might still encounter binary numbers represented in their octal form. Octal numbers group binary numbers in units of three. Table 2.11 shows the correspondence between octal symbols and their 3-bit binary values.

# Table 2.11 Octal to Binary Conversion

| Octal Symbol | Binary Value |
|---|---|
| 0 | 000 |
| 1 | 001 |
| 2 | 010 |
| 3 | 011 |
| 4 | 100 |
| 5 | 101 |
| 6 | 110 |
| 7 | 111 |

Using the values listed in Table 2.11, the octal number 541 represents the binary number 101100001. This is done by replacing the octal value 5 with its equivalent 101 binary bit pattern, replacing the 4 with its corresponding 100 binary bit pattern, and replacing the 1 with its corresponding 001 binary bit pattern.

To convert from binary to octal, first group the binary digits in units of three, proceeding from right to left. In doing this, you might have to add one or two leading zeros to the binary number to pad out the leftmost bit pattern to three binary digits. For example, the 8-bit binary number 11111010 is padded out to nine binary digits by adding a leading zero. The resulting number, 011111010, is then grouped in units of three, as [011]111[010]. The bar symbol, [, has been used to separate each group of three binary digits clearly. Using the correspondence between 3-bit patterns and octal symbols in Table 2.11, this binary number becomes the octal number 372.

Before a byte was standardized to consist of 8 bits, octal numbers were typically used to represent binary values. This method had the added advantage of using numeric symbols that were familiar to people used to dealing with decimal numbers. With the standardization of 8-bit bytes, however, the use of hexadecimal symbols and their correspondence with 4-bit binary numbers became the numbering system of choice for representing binary numbers.