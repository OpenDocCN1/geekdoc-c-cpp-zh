Furthermore, by setting the right-hand side b to be the jth column in the identity matrix (stored in "ej" in the code below), the above function produces the jth column in the inverse matrix A⁻¹:

```
template<class T>
const dynamicMatrix<T>
invert(const dynamicMatrix<T>&LU,
    const dynamicVector<int>&P) {
dynamicMatrix<T> inverse(LU.height(),LU.width());
dynamicVector<T> zero(LU.height(),0.);
for(int j=0; j<LU.width(); j++){
    dynamicVector<T> ej = zero;
    ej(j) = 1.;
    dynamicVector<T> columnJ = invert(LU,P,ej);
    for(int i=0; i<LU.height(); i++)
        inverse(i,j) = columnJ[i];
}
    return inverse;
} // invert a matrix using its LU factorization
```

This algorithm avoids the expensive recursion used in Cramer's formula, and thus can be used for larger matrices as well.

# 3.21 Using the Heap Memory Efficiently

The "new" command used in the above dynamic objects allocates memory (during run time) in the so-called "heap" memory, which is the most easily accessed part of the secondary memory, and returns a pointer to it, which is stored in the so-called "stack" memory, which is a part of the primary memory. This memory should be released at the end of the block in which such a dynamic object is defined. This should be done by the C++ compiler, which invokes the relevant destructor implicitly.

The C++ compiler, however, may often decline to call the destructor at the end of the relevant block. In fact, the destruction can be delayed until there are many objects to destroy. Unfortunately, destroying many objects together may be far more expensive than destroying them one by one.

Indeed, the most time-consuming part of the destruction is to locate the memory occupied by the object in the heap memory. Because the C++ compiler is originally programmed to serve the users of the Windows operating system and give them real-time responses, it doesn't care to complete one task before moving ahead to the next task. Instead, it completes only a small portion of the first task, then starts the next task, then goes back to the first task to complete another small portion of it, and so on.

This strategy may make sense for operating systems to let the user have simultaneous real-time progress in every respect of the project that he/she wants to accomplish, but not for running C++ programs as required here. Indeed, because the most time-consuming part in the destruction task is to find the heap memory that should be released, it makes much more sense to look for it only once and release it in one go, rather than halting and then having to look for it once again.