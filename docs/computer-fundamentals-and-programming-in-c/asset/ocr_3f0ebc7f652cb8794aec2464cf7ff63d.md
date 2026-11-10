+   4. Now, subtraction of the next column is carried out. Since a 1 was borrowed from this column, the subtraction is 0 minus 1 and a borrow has to be made again. However, there is no borrow in the next column. So first, a borrow from the most significant column must be made.
+   
+       1 1  Borrow
+       10101
+       - 01110  Subtrahend
+       -------
+       00111  Result
+   
+   5. Then borrow a 1 from the fourth column to the current column.
+   
+         1
+       111  Borrow
+       10101  Minuend
+       - 01110  Subtrahend
+       -------
+       00111  Result
+   
+   6. Now the current column can be subtracted. A 1 is taken away from the group of two 1's. This leaves a single 1 which is written below the column.
+   
+         1
+       111  Borrow
+       10101  Minuend
+       - 01110  Subtrahend
+       -------
+       00111  Result
+   
+   7. In the fourth column, a 1 is subtracted from a 1 for a result of 0.
+   
+         1
+       111  Borrow
+       10101  Minuend
+       - 01110  Subtrahend
+       -------
+       00111  Result
+   
+   8. The most significant column contains all zeros, so 0 is written below it. Hence, the result is 00111₂.
+   
+         1
+       111  Borrow
+       10101  Minuend
+       - 01110  Subtrahend
+       -------
+       00111  Result

# 2.6.3 Binary

So far in the study of binary arithmetic, only positive numbers have been considered. Now, a way is needed to represent numbers such as −32₁₀. When computations are done in decimal, a minus sign precedes a number to make it negative. Since computers can only work with 1's and 0's, it is necessary to modify this approach slightly.

One solution is to add an extra binary digit to the left of the binary number to indicate whether the number is positive or negative. In computer terminology, this digit is called a sign bit. Remember that a 'bit' is simply another name for a binary digit. When a number is positive, the sign bit is zero, and when the number is negative, the sign bit is one. This approach is

called the signed magnitude representation. Note that this is very similar to adding a minus sign in decimal.

Still one small problem remains with the representation. It is necessary to specify how many bits are there in a number to know which bit is representing the sign. Let us convert the decimal numbers −5₁₀ and −1₁₀ to binary using signed magnitude representation. For these numbers, four bits will be enough to represent both.

+   1. 5 and 1 are converted to binary.
+   
+       101  (5)
+         1  (1)
+   
+   2. Now a positive sign bit is added to each one. Notice that '1' is padded with zeros so that it has four bits.
+   
+       0101  (5)
+       0001  (1)
+          ↑
+       sign bit
+   
+   3. To make the binary numbers negative, simply change the sign bit from 0 to 1.
+   
+       1101  (−5)
+       1001  (−1)

One has to be sure not to mistake the number 1101₂ for 13₁₀. Since a four-bit signed magnitude representation is used, the first bit is the sign bit and the remaining three bits are for the magnitude (absolute value) of the number.

Therefore, the sign and magnitude of the integer are represented separately. A negative integer, for example, is represented by a 1 in the leftmost bit and the absolute value in the remaining bits. The range of integers that can be stored in signed magnitude is −2^{n−1} + 1 to +2^{n−1} − 1, where n is the number of bits in the signed magnitude number.

While representing negative numbers with signed magnitude is simple, performing arithmetic with signed magnitude is difficult. Consider the subtraction problem 30₁₀ − 6₁₀. This can be converted to an equivalent addition problem by changing 6₁₀ to −6₁₀. Now, the problem may be restated as 30₁₀ + (−6₁₀) = 24₁₀. Something similar can be done in binary by representing negative numbers as complements. Two ways of representing signed numbers using complements will be discussed: 1's complement and 2's complement in the next section.

+   **Note**
+   
+   - When a single bit number 1 is added with another single bit number 1 the sum bit is 0 and the carry bit is 1.
+   - When a single bit number 1 is subtracted from a single bit number 0 the difference bit is 1 and the borrow bit is 1.
+   - In the signed magnitude representation of binary numbers, the integer is represented by a sign bit in the most significant bit position followed by the binary representation of the magnitude. For a negative integer, the msb is 1 whereas for a positive integer the msb is 0.
+   - Subtraction of integers in signed 2's complement representation produces results in true signed magnitude form.