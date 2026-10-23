Here is the overloaded “max()” function that produces the alternative right-hand side in Chapter 23, Section 23.10. This function takes two extra arguments: the (symmetric) sparse matrix “A” and the list “u” of the original (blurred) images:

```
template<class T>
const dynamicVector<T>
max(const sparseMatrix<T>&A,
    const list<dynamicVector<T> >&u,
    const list<dynamicVector<T> >&f){
    dynamicVector<T> maxu(u[0].dim(),0.);
    for(int j=0; j<u[0].dim(); j++){
```

For each component (or pixel) j, we first find the index “maxi” of the image with maximal right-hand side (in modulus) at that pixel:

```
    int maxi = 0;
    for(int i=1; i<u.size(); i++)
        if(fabs(f[i][j])>fabs(f[maxi][j]))
            maxi = i;
```

The index “maxi” is now used to multiply the relevant row (or column) in “A” and add it to “maxu”:

```
    maxu += A[j] * u[maxi][j];
}
return maxu;
}  // alternative right-hand side
```

In order to modify the original multigrid fusion algorithm, we also need another binary arithmetic operator that divides the items in a given list by a constant object of any type:

```
template<class S, class T>
const list<T>
operator/(const list<T>&l, const S&R){
    list<T> Rl(l.size(), 1.0);
    for(int i=1; i<l.size(); i++)
        Rl(i) = l[i] / R;
    return Rl;
}  // list divided by an object ‘R’
```

With this operator, the user can write “f/R” to divide the items in the well-defined list f by the well-defined object R. In particular, if f is a list of vectors and R is a “multigrid” object, then the result is the list of vectors obtained by applying the inverse of the fine-level coefficient matrix to the original vectors in f. (See the definition of “operator,()” in Chapter 23, Section 23.13.)

The overloaded function “fuse()” that reimplements the multigrid fusion algorithm with the alternative right-hand side must also take the extra argument “um” that contains the original (blurred) images u^(1), u^(2), ..., u^(m).