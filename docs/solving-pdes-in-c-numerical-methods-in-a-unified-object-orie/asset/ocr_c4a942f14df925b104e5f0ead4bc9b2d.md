"rowSumCoarse" and "addCoarse" are member functions of the "row" class. "rowSumCoarse" sums only those elements in the "row" argument that lie in columns j ∈ c for which the corresponding element in the current "row" object is also nonzero:

```
const T rowSumCoarse(const row<T>&r,
    const dynamicVector<int>&coarse) const{
    T contribution =
        coarse[getColumn()] ? r[getColumn()] : 0.;
    return next ? contribution +
        ((row<T>*)next)->rowSumCoarse(r,coarse)
        : contribution;
} // row sum at coarse points
```

"addCoarse" adds values to nonzero elements in the current "row" object that lie in columns j for which j ∈ c:

```
void addCoarse(const row<T>&r,
    const dynamicVector<int>&coarse){
    if(coarse[getColumn()])
        item += r[getColumn()];
    if(next) ((row<T>*)next)->addCoarse(r,coarse);
} // add values at coarse points
```

Note that the vector of integers "coarse" that indicates the coarse grid is passed to the above functions by reference rather than by name to avoid highly expensive and unnecessary reconstructions, particularly in the inner recursive calls.

Next, we implement the assignment operator of the "multigrid" class in Chapter 17, Section 10. This operator uses the recursive nature of the "multigrid" class: it first assigns the matrices corresponding to the finest grid and is then applied recursively to the coarser grids in the "next" field:

```
template<class T>
const multigrid<T>&
multigrid<T>::operator=(const multigrid<T>&mg){
    if(this != &mg){
        A = mg.A;
        U = mg.U;
        L = mg.L;
        P = mg.P;
        R = mg.R;
        if(next){
            if(mg.next)
                *next = *mg.next;
            else{
                delete next;
                next = 0;
            }
        }
    }
```