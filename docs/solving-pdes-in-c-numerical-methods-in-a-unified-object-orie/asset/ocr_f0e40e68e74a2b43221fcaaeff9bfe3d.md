10. Index the sides in the mesh M. The solution can be found in Section A.31 in the Appendix.

11. Show that the stiffness matrix A^(s) is symmetric.

12. Write a constructor that produces the sparse matrix B in Section 28.2. The solution can be found in Section A.29 in the Appendix.

13. Modify the above constructor so that the first 10 rows in B are reordered in such a way that the first row corresponds to the zeroth partial derivative (the function itself), the next three rows correspond to the first partial derivatives (the gradient), and the next six rows correspond to the second partial derivatives (the Hessian). Apply the same reordering to the next 30 rows in B as well. (In this order, the basis functions in the reference tetrahedron T are ready for the transformations required to produce the basis functions in a tetrahedron t in the mesh.) The solution can be found in Section A.29 in the Appendix.

14. Write a function that produces the polynomial of three variables p_q from the 56-dimensional vector x̄ in Section 28.2. The solution can be found at the end of Section A.29 in the Appendix.

15. Use the function "d()" in the last exercise at the end of Chapter 24 to verify that the polynomial p_q computed above is indeed a basis function in the sense that it has only one nonvanishing degree of freedom in the reference tetrahedron T.

16. Write the constructor that uses the present high-order finite elements to produce the stiffness matrix A^(s). The solution can be found on the Web page of the book at http://www.siam.org/books/cs09.

17. Let v be an N-dimensional complex vector, in which each component v_i corresponds to the i-th degree of freedom in the above indexing scheme. For each t ∈ M, redefine P_t(v) in Section 27.5 by

P_t(v) ≡ Σ_{i~t} v_i h_{i,t} ∘ D_t.

Use this new definition to redefine and reconstruct the 2N × 2N matrix A^(n)(v), using the present high-order finite elements. The solution can be found on the Web page of the book at http://www.siam.org/books/cs09.

18. Use the previous exercise and the exercises at the end of the previous chapter to write the C++ code that solves the nonlinear Helmholtz equation in the unit cube, using the present high-order finite elements. The solution can be found on the Web page of the book at http://www.siam.org/books/cs09.