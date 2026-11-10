```
```text
for (j = 2, j <= jl, j++)
    for (ii = 2, ii <= il, ii+=b) {
        for (i = ii; i <= min(ii+b-1,il); i++) {
            ib          = i-ii+1;
            AP[ib]      = ...;
            T           = 1.0/(1.0 + AP[ib]);
            D[2,ib]     = T*AP[ib];
            DW[1,2,j,i] = T*DW[1,2,j,i];
        }
        for (i = ii; i <= min(ii+b-1,il); i++) {
            for (k=3, k <= kl-1, k++) {
                ib          = i-ii+1;
                AM          = AP[ib];
                AP[ib]      = ...;
                T           = ...AP[ib]-AM*D[ib,k-1]...;
                D[ib,k]     = T*AP;
                DW[1,k,j,i] = T*(DW[1,k,j,i]+DW[1,k-1,j,i])...;
            }
            ...
            for (i = ii; i <= min(ii+b-1,il); i++)
                for (k=kl-1, k>=2, k--) {
                    DW[1,k,j,i] = DW[1,k,j,i] + [D?][1,k+1,j,i];
                    /* Ends code to be executed by processor (j, i) */
                }
        }
    }
```
```

Figure 11.66: Excerpt of Fig. 11.23 after partitioning, array contraction, and blocking

+   2. Apply Algorithm 11.71 to the SPMD program produced in Step 1 to optimize its locality.

# 11.10.5 Exercises for Section 11.10

**Exercise 11.10.1:** Perform array contraction on the following vector operations:

```
```text
for (i=0; i<n; i++) T[i] = A[i] * B[i];
for (i=0; i<n; i++) D[i] = T[i] + C[i];
```
```

**Exercise 11.10.2:** Perform array contraction on the following vector operations: