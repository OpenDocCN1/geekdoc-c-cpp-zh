# Appendix B = Solutions to Exercises 491

# Chapter 2: Numerical Algorithms

+   1. Simply map 1, 2, and 3 to heads and 4, 5, and to tails.

+   2. In this case, the probability of getting heads followed by heads is $3 \div 4 \times 3 = 9 \div 16$. The probability of getting tails followed by tails is $1 \div 4 \times 1 = 1 \div 16$. Because these independent outcomes, you can add their probabilities. So there is $9 \div 16 + 1 \div 16 = 10 \div 16$, or $62.5\%$, probability that you'll need to try again.

+   3. If the coin is fair, the probability that you will get heads followed by tails is $1 \div 2 \times 1 = 1 \div 4$. Similarly, the probability that you'll get tails followed by tails is $1 \div 2 \times 1 = 1 \div 4$. Because these are independent outcomes, you can add their probabilities. So there is $1 \div 4 + 1 \div 4 = 1 \div 2$, or $50\%$, probability that you'll need to try again.

+   4. You can use a method similar to the one that uses a biased coin to produce coin flips:

Roll the biased die 6 times.
If the rolls include 6 possible values, return the first one.
Otherwise, repeat.

Depending on how biased the die is, it could take many trials to roll all six values. For example, if the die is fair (the same case), the probability of rolling all six values is $6! \div 6^6 = 720 \div 46656 = 0.015$, so there's only about $1.5\%$ chance that six rolls will give six different values. Another example, if the die rolls 1 half of the time and each of the other five values one-tenth, the probability of getting all five values in six rolls is $0.5 \times 0.1^5 \times 6! = 0.0036$, or $0.36\%$. You may be rolling the die for a long time.

+   5. You can use the same algorithm to randomize an array, you can stop after positioning the first M items:

```
String: PickM(String: array[], Integer: M)
Integer: max_i = <Upper bound of array>
For i = 0 to M - 1
  // Pick the item for position in the array.
  Integer: j = <pseudo-random number between i and max_i inclusive>
  <Swap the values of array[i] and array[j]>
Next i
<Return array[0] through array[M-1]>
PickM
```

This algorithm runs in O(M) time because $M \le N, O(M) \le O(N)$. In practice, M is often much less than N, so this algorithm may be much faster than randomizing the entire array.