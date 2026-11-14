```
Inv= 0;
for (unsigned k= 0; k < n; ++k)
Inv[irange{0, k+1}][k]=
upper_trisolve(A[irange{0, k+1}][irange{0, k+1}],
unit_vector(k, k+1));
```