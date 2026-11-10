3. Let φ be an annihilating polynomial for the vector e = e_i + e_j and let φ_1 = φ_{A,e_i}, φ_2 = φ_{A,e_j}. We have φ_2(A)φ(A)e_i = φ_2(A)φ(A)e − φ(A)φ_2(A)e_j = 0. Hence φ_2φ is annihilating the vector e_i, and is therefore divisible by φ_1. Now since φ_1 and φ_2 are coprime, we have φ_1 | φ_2φ, thus φ is a multiple of φ_1φ_2. Now φ_1φ_2 is annihilating e, thus φ = φ_1φ_2.

4. P_1 and P_2 being coprime, there exist two polynomials α and β such that 1 = αP_1 + βP_2. Thus for any vector x, we have x = α(A)P_1(A)x + β(A)P_2(A)x = x_2 + x_1, where x_1 = β(A)P_2(A)x and x_2 = α(A)P_1(A)x. As φ_A = P_1P_2, P_1 is annihilating x_1 = β(A)P_2(A)x (similarly P_2 is annihilating x_2). If for any vector x, x_1 = 0, then βP_2 is annihilating A and is therefore a multiple of P_1P_2, hence 1 = P_1(α + γP_2), which implies deg P_1 = 0. Therefore, there exists a nonzero x_1 such that P_1 is an annihilating polynomial of x_1. We will now show that P_1 is minimal for x_1: let P̃_1 be an annihilating polynomial of x_1. Then P̃_1(A)P_2(A)x = P_2(A)P̃_1(A)x_1 + P̃_1(A)P_2(A)x_2 = 0, hence P̃_1P_2 is a multiple of φ_A = P_1P_2. Hence P_1 | P̃_1, and P_1 is therefore the minimal polynomial of x_1. The reasoning is identical for x_2.

5. For each factor φ_i^{m_i}, there exists a vector x_i for which φ_i^{m_i} is the minimal polynomial and the vector x_1 + ··· + x_k has minimal polynomial φ_A.

6. One first computes the minimal polynomial of the matrix A.

```
```
sage: A = matrix(GF(7),[[0,0,3,0,0],[1,0,6,0,0],[0,1,5,0,0],
....:                  [0,0,0,0,5],[0,0,0,1,5]])
sage: P = A.minpoly(); P
x^5 + 4*x^4 + 3*x^2 + 3*x + 1
sage: P.factor()
(x^2 + 2*x + 2) * (x^3 + 2*x^2 + x + 4)
```
```

It has maximal degree.

```
```
sage: e1 = identity_matrix(GF(7),5)[0]
sage: e4 = identity_matrix(GF(7),5)[3]
sage: A.transpose().maxspin(e1)
[(1, 0, 0, 0, 0), (0, 1, 0, 0, 0), (0, 0, 1, 0, 0)]
sage: A.transpose().maxspin(e4)
[(0, 0, 0, 1, 0), (0, 0, 0, 0, 1)]
sage: A.transpose().maxspin(e1 + e4)
[(1, 0, 0, 1, 0), (0, 1, 0, 0, 1), (0, 0, 1, 5, 5),
 (3, 6, 5, 4, 2), (1, 5, 3, 3, 0)]
```
```

The method `maxspin` iterates a vector on the left. We therefore apply it on the transpose of the matrix so as to produce the list of linearly independent Krylov iterates from the vectors e_1 and e_4. The minimal polynomial of e_1 thus has degree 3, that of e_4 has degree 2, and that of e_1 + e_4 has degree 5. Note that the shape of the matrix implies that the vectors e_1 and e_4 produce iterates that are also vectors of the canonical basis. This form is also called the Frobenius normal form (see §8.2.3). It describes how the