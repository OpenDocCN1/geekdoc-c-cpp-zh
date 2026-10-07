# 516 THE MATRIX AND VECTOR CLASSES

```
cout << "Singular system!" << endl;
exit(1);
}
return b;
```

Vector Matrix::forward(const Vector& RHS) const
double temp;///temporary storage

Vector b(nRows, 0.);//solution matrix

```
//initialize the recursion
if(pA[0][0] != 0)
  b.pa[0] = RHS.pA[0]/pA[0][0];
else
  cout << "Singular system!" << endl;
  exit(1);

//now work through the remaining rows
for(int i=1; i<nRows; i++){
  if(pA[i][i] != 0) {
    temp = RHS.pA[i];
    for(int k =0; k<i; k++)
      temp -= b.pa[k]*pA[i][k];
    b.pa[i] = temp/pA[i][i];
  }
  else
    cout << "Singular system!" << endl;
    exit(1);
}
return b;
```

Vector Matrix::gauss(const Vector& RHS) const
double multiplier = 0;
Matrix G(nRows, nRows, pA);
Vector h(nRows, RHS);

for(int j= 0; j < nCols; j++)//column to be swept

```
for(int jj = j; jj < nCols; jj++){//current operation
if(G[jj][j] != 0)
  cout << "Oops! Division by O!" << endl;
  exit(1);

for(int i = j+1; i < nRows; i++){
  multiplier = G[i][j]/G[jj][j];
  G.pa[i][jj] = G.pa[i][jj]-multiplier*G.pa[jj][jj];
}
```

```
for(int i = j+1; i < nRows; i++)//do the same to the RHS
multiplier = G[i][j]/G[jj][j];
h.pa[i] = h.pa[i]-multiplier*h.pa[j];

```

//now solve
Vector b = G.backward(h);
return b;

Vector Matrix::cholesky(const Vector& RHS) const
double temp = 0;