# Table 20.1. The adaptive-refinement algorithm (with automatic boundary refinement) applied to the linear elasticity equations in the circle (with Poisson ratio ν = 1/3). The modified multigrid preconditioner costs the same as 2.5 symmetric Gauss–Seidel iterations. (The setup time is negligible.)

| level | nodes | PCG-MG | PCG-AMG | PCG-SGS |
| --- | --- | --- | --- | --- |
| 1 | 4 | 36 | 36 | 54 |
| 2 | 13 | 12 | 11 | 13 |
| 3 | 45 | 14 | 16 | 32 |
| 4 | 173 | 21 | 21 | 73 |
| 5 | 679 | 39 | 38 | 177 |
| 6 | 2690 | 64 | 58 | 398 |
| 7 | 10329 | 104 | 96 | 895 |

Gauss–Seidel preconditioner. This advantage becomes clearer as finer and finer meshes are used.

# 20.11 Exercises

+   1. Write the code that assembles the stiffness matrix for the linear elasticity equations. The solution can be found in Section A.23 of the Appendix.
+   2. Modify the "refine" function in Chapter 14, Section 6, to implement the criterion for refinement in Section 20.8. The solution can be found in Section A.23 of the Appendix.
+   3. Modify the "createTransfer" function in Section A.18 of the Appendix to implement the modified multigrid algorithm in Section 20.9. The solution can be found in Section A.23 of the Appendix.
+   4. Use your answers to the previous exercises to implement the adaptive-refinement algorithm for the linear elasticity equations. Use automatic boundary refinement, as in Chapter 14, Section 8. Print the resulting meshes and verify that they are indeed conformal. How does the number of nodes change from level to level?