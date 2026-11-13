location pointed by k in polynomial c. The pointers j and k are advanced to the next term.

+   3. If the exponent of the term pointed by j in b is less than the exponent of the current term pointed by i of a, then copy the current term of a pointed by i in the location pointed by k in polynomial c. Advance the pointer i and k to the next term.

Each time a new term is generated, its coefficient and exponent fields are set accordingly. The resultant term then is attached to the end of the polynomial c. The current term of polynomial c is indicated by k.

Figure 2.25 shows the pictorial representation of polynomials a, b, and c using a two-dimensional array and indices.

| Index i | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| Coefficient | 4 | 8 | 5 | 1 | 4 |
| Exponent | 9 | 6 | 3 | 2 | 0 |

| Index j | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| Coefficient | 3 | 1 | -2 | 5 |
| Exponent | 7 | 3 | 1 | 0 |

| Index k | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| Coefficient | 4 | 3 | 8 | 6 | 1 | 2 | 5 |
| Exponent | 9 | 7 | 6 | 3 | 2 | 1 | 0 |

Fig. 2.25 Storing polynomials in a 2D array (a) P(x) = 4x^9 + 8x^6 + 5x^3 + x^2 + 4x (b) P(x) = 3x^7 + x^3 - 2x + 5 (c) P(x) = 4x^9 + 3x^7 + 8x^6 + 6x^3 + x^2 + 2x + 5