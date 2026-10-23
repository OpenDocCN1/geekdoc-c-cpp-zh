```
int J = (*runner)()[j].getIndex();
A(I,J) += gradient[j]*weight*gradient[i];
}
} // assembling the stiffness matrix
```

Actually, in the nested loop over the vertices of a triangle, only pairs 'i' and 'j' for which 'i' is less than or equal to 'j' are used; contributions from pairs for which 'i' is greater than 'j' will be added to the stiffness matrix A later by substituting

A ← A + Aᵗ − diag(A).

Indeed, thanks to the symmetry in the original bilinear form a(·,·), the contribution from e to the matrix element Aᵢ,ⱼ is the same as the contribution to Aⱼ,ᵢ. It is thus unnecessary to calculate it twice; it would be more efficient to add it only to Aᵢ,ⱼ now, and postpone its addition to Aⱼ,ᵢ to the next part of the code, where the transpose Aᵗ will be added as above.

# 13.6 Exercises

+   1. Assume that the numerical solution is contained in a dynamic vector v, with dimension equal to the number of nodes in the mesh. (The "index" field in a "node" object is the same as the index of the component in v that contains the value at that node.) Assume also that the solution has a singularity at the origin, so one is interested in the maximum solution away from it. Write a function "maxNorm" that calculates the maximum modulus of the components in v that correspond to nodes of distance 0.1 or more from the origin. (You may assume that the function is a member of the "mesh" class.) The solution can be found in Section A.14 of the Appendix.

+   2. Write a function "refineBoundary" that successively refines a coarse mesh as in Figure 12.9 until it approximates the circular boundary well (Figure 12.10). You may assume that the function is a member of the "mesh" class. The solution can be found in Section A.14 of the Appendix.

+   3. Assume that the right-hand side of the PDE is F(x,y) ≡ 1. Write a function that takes a "mesh" object as an argument and returns the right-hand-side vector in the stiffness system. (You may use the polynomials of two variables in Chapter 5, Sections 13 and 14.)

+   4. Modify the code in Section 13.5 so that it also calculates and assembles the contribution to the stiffness matrix from the mixed boundary conditions (see Chapter 12, Section 6).

+   5. Apply your code to the uniform mesh in Figure 12.3 and verify that the stiffness matrix is indeed symmetric and diagonally dominant.

+   6. Apply your code to the mesh that approximates a circle as in Figure 12.10. Verify that the stiffness matrix is indeed tridiagonal as in Chapter 12, Section 9.

+   7. Modify the above code to assemble the stiffness matrix for the PDE
+   −uₓₓ(x,y) − uᵧᵧ(x,y) + u(x,y) = F(x,y).