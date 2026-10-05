15. Let the target consist of a series of A's and the text consist of runs M - 1 A's followed by a B. For example, if M is 4, the target is AAAA, and the text is AAAB repeated number of times. In this case, the target is not present in the text, there are never M A's in a row. The outer loop runs i, the inner loop runs over M, M - 2, ..., values to decide that it has not found a match. The sequence repeats. On average, the inner loop runs roughly M / 2 times, giving a total run time of O(N × M / 2) = O(N × M).

16. The least-cost path uses as diagonal lines as possible. In Figure 15-13, a path can use four diagonal lines. A path that uses four diagonal lines uses five nondirectional links, so the edit distance is 5.

17. Example program StringDistance does this.

18. Example program'Distance does this.

19. The edit distance is commutative. To transform word 2 into word 1, you can reverse operations. In other words, instead of deleting a character, insert one, and instead of inserting a character, delete one.

20. Example program FileEditDistance does this.

21. Example program FileEditDistance does this.

# # Chapter 16: Encryption

+   1. Example program RowColumnTranspose does this.
2. Example program SwapColumns does this.
3. If the keys contain duplicated characters, there's no way to know which of the corresponding columns should come first.

One solution is to use only the first occurrence of each letter, so PIZZA becomes PIZA and BOOKWORD becomes BOKWRM. This actually has the small benefit of increasing obscurity if the attacker doesn't know the rule, because it disguises the number of columns in the encryption array.

Swapping both columns and rows greatly increases the possible number of arrangements of rows and columns. For
 Swapping both columns and rows greatly increases the possible number of arrangements of rows and columns. For example, a message contains 100 characters and is written into a 10×10 array, there are 10! × 10! = 1.3×10¹³ possible arrangements of rows and columns.

However, if the attacker figures out the column ordering, the rows will be out of order, but each row in the array will contain valid words. By recognizing the valid rows, the attacker can recover the column ordering and try to swap rows to recover the full message.

If each row begins with a new word, finding the row ordering could be difficult. But if words spans rows, the pieces of the words will give the attacker extra clues for finding the row ordering. For example, suppose the first row ends with GREA,