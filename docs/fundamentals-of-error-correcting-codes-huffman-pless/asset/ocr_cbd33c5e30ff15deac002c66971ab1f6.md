of coordinates in which x and y differ. The proofs of the following properties of distance are left as an exercise.

# Theorem 1.4.1 The distance function d(x, y) satisfies the following four properties:

+   - (i) (non-negativity) d(x, y) >= 0 for all x, y in F_q^n.
+   - (ii) d(x, y) = 0 if and only if x = y.
+   - (iii) (symmetry) d(x, y) = d(y, x) for all x, y in F_q^n.
+   - (iv) (triangle inequality) d(x, z) <= d(x, y) + d(y, z) for all x, y, z in F_q^n.

This makes the distance function a metric on the vector space F_q^n.

# Exercise 11 Prove Theorem 1.4.1.

The (minimum) distance of a code C is the smallest distance between distinct codewords and is important in determining the error-correcting capability of C; as we see later, the higher the minimum distance, the more errors the code can correct. The (Hamming) weight wt(x) of a vector x in F_q^n is the number of nonzero coordinates in x. The proof of the following relationship between distance and weight is also left as an exercise.

# Theorem 1.4.2 If x, y in F_q^n, then d(x, y) = wt(x - y). If C is a linear code, the minimum distance d is the same as the minimum weight of the nonzero codewords of C.

As a result of this theorem, for linear codes, the minimum distance is also called the minimum weight of the code. If the minimum weight d of an [n, k] code is known, then we refer to the code as an [n, k, d] code.

# Exercise 12 Prove Theorem 1.4.2.

When dealing with codes over F_2, F_3, or F_4, there are some elementary results about codeword weights that prove to be useful. We collect them here and leave the proof to the reader.

# Theorem 1.4.3 The following hold:

+   - (i) If x, y in F_2^n, then wt(x + y) = wt(x) + wt(y) - 2wt(x AND y), where x AND y is the vector in F_2^n which has 1s precisely in those positions where both x and y have 1s.
+   - (ii) If x, y in F_2^n, then wt(x AND y) = x . y (mod 2).
+   - (iii) If x in F_2^n, then wt(x) = x . x (mod 2).
+   - (iv) If x in F_3^n, then wt(x) = x . x (mod 3).
+   - (v) If x in F_4^n, then wt(x) = (x, x) (mod 2).

# Exercise 13 Prove Theorem 1.4.3.

Let A_i, also denoted A_i(C), be the number of codewords of weight i in C. The list A_i for 0 <= i <= n is called the weight distribution or weight spectrum of C. A great deal of research