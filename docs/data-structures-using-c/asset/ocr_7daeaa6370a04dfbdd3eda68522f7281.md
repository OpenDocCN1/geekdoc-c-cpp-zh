9. Explain the term dictionary. List the suitable data structures for implementation of dictionaries.

10. In what way is a skip list a more suitable data structure for implementing dictionaries?

11. Compare skip lists and hashing.

# Answers to multiple choice questions

+   1. (b) It will be one more than the size of the biggest cluster (which is 4 here). This is because assume a search key hashing on to bin 8. By linear probing, the next location for searching is bin 9, then 0, and then 1. If all these resulted in a mess, we try at bin 2 and stop as it is vacant. Of course, this logic will not work if deletion is performed before search.

| $S_7$ | $S_1$ | $S_4$ | $S_2$ | $S_6$ | | | | $S_8$ | $S_3$ |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

+   2. (c)

+   3. (a) Using Huffman code, a is 1111, b is 0, c is 110, d is 1110, e is 10.
+   Average code length = (4 x 0.12) + (1 x 0.4) + (3 x 0.15) + (4 x 0.08) + (2 x 0.25) = 2.15

+   4. (a) Load factor is the ratio of the number of records that are currently present and the total number of records that can be present. If the load factor is less, free space will be more. Hence, the probability of collision is less. So the search time will be less.

+   5. (b) If the new record hashes onto one of the six locations 7, 8, 9, 10, 1 or 2, the location will receive a new record. The probability is 6/10 as 10 is the total possible number of locations.

+   6. (a)