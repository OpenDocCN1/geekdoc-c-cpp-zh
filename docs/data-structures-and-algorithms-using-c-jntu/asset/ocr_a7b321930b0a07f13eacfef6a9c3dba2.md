$\Sigma$ is the set of pattern symbols or characters. */

# Algorithm 15.2: BM (T, P, $\Sigma$)

```
last=LastFunction(P,$\Sigma$) /*last function prepares the shift table*/
i=m-1
j=m-1
repeat
  if T[i]=P[j]
    if j=0
      return i /*pattern match found at i*/
    else
      i=i-1
      j=j-1
    else /*character-jump*/
      i=last(T[i])
      i=i-max(i,j+1)
    j=m-1
  until i>n-1
return -1 /*pattern not found*/
```

# Boyer-Moore Algorithm with an example:

Text : "THIS IS A TEST OF BOYER MOORE ALGORITHM"

Pattern : "ALGORITHM"

In the first step SHIFT table is filled with all the ASCII characters associated with the length of the pattern “ALGORITHM” (i.e, 9). In the second step, the SHIFT table is modified with the descending count from the length of the pattern.

The SHIFT table consists of the ASCII characters associated with the number of shifts. The matching of the characters starts from the rightmost character of the pattern.

**Pass 1**: In this pass, the **text** character ‘A’ and the **pattern** character ‘M’ are compared. In this case the comparison fails. But the character ‘A’ is present in the set of characters of the pattern. This case is referred to as the Good Suffix Shift. In the shift table, the number of shifts for the character ‘A’ is 8. So, the pattern ‘ALGORITHM’ is moved 8 characters forward.

| A | L | G | O | R | I | T | H | M |
|---|---|---|---|---|---|---|---|---|
| 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | |

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 | 36 | 37 | 38 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Text | T | H | I | S | | I | S | | A | | T | E | S | T | | T | E | S | T | | O | F | | B | O | Y | E | R | | M | O | O | R | E | | A | L | G | O | R | I | T | H | M |
| Pass 1 | A | L | G | O | R | I | T | H | M | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | PASS 1 |
| Pass 2 | | | | | | | A | L | G | O | R | I | T | H | M | | | | | | | | | | | | | | | | | | | | | | | | | | | | PASS 2 |
| Pass 3 | | | | | | | | | | | | | A | L | G | O | R | I | T | H | M | | | | | | | | | | | | | | | | | | | | | | PASS 3 |
| Pass 4 | | | | | | | | | | | | | | | | | | | | A | L | G | O | R | I | T | H | M | | | | | | | | | | | | | | | | | | PASS 4 |
| Pass 5 | | | | | | | | | | | | | | | | | | | | | | | | | A | L | G | O | R | I | T | H | M | | | | | | | | | | | | | PASS 5 |

# Figure 15.2 Execution trace of Boyer-Moore Algorithm