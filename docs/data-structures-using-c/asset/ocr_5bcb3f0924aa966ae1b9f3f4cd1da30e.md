Let us execute the KMP algorithm to find whether P occurs in the string S or not, and if yes, we find the number of its occurrences.

For P, the prefix function π was computed previously and is as follows:

| Q | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| P | a | b | a | b | a | c | a |
| π | 0 | 0 | 1 | 2 | 3 | 1 | 1 |

Initially, n = size of S = 15

m = size of P = 7

# Step 1: i = 1, q = 0

Now, compare P[1] with S[1].

We notice that P[1] does not match with S[1].

So, let us shift P by one position to the right.

![](bbox=[0.223, 0.422, 0.882, 0.522])

# Step 2: Now, i = 2, q = 0

Comparing P[1] with S[2], we see that there is a match; P is not shifted.

![](bbox=[0.223, 0.602, 0.882, 0.692])

# Step 3: Currently, i = 3, q = 1. Comparing P[2] with S[3], we notice that P[2] does not match with S[3].

![](bbox=[0.223, 0.772, 0.882, 0.872])