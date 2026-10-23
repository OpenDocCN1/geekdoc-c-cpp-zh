destructor built in the C++ compiler, which is invoked automatically at the end of every call to the above destructor.

Because the "dimension" field is protected, we need a public function to read it from ordinary classes that are not derived from the "dynamicVector" class:

```
int dim() const{
    return dimension;
} // return the dimension
```

The "operator()" defined below returns a reference to the 'i'th component in the current "dynamicVector" object. Because this reference is nonconstant, it can be changed by the user. The "operator[]", on the other hand, returns a constant reference, so the 'i'th component can only be read by it:

```
T& operator()(int i){
    return component[i];
} // read/write ith component
```

```
const T& operator[](int i) const{
    return component[i];
} // read only ith component
```

We also declare some member arithmetic operators that operate on the current "dynamic Vector" object. The complete definition will be given later on.

```
const dynamicVector& operator+=(const dynamicVector&);
const dynamicVector& operator-=(const dynamicVector&);
const dynamicVector& operator*=(const T&);
const dynamicVector& operator/=(const T&);
};
```

This concludes the block of the "dynamicVector" class.

We now define the functions that are only declared above. In the constructor defined below, memory for the array of components is allocated in the initialization list, provided that the dimension is nonzero: this dynamic memory allocation is done by the "new" command. The address returned by this command is placed in the "component" field for future access:

```
template<class T>
dynamicVector<T>::dynamicVector(
    int dim = 0, const T& a = 0)
    : dimension(dim), component(dim ? new T[dim] : 0){
for(int i = 0; i < dim; i++)
    component[i] = a;
} // constructor
```

The same approach is used in the copy constructor:

```
template<class T>
dynamicVector<T>::dynamicVector(const dynamicVector<T>& v)
```