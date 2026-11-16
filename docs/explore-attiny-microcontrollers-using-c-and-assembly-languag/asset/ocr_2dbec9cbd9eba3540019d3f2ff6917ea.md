number to 1's compliment and then add 1. Positive 23 changes from 0b0001_0111 to 1's compliment format which is 0b1110_1000. Now we add 1 to change the number to 2's compliment format: 0b1110_1000 + 1 becomes 0b1110_1001. When adding binary digits we have the following possible sums:

+   0 + 0 = 0
+   0 + 1 = 1
+   1 + 0 = 1
+   1 + 1 = 0 with a carry of 1

If we take another example and convert -40 to 2's compliment format, first +40 is 0b0010_1000. 1's compliment is then 0b1101_0111. We must now add 1 to make it 2's compliment. The addition can be done on a calculator in binary mode, or using the binary addition rules mentioned above as follows. Write the 1's compliment number down and place the 1 to add to it directly under the LSB as follows.

```
11010111
+
1
```

Add the LSB of the top number to the digit below it, which is 1 + 1. We get a result of 0 and a carry of 1. The 0 result is placed below the second number, and aligned with the LSB, as can be seen in the next box. The carry is placed above the digit to the left of the LSB as shown below. It is placed here in preparation for the next step, where it is added to the digit below it.

```
  1
11010111
+    1
=    0
```

Add the carry from the previous addition to the digit at the left of the LSB, which is the digit below the carry. This results in 1 + 1 = 0, with a carry of 1 again, which is placed above the third digit from the right, as shown in the next box. Strictly speaking, we are adding the carry, plus the digit from the first number, plus an invisible zero from the second number. In the next box the invisible zeros from the second number have been filled in with 0 digit place holders, making it 00000001. This number still has a value of 1, but it is easier to see that we are adding the remaining digits of the first number to 0 in the second number, and to the carry number.