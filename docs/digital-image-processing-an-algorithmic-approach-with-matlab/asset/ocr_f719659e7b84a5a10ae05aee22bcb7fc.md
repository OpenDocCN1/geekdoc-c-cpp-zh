# TABLE 1.1 Comparison of MATLAB and C Code for Simple Matrix Operations

| Operation | Part of C code | MATLAB statements |
| :--- | :--- | :--- |
| Addition of two matrices A and B | `for (i==1, i<=M, ++) {
 for (j==1, j<=N, j++) {
 D[i][j] = A[i][j] + B[i][j];
 }
}` | D = A + B ; |
| Multiplication of two matrices A and B | `for (i==1, i<=M, ++) {
 for (j==1, j<=N, j++) {
 for (c==1, c<=N, c++) {
 for (r==1, r<=M, r++) {
 D[i][j] += A[i][c] * B[c][j] [r];
 }
 }
 }
}` | D = A * B ; |

applications. The best solution would be to test the logic and algorithms in MATLAB first because this will boost the initial development speed. Once the algorithm is finalized, it should be translated into C and then compiled into an executable file for real-time or near real-time applications. One comment for those students who are not too enthusiastic about coding: "You will forget about other languages once you start working with MATLAB." This is true most of the time for typical engineering student chores, as observed from personal experience. However, one must realize the fact that for real-world applications, the need for a near machine-language-type environment cannot be eliminated, at least for the time being.

# 1.4.2 The Image Processing Toolbox in MATLAB

The Image Processing Toolbox in MATLAB is a collection of functions that supports a wide range of image processing operations, including the following:

+   - Image I/O
+   - Spatial transformations