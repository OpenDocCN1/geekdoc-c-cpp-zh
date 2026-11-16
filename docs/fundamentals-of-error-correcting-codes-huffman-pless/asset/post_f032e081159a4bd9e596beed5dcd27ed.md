
| Group number | Hexacode codeword | Number in group |
| :--- | :--- | :--- |
| I | 01 01 \(\bar{\omega}\bar{\omega}\) | \(3 \times 12 = 36\) |
| II | \(\bar{\omega}\bar{\omega}\) \(\bar{\omega}\bar{\omega}\) \(\bar{\omega}\bar{\omega}\) | \(3 \times 4 = 12\) |
| III | 00 11 11 | \(3 \times 3 = 9\) |
| IV | 11 \(\omega\bar{\omega}\) \(\omega\bar{\omega}\) | \(3 \times 2 = 6\) |

in \(\mathcal{G}_6\) in Table 10.1 in groups, telling how many are in each group. Each codeword in the table is separated into pairs. Additional codewords in the group are obtained by multiplying by \(\omega\) or \(\bar{\omega}\), permuting the pairs in any order, switching the order in any two pairs, and by any combination of these. In the table, the column "Number in group" tells how many codewords can be obtained from these operations. For example the group containing 00 11 11 also contains 11 00 11 and 11 11 00 together with all multiples by \(\omega\) and \(\bar{\omega}\).

## **Exercise 583** Do the following:
- (a) Show that the permutations \(p_1 = (1, 3)(2, 4)\), \(p_2 = (1, 3, 5)(2, 4, 6)\), and \(p_3 = (1, 2)(3, 4)\) are in \(\text{PAut}(\mathcal{G}_6)\).
- (b) Find a product of \(p_1\), \(p_2\), and \(p_3\) that:
  - (i) interchanges the pairs (3, 4) and (5, 6),
  - (ii) sends (3, 4) to (4, 3) and simultaneously (5, 6) to (6, 5). \(\blacklozenge\)

## **Exercise 584** Show that the number of codewords in each group of Table 10.1 is correct. \(\blacklozenge\)

## **Exercise 585** Decide if the following vectors are in the hexacode \(\mathcal{G}_6\):
- (a) \(10\bar{\omega}01\),
- (b) \(\bar{\omega}\omega 0011\),
- (c) \(0\bar{\omega}\bar{\omega}\bar{\omega}01\),
- (d) \(1\omega 10\omega 1\). \(\blacklozenge\)

We now demonstrate how to decode a received vector \(\mathbf{y} = \mathbf{c} + \mathbf{e}\) where \(\mathbf{c} \in \mathcal{G}_{24}\) and \(\text{wt}(\mathbf{e}) \le 3\). The decoding falls naturally into four cases depending on the parities of the columns of \([\mathbf{y}]\). The received vector uniquely determines which case we are in. In particular, if the received vector has odd weight, then one or three errors have occurred and we are in Case 1 or Case 3 below. (Note that the case number is **not** the number of errors.) If the received vector has even weight, then zero or two errors have occurred and we are in Case 2 or Case 4. If we cannot correct the received vector by following the procedure in the appropriate case, then more than three errors have been made. Because the covering radius of \(\mathcal{G}_{24}\) is 4, if more than three errors are made, the nearest neighbor is not the correct codeword and the procedure will fail to produce \(\mathbf{c}\). If four errors have been made, then Case 2 or Case 4 will arise; with more work, we can find six codewords within distance 4 of the received vector using these same techniques as in Cases 2 or 4. We will not describe the procedure for handling four errors; the interested reader can consult [268]. Please keep in mind that we are assuming at most three errors have been made.

## Case 1: Three columns of [y] have even parity and three have odd parity

In this case, we know that three errors must have occurred and either there is one error in each odd parity column or there is one error in each even parity column. We look at each possibility separately. With each choice, we know three components of Pr(y) that are correct and hence there is only one way to fill in the coordinates in error to obtain a codeword in \(\mathcal{G}_6\).

### Example 10.3.6 Suppose y = 101000011100001000011001. Then we obtain

```
Pr(y) =
0 [1 0 1 0 0 1]
1 0 0 1 0 0 0
ω 1 0 0 1 1 0 0
ω̄ 0 1 0 0 0 1
  ω ω̄ 1 ω ω̄ ω̄
```

Notice that columns 1, 3, and 6 have even parity and columns 2, 4, and 5 have odd parity. Suppose the columns with odd parity are correct. Then Pr(c) = *0*ω0*ω*, where we must fill in the *'s. The only possibility for Pr(c) is from group I or II in Table 10.1. If it is in group I, it must be 0ω0ω0ω0, which cannot be completed. So Pr(c) = ω0ω0ω0ω0. Since we make only one change in each of columns 1, 3, and 6, we obtain

```
0 [0 0 1 0 0 1]
1 0 0 1 0 0 1
ω 1 0 1 1 0 0
ω̄ 0 1 0 0 1 1
  ω ω̄ ω̄ ω ω ω
```

However, the columns have odd parity while the first row has even parity, which is a contradiction. So the columns with even parity are correct and Pr(c) = *1***ω*. The only possibility for Pr(c) is from group IV; hence Pr(c) = ω011ω0. Since we make only one change in each of columns 2, 4, and 5, we obtain:

```
0 [1 0 1 0 1 1]
1 0 1 1 0 0 0
ω 1 0 0 1 0 0
ω̄ 0 1 0 1 1 1
  ω 1 1 1 ω ω
```

As all columns and the first row have even parity, this is the codeword.

## Case 2: Exactly four columns of [y] have the same parity

As we are assuming that at most three errors have been made, we know that the four columns with the same parity are correct and the other two columns each contain exactly one error.

### Example 10.3.7 Suppose y = 10001110100000000101000. Then:

```
0 [ 0 1 1 0 0 0 1 ]
1   0 1 1 0 0 0 0
ω   0 0 1 0 0 1 0
ω̄   0 1 0 0 0 0 0
   0 0 1 0 ω ω 0
```

Thus columns 1, 3, 5, and 6 have odd parity and 2 and 4 have even parity. So Pr(c) = 0*1*ω0. This must be in group I; hence Pr(c) = 0ω1ω̄00. We must make one change in each of columns 2 and 4 so that the top row has odd parity. This gives

```
0 [ 1 1 0 0 0 1 ]
1   0 1 1 0 0 0
ω   0 0 0 0 1 0 0
ω̄   0 1 0 1 0 0 0
   0 ω 1 ω ω 0
```

Since the columns and first row all have odd parity, this is the codeword.

## Case 3: Exactly five columns of [y] have the same parity

As at most three errors have been made, either the five columns with the same parity are correct and the other column has either one or three errors, or four of the five columns are correct with two errors in the fifth and one error in the remaining column. It is easy using Table 10.1 to determine if all five columns of the same parity are correct and then to correct the remaining column. If four of the five columns are correct, a bit more analysis is required.

### Example 10.3.8 Suppose y = 110010001001000010010110. Then:

```
0 [ 1 1 0 0 1 0 ]
1   1 0 0 0 0 1
ω   0 0 0 0 0 1
ω̄   0 0 1 0 1 0
   1 0 ω 0 ω ω
```

Column 2 is the only column of odd parity, and so one or three errors have been made in this column. If all but column 2 of Pr(y) is correct, it is easy to see that no change in column 2 will yield a hexacode codeword from Table 10.1. So four of columns 1, 3, 4, 5 and 6 are correct. If columns 5 and 6 are both correct, then Pr(c) must be in either group III or IV in which case two of columns 1, 3, and 4 must be in error; this is an impossibility. In particular, columns 1, 3, and 4 are correct, and Pr(c) = 1*ω̄*ω*, which must be in group I. The only possibility is Pr(c) = 1ω0ω0ω0. Thus the correct codeword must be:

```
0 [ 1 1 1 0 1 0 ]
1 [ 1 0 0 0 0 0 ]
ω [ 0 1 0 0 0 0 ]
ω̄ [ 0 0 1 0 1 0 ]
[ 1 ω ω̄ 0 ω̄ 0 ]
```

Note that the columns and first row all have even parity.

## Case 4: All six columns of [y] have the same parity

This is the easiest case to solve. If the top row has the same parity as the columns and Pr(y) is in \(\mathcal{G}_6\), no errors were made. Otherwise, as we are assuming that at most three errors have been made and because the parity of the six columns is correct, any column that is incorrect must have two errors. Hence at most one column is incorrect. The correct vector Pr(c) is easy to find and hence the incorrect column, if there is one, is then clear.

### Example 10.3.9 Suppose y = 011100101011000111011101. Then:

```
Pr(y) =
0 [ 0 0 1 0 0 1 1 ]
1 [ 1 0 0 0 0 1 1 ]
ω [ 1 1 1 0 0 0 0 ]
ω̄ [ 1 0 1 1 1 1 1 ]
[ 0 ω 1 ω̄ ω ω ]
```

Clearly, all columns cannot be correct, and it is impossible for both columns 5 and 6 to be correct. Thus as columns 1, 2, 3, and 4 must be correct, the only possibility is for Pr(c) to be in group I and Pr(c) = 0ω1ω0ω0. Thus two entries in column 6 must be changed and the correct codeword is

```
0 [ 0 0 1 0 1 1 ]
1 [ 1 0 0 0 1 0 ]
ω [ 1 1 0 0 0 0 ]
ω̄ [ 1 1 1 0 1 0 ]
[ 0 ω 1 ω̄ ω 0 ]
```

## **Exercise 586** Decode the following received vectors when \(\mathcal{G}_{24}\) is used in transmission or show that more than three errors have been made:

- (a) 00111001101110101000011,
- (b) 11001101011011101001100,
- (c) 00010100101111010111001,
- (d) 10101011110010010010101,
- (e) 10111011110010000100110.

The tetrahedral code can be used in a similar manner to decode the [12, 6, 6] extended ternary Golay code; see [268]. This technique has been generalized in [143].
