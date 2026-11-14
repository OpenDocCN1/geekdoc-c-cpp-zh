```
double *x= new double[size];
double *b= new double[size];

for (int i=0; i<size; i++)
    b[i] = 1.0 ;

for (int i=0; i<size; i++)
    x[i] = 0.0 ;

// set A and b
cg(size, x, b, diag_prec, 1e-9);

return 0 ;
}
```