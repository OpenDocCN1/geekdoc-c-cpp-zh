These scalars are placed in a "polynomial" object, on which Horner’s algorithm is called once again to calculate the required value

p(x, y) = Σ_i a_i x^i.

The solution can be found in Section 24.7 below.

29. Modify your code in the previous exercise to use the short-memory approach. The a_i’s are calculated as before, but no longer placed in a "polynomial" object but rather only used to add on the term a_i x^i, and dropped soon after. In this case, however, Horner’s algorithm cannot be used to calculate the final sum Σ a_i x^i, and the standard algorithm in Section 5.6 must be used instead. Is this worthwhile to avoid the construction of the extra "polynomial" object and simplify the code?

30. Let f(x, y) be a given function of two variables, and let x and y be fixed. Consider the polynomial p(h_x, h_y) of the two variables h_x and h_y, whose coefficients are given by

a_{i,j} = 1/(i!·j!) · ∂^{i+j} f / ∂^i x ∂^j y (x, y).

Actually, p(h_x, h_y) is the Taylor approximation of f(x + h_x, y + h_y):

f(x + h_x, y + h_y) ≈ p(h_x, h_y).

Calculate the Taylor approximation of the function f(x, y) = sin(x)cos(y) at x = ±π/4, y = ±π/3, h_x = ±0.1, and h_y = ±0.1. Verify that the approximation indeed improves as the degree of p increases.

31. Compare your code from the previous exercise to your answer to a similar exercise at the end of Chapter 3. Do you indeed obtain the same numerical results? Which code is more efficient? Which code is more transparent?

32. Use the above guidelines to implement polynomials of three variables x, y, and z. (Use polynomials of polynomials of polynomials.) The solution can be found in Section 24.8 below.

33. In some cases, most of the coefficients in the polynomial p(x) vanish, so it makes no sense to store them. In this case, it makes more sense to store only the nonzero coefficients of the polynomial in a linked list. Implement the class of sparse polynomials, including arithmetic operations such as addition and multiplication of polynomials. The solution can be found in Section A.9 in the Appendix.

34. In the context of sparse polynomials, it makes no sense to implement polynomials of two variables as polynomials of polynomials, because the linked list may then become rather dense, which spoils the whole idea of sparsity. Instead, the polynomial p(x, y) should be implemented as a linked list of its coefficients a_{i,j}, ordered lexicographically in the indices i and j. Write the class that implements these objects. The solution can be found in Section A.9 in the Appendix.