If the approximate factors $L$ and $U$ produced by the incomplete factorization are close enough to the original $L$ and $U$ of Gaussian elimination, then the ILU iteration should converge rapidly to the numerical solution $x$.

Here is one of the many possible algorithms to construct the approximate $L$ and $U$ factors. The algorithm uses some small predetermined threshold, say $0.1$, to detect small matrix elements that should be dropped. It is also assumed that the pivots $U_{i,i}$ are not too small in magnitude, so the algorithm doesn’t fail due to division by (almost) 0. (This is guaranteed, e.g., when the original matrix $A$ is an M-matrix [49].)

# Algorithm 17.1.

+   1. Initialize $L=(L_{i,j})_{0\le i,j<N}$ to be the identity matrix $I$.
+   
+   2. Initialize $U=(U_{i,j})_{0\le i,j<N}$ to be the same matrix as $\hat{A}$.
+   
+   3. For $i=0,1,2,3,\ldots,N-1$, do the following:
+   
+      - For $j=0,1,2,\ldots,i-1$, do the following:
+   
+        (a) Define
+        $$factor=U_{i,j}/U_{j,j}.$$
+   
+        (b) Set
+        $$U_{i,j}\leftarrow 0.$$
+   
+        (c) If $|factor|\ge threshold$, then do the following:
+   
+        - For $k=j+1,j+2,\ldots,N-1$, set
+          $$U_{i,k}\leftarrow U_{i,k}-factor\cdot U_{j,k}.$$
+   
+        - Set
+          $$L_{i,j}\leftarrow factor.$$
+   
+      - For $j=i+1,i+2,\ldots,N-1$, if
+        $$|U_{i,j}|\le threshold\cdot|U_{i,i}|,$$
+        then set
+        $$U_{i,j}\leftarrow 0.$$

Next, we provide the detailed implementation of the ILU factorization. The function "factorize" is a member of the "sparseMatrix" class, so it can access its "item" field, which contains the addresses of the rows. Using this access privilege, the "factorize" function modifies the current "sparseMatrix" object and converts it from the original matrix $A$ into the upper triangular factor $U$. In the process, it also creates the lower triangular factor $L$ and returns it as output. Of course, a copy of the original matrix $A$ must also be stored elsewhere for safekeeping before the function is called, because the current "sparseMatrix" object is changed.