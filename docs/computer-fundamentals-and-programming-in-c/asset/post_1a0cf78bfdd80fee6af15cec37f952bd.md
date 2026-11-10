
### 1's Complement

A signed number with 1's complement is represented by changing all the bits that are 1 to 0 and all the bits that are 0 to 1. Reversing the digits in this way is also called complementing a number, as illustrated by the examples below.

**EXAMPLE**

Obtaining the 1's complement of (i) 10001 and (ii) 101001.

**Solution:**

| Number | 1's Complement |
| --- | --- |
| 10001 | 01110 |
| 101001 | 010110 |

> **Note**
>
> - -0 and +0 are represented differently even though they are the same algebraically.
> - This causes problems when carrying out tests on arithmetic results.
> - Hence, 1's complement is an unpopular choice for integer representation.
> - Most computers now use a variation of 1's complement (called 2's complement) that eliminates the problem.

### 2's Complement

The 2's complement of a binary number is obtained by adding 1 to the 1's complement representation as illustrated by the examples below.

**EXAMPLE**

Obtain 2's complement of (i) 10001 and (ii) 101001.

**Solution:**

| Number | 1's Complement | 2's Complement |
| --- | --- | --- |
| 10001 | 01110 | 01111 |
| 101001 | 010110 | 010111 |

### Subtraction using signed 1's complement representation

In this type of representation, subtraction is carried out by addition of 1's complement of the negative number. The sign bit is treated as a number bit in the subtraction method. For the sign bit being 0, i.e., positive, the magnitude part of the result is the true value. For the sign bit being 1, i.e., negative, the magnitude part of the result is in 1's complement form. For subtracting a smaller number from a larger number, the 1's complement method is implemented as follows.

- 1. Determine the 1's complement of the smaller number.
- 2. Add the 1's complement to the larger number.
- 3. Remove the final carry (overflow bit) and add it to the result, i.e., if the sum exceeds n bits, add the extra bit to the result. This bit is called the end-around carry.

**EXAMPLE**

Subtract 1₁₀ from 7₁₀ using 1's complement.

**Solution:**

Now, 1₁₀ = 0001₂ and 7₁₀ = 0111₂.

- 1. The problem is stated with the numbers in binary.

  ```
  0111  (7)  Minuend
  - 0001  (1)  Subtrahend
  ------
  sign bit
  ```

- 2. Convert 0001₂ to its negative equivalent in 1's complement. To do this, change all 1's to 0's and 0's to 1's in 0001₂ form. Notice that the most significant digit is now 1 since the number is negative.

  ```
  0001  →  1110
  sign bit's complement / Subtrahend in 1's complement form
  ```

- 3. Add the negative value 1110₂ to 0111₂. This gives the sum 10101₂.

  ```
  0101
  +   1
  -----
  0110  (6) Sum
  Overflow bit / sign bit
  ```

- 4. Notice that the addition generated an overflow bit. Whenever an overflow bit occurs in such a method, add the bit to the sum to get the correct answer. If there is no overflow bit, leave the sum as it is.

  ```
  0101
  +   1
  -----
  0110  (6) Sum
  Overflow bit / sign bit
  ```

- 5. This gives a final answer of 0110₂ (or 6₁₀).

  ```
  0111  (7)
  - 0001  (1)  True magnitude
  ------
  0110  (6)
  sign bit
  ```

**EXAMPLE**

Subtracting 1001₂(9₁₀) from 1101₂(13₁₀) using 1's complement.

**Solution:**

The subtraction between binary numbers 1101₂(13₁₀) and 1001₂(9₁₀) can be carried out by converting 1001₂ to its negative equivalent in 1's complement and adding this value to 1101₂.

- 1. The problem is stated in binary numbers.

  ```
  1101  (13)
  - 1001   (9)
  ------
  sign bit
  ```

- 2. Convert 01001₂ to its negative equivalent 10110₂ in 1's complement. To do this, change all the 1's to 0's and 0's to 1's. Notice that the most significant digit is now 1 since the number is negative.

- 3. Add the negative value 10110₂ to 01101₂. This gives the sum 100011₂.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_0.png)

- 4. Note that the addition caused an overflow bit. Whenever an overflow bit occurs in such a method, add this bit to the sum to get the correct answer. Hence, the result is 00100₂ (or 4₁₀).

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_1.png)

For subtracting a larger number from a smaller number, the 1's complement method is as follows:

- 1. Determine the 1's complement of the larger number.
- 2. Add the 1's complement to the smaller number.
- 3. There is no carry (overflow). The result has the proper sign bit but the answer is in 1's complement of the true magnitude.
- 4. Take the 1's complement of the result to get the final result. The sign of the result is obtained from the sign bit of the result.

**EXAMPLE**

Subtracting 7₁₀ from 1₁₀ using 1's complement.

**Solution:**

- 1. State the problem with the numbers in binary.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_2.png)

- 2. Convert negative 0111₂ to 1's complement and add this to 0001₂.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_3.png)

- 3. The result does not cause an overflow, so the sum need not be adjusted. Note that the final result is a negative number since the sign bit is 1. Therefore, the result is in 1's complement notation; the correct decimal value for the result is −6₁₀ and not 9₁₀. This is obtained by taking the 1's complement of the result.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_4.png)

**EXAMPLE**

Subtracting 1101₂ (13₁₀) from 1001₂ (9₁₀) using 1's complement.

**Solution:**

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_5.png)

- 1. The problem is stated.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_6.png)

- 2. Convert 01101₂ to its negative equivalent in 1's complement and add to 01001₂.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_7.png)

- 3. The sign bit of the sum being 1, the resulting number is negative and the value is in 1's complement form.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_8.png)

### Subtraction using signed 2's complement representation

Subtraction for this representation is done by addition of the 2's complement of the negative number. The sign bit is treated as a number bit during subtraction. Thus, the result is obtained with the sign bit. When the sign bit is 0, i.e., positive, the magnitude part of the result is the true value. But when the sign bit is 1, i.e., negative, the magnitude part of the result is in 2's complement form. Therefore, the 2's complement of the magnitude part of the result gives the true value. The carry bit that evolves with the sum is ignored in the 2's complement method.

For subtracting a smaller number from a larger number, the 2's complement method is implemented as follows:

- 1. Determine the 2's complement of the smaller number.
- 2. Add the 2's complement to the larger number.
- 3. Discard the final carry (there is always one in this case).

**EXAMPLE**

Subtracting 1₁₀ from 7₁₀ using 2's complement.

**Solution:**

Now, 1₁₀ = 0001₂ and 7₁₀ = 0111₂.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_9.png)

- 1. The problem is stated with numbers in binary.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_49_10.png)

- 2. Convert 0001₂ to its negative equivalent in 2's complement. To do this, change all the 1's to 0's and 0's to 1's and add one to the number. Notice that the most significant digit is now 1 since the number is negative.

  ```
  0001 → 1110
         + 1
  2's complement form → 1111
  ```

- 3. Add the negative value 1111₂ to 0111₂. This gives the sum 10110₂.

  ```
  sign bit
      0111   (7)
   + 1111  (-1)
   -------
    10110   (?)
  overflow bit
  ```

- 4. Notice that the addition caused an overflow bit. Whenever an overflow bit in 2's complement occurs, it is discarded. Hence, the final result is 0110₂ (or 6₁₀).

  ```
      0111   (7)
   + 1111  (-1)
   -------
     0110   (6)
  Result in true magnitude
  sign bit
  ```

**EXAMPLE**

Subtracting the binary number 1001₂(9₁₀) from 1101₂(13₁₀) by converting 1001₂ to its negative equivalent in 2's complement and adding this value to 1101₂.

**Solution:**

- 1. State the problem.

  ```
         Magnitude part
   01101   (13)  Minuend
 - 01001   (9)   Subtrahend
  ```

- 2. Convert 1001₂ to its negative equivalent in 2's complement. To do this, change all 1's to 0's and vice versa.

  ```
  1's complement form
   01001 → 10110
   ↑
  sign bit
  ```

- 3. Add 1 to the number to obtain the negative equivalent. Notice that the most significant digit is now 1 since the number is negative.

  ```
   10110
 +     1
 -------
   10111   (-9) Subtrahend in 2's complement
  ```

- 4. Add the negative value 10111₂ to 01101₂. This gives the sum 100100₂. However, the leftmost bit, which is the overflow bit, is discarded.

  ```
   01101   (13)
 + 10111  (-9)
 ---------
  100100   (?)
 Overflow bit
  ```

- 5. Hence, the final result is 00100₂ (or 4).

  ```
   01101   (13)
 + 10111  (-9)
 ---------
   00100   (4)
 sign bit   True magnitude
  ```

For subtracting a larger number from a smaller number, the 2's complement method is implemented as follows.

- 1. Determine the 2's complement of the larger number.
- 2. Add 2's complement to the smaller number.
- 3. There is no carry from the leftmost column. The result is in 2's complement form and is negative.
- 4. Take the 2's complement of the result to get the final answer.

**EXAMPLE**

Subtracting 1101₂(13₁₀) from 1001₂(9₁₀) using 2's complement.

**Solution:**

- 1. State the problem.

  ```
   01001   (9)
 - 01101  (13)
  ```

- 2. Convert 1101₂ to its negative equivalent in 2's complement.

  ```
   01101 → 10011
           ↑
       2's complement
  ```

- 3. Next, add 10011₂ to 01001₂. The sign bit being 1, the result is negative and the magnitude is in 2's complement.

  ```
   01001
 + 10011
 -------
   11100
   ↑ sign bit
   2's complement
  ```

- 4. Take the 2's complement of the sum to get -0100₂ = -4₁₀.

### Points to remember

The steps for subtracting y from x, with an n-bit 1's complement representation are as follows.

- 1. Negate y using 1's complement, i.e., reverse all the bits in y to form -y.
- 2. Add -y in 1's complement form, and x.
- 3. If the sum exceeds n bits, add the extra bit to the result.
- 4. If the sum does not exceed n bits, leave the result as it is.

The steps for subtracting y from x with an n-bit 2's complement representation are as follows.

- 1. Negate y using 2's complement, i.e., reverse all the bits in y and add 1 to form -y.
- 2. Add -y in 2's complement form, and x.
- 3. If the sum exceeds n bits, discard the extra bit.

Notice that with 1's complement, it is necessary to check for an overflow bit each time subtraction is performed. If the result has an overflow bit, the extra bit is added to the result to obtain the correct result. However, with 2's complement, this extra bit is ignored. No other computations are required to find the correct result.

## 2.6.4 Multiplication

Binary multiplication uses the same techniques as decimal multiplication. In fact, binary multiplication is much easier because each multiplying digit is either zero or one. Consider the simple example of multiplying 110₂ by 10₂. This example is used to review some terminology and illustrate the rules for binary multiplication.

**EXAMPLE**

Multiplying 110₂ by 10₂.
