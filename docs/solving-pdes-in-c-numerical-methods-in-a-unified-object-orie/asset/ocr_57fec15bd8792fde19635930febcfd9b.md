```
if((i==l)&&(j==m)&&(k==n)){
    T coef = factorial(i) * factorial(j) *
        factorial(k);
    if(item[I])
        item[I]->append(coef,J);
    else
        item[I] = new row<T>(coef,J);
}
```

Furthermore, the next 10 rows are associated with partial derivatives evaluated at the corner (1,0,0). Clearly, at this corner, the (n,m,l)th partial derivative is nonzero only for monomials that their y-power is exactly m, their z-power is exactly l, and their x-power is at least n:

```
if((i==l)&&(j==m)&&(k>=n)){
    T coef = factorial(i) *
        factorial(j) * C(k,n);
    if(item[10+I])
        item[10+I]->append(coef,J);
    else
        item[10+I] = new row<T>(coef,J);
}
```

Similarly, the next 10 rows are associated with partial derivatives evaluated at the corner (0,1,0). Clearly, at this corner, the (n,m,l)th partial derivative is nonzero only for monomials that their x-power is exactly n, their z-power is exactly l, and their y-power is at least m:

```
if((i>=l)&&(j>=m)&&(k==n)){
    T coef = factorial(i) *
        C(j,m) * factorial(k);
    if(item[20+I])
        item[20+I]->append(coef,J);
    else
        item[20+I] = new row<T>(coef,J);
}
```

Similarly, the next 10 rows are associated with partial derivatives evaluated at the corner (0,0,1). Clearly, at this corner, the (n,m,l)th partial derivative is nonzero only for monomials that their x-power is exactly n, their y-power is exactly m, and their z-power is at least l:

```
if((i>=l)&&(j==m)&&(k==n)){
    T coef = C(i,l) * factorial(j) *
        factorial(k);
    if(item[30+I])
        item[30+I]->append(coef,J);
    else
        item[30+I] = new row<T>(coef,J);
}
```

This completes the first 40 rows in the matrix.