rather than a reference to it, as is indicated by the word "double" (rather than "double&") that precedes the function name.

Another possible strategy to implement the read-only operator is to define the returned variable as a constant reference to double:

```
const double& operator[](int i) const{
    return coordinate[i];
} // read-only ith coordinate
```

This approach is preferable if the coordinates are themselves big objects that are expensive to copy: here, however, since they are only "double" objects, it makes no difference whether they are returned by value or by constant reference.

The "operator[]" function can also be implemented as a "read-write" operator as follows:

```
double& operator[](int i) {
    return coordinate[i];
} // read/write ith coordinate (risky)
```

This version returns a nonconstant reference to the 'i'th coordinate, which can be further changed even from ordinary functions that are neither members nor friends of the "point" class. With this version, a call of the form "P[i]" can be made only if the "point" object 'P' is nonconstant; otherwise, its 'i'th coordinate is constant and cannot be referred to as nonconstant, for fear that it will be changed through it. For this reason, the reserved word "const" before the '{' character that opens the function block is missing: this indicates that the current object can be changed by the function and, therefore, cannot be constant.

The latter version, however, is somewhat risky, because the coordinates can be changed inadvertently, which will spoil the original "point" object. This version must, therefore, be used with caution and only when necessary.

It is also possible to define "operator()" rather than "operator[]" by using parentheses. The 'i'th coordinate in the "point" object 'P' is then read as "P(i)" rather than "P[i]". Here, there is no real difference between the two styles. In other cases, however, "operator()" may be more useful because it may take any number of arguments, whereas "operator[]" must take exactly one argument.

The only thing left to do in the "point" template class is to define explicitly the copy constructor declared above. This task is discussed and completed below.

The "point" template class must have a copy constructor, because the default copy constructor provided by the compiler does the wrong thing. Indeed, this copy constructor just copies every data field from the copied object to the constructed object. Since the field in the "point<>" template class is an array, it contains the address of a "double" variable. As a result, the default copy constructor just copies this address to the corresponding field in the constructed object, and no new array is created, and both objects have the same array in their data field. The result is that the constructed object is not really a new object but merely a reference to the old one, which is definitely not what is required. The copy constructor in the code below, on the other hand, really creates a new object with the same data as in the old one, as required.

The words "template<int N>" before the definition indicate that this is a template function. The prefix "point<N>::" before the function name indicates that this is a definition of a member function: