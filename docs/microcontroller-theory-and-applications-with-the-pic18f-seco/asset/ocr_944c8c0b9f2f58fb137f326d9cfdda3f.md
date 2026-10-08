# 1.2.2  **ASCII and EBCDIC Codes**

If it is to be very useful, a microcontroller must be capable of handling nonnumeric information. In other words, a microcontroller must be able to recognize codes that represent numbers, letters, and special characters. These codes are classified as alphanumeric or character codes. A complete and adequate set of necessary characters includes the following:

+   - 26 lowercase letters
- 26 uppercase letters
- 10 numerical digits (0–9)

+   - Approximately 25 special characters, which include +, /, #, %, and others.

This totals to 87 characters. To represent 87 characters with some type of binary code would require at least 7 bits. With 7 bits there are $2^{7}=128$ possible binary numbers; 87 of these combinations of 0 and 1 bits serve as the code groups representing the 87 different characters.

The two most common alphanumerical codes are the American Standard Code for Information Interchange (ASCII) and the extended binary-coded-decimal interchange code (EBCDIC). ASCII is typically used with microprocessors; IBM uses EBCDIC code. Eight bits are used to represent characters, although 7 bits suffice, because the eighth bit is frequently used to test for errors and is referred to as a *parity bit*. It can be set to 1 or 0 so that the number of 1 bits in the byte is always odd or even.

Note that decimal digits 0 through 9 are represented by $30_{16}$ through $39_{16}$ in ASCII. On the other hand, these decimal digits are represented by $F0_{16}$ through $F9_{16}$ in EBCDIC.

A microcontroller program is usually written for code conversion when input/output devices of different codes are connected to the microcontroller. For example, suppose that it is desired to enter the number 5 into a computer via an ASCII keyboard and to print this data on an EBCDIC printer. The ASCII keyboard will generate $35_{16}$ when the number 5 is pushed. The ASCII code $35_{16}$ for the decimal digit 5 enters the microcontroller and resides in the memory. To print the digit 5 on the EBCDIC printer, a program must be written that will convert the ASCII code $35_{16}$ for 5 to its EBCDIC code, $F5_{16}$. The output of this program is $F5_{16}$. This would be supplied to the EBCDIC printer. Because the printer understands only EBCDIC codes, it inputs the EBCDIC code $F5_{16}$ and prints the digit 5. Note that EBCDIC code is obsolete; it is used here merely for illustrative purposes.

Typical microprocessors such as the Intel Pentium include instructions to provide correct unpacked BCD after performing arithmetic operations in ASCII. The Pentium instruction AAA (ASCII adjust for addition) is such an instruction. The PIC18F does not provide such an instruction.

# 1.2.3  **Unpacked and Packed Binary-Coded-Decimal Numbers**

The 10 decimal digits 0 through 9 can be represented by their corresponding 4-bit binary numbers. The digits coded in this fashion are called *binary-coded-decimal digits* in 8421 code, or BCD digits. Two unpacked BCD bytes are usually packed into a byte to form *packed BCD*. For example, two unpacked BCD bytes $02_{16}$ and $05_{16}$ can be combined as a packed BCD byte $25_{16}$.

Let us consider entering data decimal 24 via an ASCII keyboard into a microcontroller. Two keys (2 and 4) will be pushed on the ASCII keyboard. This will generate 32 and 34 (32 and 34 are ASCII codes in hexadecimal for 2 and 4, respectively)