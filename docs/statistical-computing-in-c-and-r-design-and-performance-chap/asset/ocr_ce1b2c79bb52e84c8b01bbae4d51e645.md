# SOLVING LINEAR EQUATIONS

```
exit(1);
}
//now work through the remaining rows
for(int i = nrows - 2); i >= 0; i--) {
  if ((*this)[i][0] == 0) {
    temp = RHS.PA[i];
    up = std::min(nrows, q + 1);
    for(int k = 1; k < up; k++) {
      temp = b.PA[i+k]*(*this)[i][k];
    }
    b.PA[i] = temp/(*this)[i][0];
  } else {
    cout << "Singular system!" << endl;
    exit(1);
  }
}
return b;
```

This is a straightforward modification of the Vector class that is necessary to make this in Appendix D. There is an important change to make this and subsequent methods work: namely, the pdBand class must be added as a friend to class Vector. This allows us to write statements such as b.PA[i] for a Vector object b without producing compilation errors. If status is not inherited from class Matrix,

```
friend class pdBand;
```

must be explicitly placed in the Vector class header.
The Cholesky recursion that we employ will produce an upper-triangular matrix that will be held in storage mode. This will work for the final back-solving step in the Cholesky method. However, the first step requires us to solve a lower triangular system using the transpose of the upper-triangular matrix that is being held in a compressed storage format. Symmetry considerations ensure that all the information that needed for forward solving is available from the compressed, upper-triangular, array. The only question is how to extract it. The solution is provided by observing that, due to symmetry and relation (7.17), (7.6) can be expressed as

> $b_j = c_j - \sum_{k=max(1,j-j)}^{j-1} a_{jk}b_k / a_{jj}$
$$c_j = c_j - \sum_{k=max(1,j-j)}^{j-1} \tilde{a}_{(j-k+1)}\tilde{b}_k / \tilde{a}_0$

with the $b_j$ and $c_j$ representing the elements of the solution vector and the right-hand vector, respectively. The next listing uses this formula to produce the code for our solution method.

```
Vector pdBand::bandForward(const Vector& RHS) const {
double temp;;temporary storage
int low;
int nrows = this->getNRrows();
Vector b(nrows, 0.0);//solution vector
//initialize recursion on first row of right-hand side
```