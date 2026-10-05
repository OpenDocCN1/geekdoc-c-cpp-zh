# 492 Appendix B — Solutions to Exercises

To give away five books, you would pick five names to go in the array's first positions and then not stop. This would take five steps, so it would be very quick. It doesn't matter how many names are in the array, as long as there are at least five.

+   6. Simply make an array holding all 52 cards, randomize it, and then deal the cards as you would normally—one to each player in turn until everyone has.

It doesn't matter whether you deal one card to each player in turn or deal all cards not to each player. As long as the deck is randomized, each player will get five randomly cards.

+   7. Figure B-2 shows the program written in C#, which is available for download on the book's website. The numbers for each value are the percentage of rolls that gave the value, the expected percentage for the actual, and the percentage difference.

![](bbox=[0.196, 0.335, 0.583, 0.545])

Figure B-2: Relatively small numbers of trials sometimes result in significant differences between observed and expected frequencies of rolls.

The actual results don't consistently match the expected results until the number of trials is quite large. The program produces more than 5% error for some values about 10,000 or more trials.

+   8. If $A_1 < B_1$, $Mod\ B_1 = A_1$, so $A_2 = B_2$ and $B_2 = A_1$; Mod $B_1 = A_1$. In other words, during the first trip through the While loop, the values of A and B switch.

+   9. $LCD(A, B) = A 	imes B / GCD(A, B)$. Suppose $g = GCD(A, B)$, so $A = g 	imes m$ and $B = g 	imes n$ for some integers $m$ and $n$. Then $A 	imes B / GCD(A, B) = g 	imes m 	imes n / g = g 	imes m 	imes n$. The values $m$ and $n$ have no common factors, so this is the LCM.

+   10. The following pseudocode shows the algorithm used by the FastExponentiation example program that is available for download on the book's website. (The bold lines of code are used for the solution to Exercise 11.)

```
// Perform the exponentiation.
Integer: Exponentiate(Integer: value, Integer: exponent)
```